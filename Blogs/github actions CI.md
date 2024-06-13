```sh
sudo apt update && sudo apt upgrade
```

```sh
sudo apt install certbot nginx python3-certbot-nginx -y
```

```sh
cd /etc/nginx/
```

```bash
cp sites-enabled/default conf.d/static.conf
```

cp sites-enabled/default conf.d/static.conf

```nginx
server {
        listen 80;
        listen [::]:80;

        server_name self-host.bernoussama.com;

        root /var/www/bernoussama.com;
        index index.html;

        location / {
                try_files $uri $uri/ =404;
        }
}
```

```bash
sudo nginx -t
```


```bash
sudo iptables -I INPUT 6 -m state --state NEW -p tcp --dport 80 -j ACCEPT

sudo iptables -I INPUT 6 -m state --state NEW -p tcp --dport 443 -j ACCEPT

sudo netfilter-persistent save
```
make sure to have port 80 open on server and infra firewall(security group)
and that you also set A dns record of the domain name pointing to the server ip address
```bash
sudo certbot --nginx -d self-host.bernoussama.com -v
```

on the client
```bash
ssh-keygen -t ed25519 -f ~/.ssh/deploy
```
```bash
echo "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIBMbtTB/d8DXoGi+SqRyqLkWUFxfGZRCHiGshsWbn9s8 oussama@pop-os" | tee authorized_keys
```
```bash
chown -R deploy:deploy /var/www/bernoussama.com/
chmod 700 /var/www/bernoussama.com/.ssh/
chmod 500 /var/www/bernoussama.com/.ssh/authorized_keys
```