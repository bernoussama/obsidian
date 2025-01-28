 https://chat.deepseek.com/a/chat/s/f375b4f7-91a0-4948-a4ee-6a2527e1969f
 version that supports connecting to a remote server with a public IP address:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <linux/if.h>
#include <linux/if_tun.h>
#include <sys/ioctl.h>
#include <pthread.h>
#include <openssl/evp.h>

#define SERVER_PORT 5555
#define CLIENT_IP "10.8.0.2"
#define SERVER_TUN_IP "10.8.0.1"
#define NETMASK "255.255.255.0"
#define BUFFER_SIZE 2000
#define KEY "0123456789abcdef0123456789abcdef" // 32 bytes for AES-256
#define IV "abcdef0123456789" // 16 bytes for AES-128

int tun_fd;
int sock_fd;
struct sockaddr_in remote_addr;

int tun_alloc(char *dev) {
    struct ifreq ifr;
    int fd, err;

    if ((fd = open("/dev/net/tun", O_RDWR)) < 0) {
        perror("open");
        return -1;
    }

    memset(&ifr, 0, sizeof(ifr));
    ifr.ifr_flags = IFF_TUN | IFF_NO_PI;

    if (*dev)
        strncpy(ifr.ifr_name, dev, IFNAMSIZ);

    if ((err = ioctl(fd, TUNSETIFF, (void *)&ifr)) < 0) {
        perror("ioctl");
        close(fd);
        return err;
    }

    strcpy(dev, ifr.ifr_name);
    return fd;
}

void configure_interface(char *dev, char *ip, char *netmask) {
    char cmd[1024];
    snprintf(cmd, sizeof(cmd), "ip link set dev %s up", dev);
    system(cmd);
    
    snprintf(cmd, sizeof(cmd), "ip addr add %s/%s dev %s",
             ip, netmask, dev);
    system(cmd);
}

void encrypt(unsigned char *plaintext, int plaintext_len, unsigned char *ciphertext) {
    EVP_CIPHER_CTX *ctx = EVP_CIPHER_CTX_new();
    int len;
    int ciphertext_len;

    EVP_EncryptInit_ex(ctx, EVP_aes_256_cbc(), NULL, 
                      (unsigned char *)KEY, (unsigned char *)IV);
    EVP_EncryptUpdate(ctx, ciphertext, &len, plaintext, plaintext_len);
    ciphertext_len = len;
    EVP_EncryptFinal_ex(ctx, ciphertext + len, &len);
    ciphertext_len += len;
    EVP_CIPHER_CTX_free(ctx);
}

void decrypt(unsigned char *ciphertext, int ciphertext_len, unsigned char *plaintext) {
    EVP_CIPHER_CTX *ctx = EVP_CIPHER_CTX_new();
    int len;
    int plaintext_len;

    EVP_DecryptInit_ex(ctx, EVP_aes_256_cbc(), NULL, 
                      (unsigned char *)KEY, (unsigned char *)IV);
    EVP_DecryptUpdate(ctx, plaintext, &len, ciphertext, ciphertext_len);
    plaintext_len = len;
    EVP_DecryptFinal_ex(ctx, plaintext + len, &len);
    plaintext_len += len;
    EVP_CIPHER_CTX_free(ctx);
}

void *tun_to_udp(void *arg) {
    unsigned char buffer[BUFFER_SIZE];
    unsigned char encrypted[BUFFER_SIZE + EVP_MAX_BLOCK_LENGTH];
    int n;

    while(1) {
        n = read(tun_fd, buffer, BUFFER_SIZE);
        if(n < 0) break;
        
        encrypt(buffer, n, encrypted);
        
        sendto(sock_fd, encrypted, n + EVP_MAX_BLOCK_LENGTH, 0,
              (struct sockaddr *)&remote_addr, sizeof(remote_addr));
    }
    return NULL;
}

void *udp_to_tun(void *arg) {
    unsigned char buffer[BUFFER_SIZE + EVP_MAX_BLOCK_LENGTH];
    unsigned char decrypted[BUFFER_SIZE];
    int n;
    socklen_t addr_len = sizeof(remote_addr);

    while(1) {
        n = recvfrom(sock_fd, buffer, BUFFER_SIZE, 0,
                    (struct sockaddr *)&remote_addr, &addr_len);
        if(n < 0) break;
        
        decrypt(buffer, n, decrypted);
        
        write(tun_fd, decrypted, n - EVP_MAX_BLOCK_LENGTH);
    }
    return NULL;
}

