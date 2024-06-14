
- installer le package `dhcp`:
```
sudo dnf install dhcp
```

- verifier lexistance du package dhcp:
```
rpm -qa dhcp
```

- config file : 
`/etc/dhcp/dhcpd.conf`

- lancer le service `dhcp`
```
systemctl (re)start dhcpd
# lancer avec demarrage
systemctl enable dhcpd
```
- la configuration du service DHCP

`vim /etc/dhcp/dhcpd.conf`

```dhcp
subnet 192.168.1.0 netmask 255.255.255.0 {
	option broadcast-address 192.168.1.255;
	range192.168.1.10 192.168.1.100;
	option domain-name-servers
	192.168.1.254;
	option domain-name "tri.lan";
	option routers 192.168.1.1;
	default-lease-time 600;
	max-lease-time 7200;
};
```