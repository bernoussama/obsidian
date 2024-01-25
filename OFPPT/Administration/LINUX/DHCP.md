
- verifier lexistance du package dhcp:
```
rpm -qa dhcp
```

- installer le package `dhcp`:
```
sudo dnf install dhcp
```

- config file : `/etc/dhcp/dhcpd.conf`

- lancer le service `dhcp`
```
systemctl (re)start dhcpd
# lancer avec demarrage
systemctl enable dhcpd
```