int main(int argc, char *argv[]) {
    char tun_name[IFNAMSIZ] = "tun0";
    pthread_t tun_thread, udp_thread;

    if (argc < 2) {
        fprintf(stderr, "Usage: %s server | client <server_ip>\n", argv[0]);
        exit(1);
    }

    tun_fd = tun_alloc(tun_name);
    if(tun_fd < 0) exit(1);

    // Configure network based on mode
    if(strcmp(argv[1], "server") == 0) {
        configure_interface(tun_name, SERVER_TUN_IP, NETMASK);
    } else if(argc > 2 && strcmp(argv[1], "client") == 0) {
        configure_interface(tun_name, CLIENT_IP, NETMASK);
    } else {
        fprintf(stderr, "Invalid arguments\n");
        exit(1);
    }

    // Setup UDP socket
    sock_fd = socket(AF_INET, SOCK_DGRAM, 0);
    memset(&remote_addr, 0, sizeof(remote_addr));
    remote_addr.sin_family = AF_INET;
    remote_addr.sin_port = htons(SERVER_PORT);

    if(strcmp(argv[1], "server") == 0) {
        struct sockaddr_in local_addr;
        memset(&local_addr, 0, sizeof(local_addr));
        local_addr.sin_family = AF_INET;
        local_addr.sin_port = htons(SERVER_PORT);
        local_addr.sin_addr.s_addr = INADDR_ANY;
        
        if(bind(sock_fd, (struct sockaddr *)&local_addr, sizeof(local_addr)) < 0) {
            perror("bind");
            exit(1);
        }
    } else {
        if(argc < 3) {
            fprintf(stderr, "Client mode requires server IP\n");
            exit(1);
        }
        
        if(inet_pton(AF_INET, argv[2], &remote_addr.sin_addr) != 1) {
            perror("Invalid server IP");
            exit(1);
        }
    }

    pthread_create(&tun_thread, NULL, tun_to_udp, NULL);
    pthread_create(&udp_thread, NULL, udp_to_tun, NULL);

    pthread_join(tun_thread, NULL);
    pthread_join(udp_thread, NULL);

    close(sock_fd);
    close(tun_fd);
    return 0;
}
```

**Key Changes Made:**

1. **Command-line Arguments:**
   - Server: `./vpn server`
   - Client: `./vpn client <server_public_ip>`

2. **Remote IP Configuration:**
   - Client now takes server IP as a command-line argument
   - Removed hardcoded `SERVER_IP` macro

3. **Improved Argument Handling:**
   - Better error checking for command-line arguments
   - Proper input validation for IP addresses

**Usage Instructions:**

1. **Compile the code:**
```bash
gcc vpn.c -o vpn -lssl -lcrypto -lpthread
```

2. **On the Server (with public IP):**
```bash
sudo ./vpn server
# Enable IP forwarding and NAT
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

3. **On the Client:**
```bash
sudo ./vpn client <server_public_ip>
# Set default route through VPN
sudo ip route add default via 10.8.0.1 dev tun0
```

**Important Notes:**

1. **Firewall Configuration:**
   - Ensure the server's firewall allows UDP traffic on port 5555
   - For cloud providers, check security group/network ACL settings

2. **Network Routing:**
   - The server must have proper NAT configuration to route traffic
   - Adjust `eth0` in the NAT command to match the server's public interface

3. **Testing Connectivity:**
```bash
# On client after connecting:
ping 10.8.0.1  # Should reach server's TUN interface
curl ifconfig.me  # Should show server's public IP
```

4. **Security Considerations:**
   - This is still a basic implementation - not production-ready
   - Consider adding authentication and proper key exchange
   - Use TLS or WireGuard for real-world applications

This modified version allows the client to connect to a VPN server using its public IP address while maintaining the same encryption and tunneling functionality. The server can now be deployed on any internet-accessible machine with proper network configuration.