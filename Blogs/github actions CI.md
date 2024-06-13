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
sudo nginx -t

```bash
sudo certbot --nginx -d self-host.bernoussama.com
```