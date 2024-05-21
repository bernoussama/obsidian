# Cloudflare tunnel
---
```bash

# download cloudflared for arm
wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-arm64.deb

# install it
sudo dpkg -i cloudflared-linux-arm64.deb

# checking if its installed
cloudflared version

# login to cloudflare account and authorize on a site
cloudflared tunnel login

# create a tunnel
cloudflared tunnel create {tunnel-name}

# create config directory
mkdir -p /etc/cloudflared/

# populate config file
sudo vim /etc/cloudflared/config.yml

# remove old config if any
sudo rm -rf /etc/systemd/system/cloudflared.service

# install cloudflared as a service
sudo cloudflared service install

# start cloudflared service
sudo systemctl start cloudflared

# enable to start at system restart
sudo systemctl enable cloudflared

# add cname to services in config (hostname)->(tunnel-id.cfargotunnel.com)
cloudflared tunnel route dns {tunnel-name} {hostname}
```
