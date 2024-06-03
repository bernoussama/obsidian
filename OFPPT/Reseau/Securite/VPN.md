
Allows to create a virtual link between 2 hosts or networks over the internet

VPN benefits:
- Security (data encryption)
- Anonimity (using a virtual ip address)
- cost saving
- Scalability
VPN types
![[Séance 21 - Comprendre et mettre en place les VPN (Intro + GRE) - Partie 1 - Khalid KATKOUT - YouTube - 0-45-21.jpeg]]

ISAKMP(Internet Security And Key management Protocol): protocol pour gerer les cles
IKEv2(Internet Key Exchange): protocol resonsable pour l'echange de cle


Tunneling protocols:
- PPTP:
- L2TP:
- 
![[Séance 22 - Comprendre et mettre en place les VPN (IPSEC + DMVPN) - Partie 2 - Khalid KATKOUT - YouTube - 0-11-09.jpeg]]

```
crypto isakmp enable
crypto isakmp policy 10
 hash md5 
 authentication pre-share
 encryption des
 group 2
 lifetime 86400
 exit
 
crypto isakmp key P@assw0rd address 49.49.49.2 255.255.255.0        
crypto ipsec transform-set IPSECSET esp-des esp-md5-hmac 
exit

crypto map IPSECMAP 10 ipsec-isakmp 
 set peer 49.49.49.2
 set transform-set IPSECSET 
 match address 101
exit

access-list 101 permit ip 192.168.100.0 0.0.0.255 192.168.1.0 0.0.0.255
interface FastEthernet0/1
 crypto map IPSECMAP
exit
```