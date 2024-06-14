- **Installation des packages**
	`Yum install bind`

- **Vérifier l'installation des packages :**
	`Rpm –aq bind`

- **Le chemin de fichier de configuration**
	`/etc/named.conf`

- **la configuration du service DNS**
	`vi /etc/named.conf`

```dns
listen-on port 53 { 127.0.0.1;192.168.10.20 };

allow-query { 192.168.10.0/24; };

zone id.ma in {
	type master ;
	file id.ma.dir ;
	allow-transfer{192.168.10.21;};
	notify yes;
};

zone 10.168.192.in-addr.arpa in {
	type master ;
	file id.ma.inv;
	allow-transfer{192.168.10.21;};
	notify yes;
};
```

	`vi /var/etc/named/id.ma.dir`
```dns
$TTL1D
@ IN SOA srvdns.id.ma. pc.id.ma. (
	64; serial number
	3600 ; refres
	600; retry
	86400 ; expire
	3600 ; minimum TTL
)

@ IN NS srvdns.id.ma
@ IN MX 10 mail.id.ma
srvdns.id.ma IN A 192.168.10.1
srvdns.id.ma IN AAAA 201:ABVD::2
www IN A 192.168.10.1
```

`vi / var/etc/named/id.ma.inv`
```
$TTL1D
@ IN SOA srvdns.id.ma. pc.id.ma. (
	64; serial number
	3600 ; refres
	600; retry
	86400 ; expire
	3600 ; minimum TTL
)
@ IN NS srvdns.id.ma
2 IN PTR srvdns.id.ma
```