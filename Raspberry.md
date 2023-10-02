## SSH
install rapberry pi os lite 64bit with ssh



## disable firewall

## Enable or Disable Firewall: nftables

As long as your Raspberry Pi OS is up to date, it should have nftables installed as the default firewall. Here is how to enable or disable it on the Raspberry Pi.

1. Check on the status of nftables to see if it is currently running:
    
    `$ sudo systemctl status nftables.service`
    
2. Start (turn on) the nftables firewall service:
    
	`$ sudo systemctl start nftables.service`
    
3. Stop (turn off) the nftables firewall service:  
    
    `$ sudo systemctl stop nftables.service`
    
4. Configure the nftables firewall to start by default upon system boot:
    
    `$ sudo systemctl enable nftables.service`
    
5. Configure the nftables firewall to be turned off by default upon system boot:
    
    `$ sudo systemctl disable nftables.service`
    
6. Check the currently configured nftables firewall rules:
    
    `$ sudo nft list ruleset`
    
7. Flush (delete) all currently configured nftables firewall rules – this will essentially make the firewall accept everything, but not actually turn it off:
    
    `$ sudo nft flush ruleset`

## Install and setup cloudflared
---
> sources
https://blog.jeffryanto.live/index.php/2022/12/23/cloudflare-tunnel-on-raspberry-pi/
https://blog.cloudflare.com/ssh-raspberry-pi-400-cloudflare-tunnel-auditable-terminal/
---
 ### download cloudflared and install cloudflared:
 ```shell
wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-arm64.deb && dpkg -i cloudflared-linux-arm64.deb
 ```


#### commands to disable rpi firewall
```bash
sudo systemctl status nftables.service
sudo systemctl stop nftables.service
sudo systemctl disable nftables.service
```

### configure cloudflare
 ```bash
cloudflared tunnel login #login
cloudflared tunnel create <tunnelName> # create a tunnel
sudo apt install vim # install vim
cd ~/.cloudflared/
touch config.yaml # create a config file
vim config.yaml # put the config in it


sudo cloudflared --config ./config.yaml service install 
# start the cloudflared daemon

sudo vim /etc/cloudflared/config.yml # change the running config
sudo systemctl restart cloudflared # restart to config take change
```
   - Example config
```yaml
 tunnel: <YourTunnelID>
credentials-file: /home/pi/.cloudflared/<YourTunnelID>.json #credential file location
ingress:
  - hostname: ssh.example.com
    service: ssh://localhost:22
  - hostname: portainer.example.com
    service: http://localhost:9443
    originRequest:
      noTLSVerify: true
  - hostname: homarr.example.com
    service: http://localhost:7575
    originRequest:
      noTLSVerify: true
  - service: http_status:404
    # catch all rule responds 404 for anything not one of the above
```



### install speedtest-cli (could be useful)
```bash
sudo apt install speedtest-cli
speedtest-cli --secure
```