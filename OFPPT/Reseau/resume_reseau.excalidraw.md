---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
VTP(Vlan Trunking Protocol) ^xxchJb5w

Etherchannel ^hnozxwKz

FHRP(First-hop redundancy protocol) ^ykWIjSCx

si priorite identique, plus grande addr ipv4 est active  ^R6GWmXGo

R1 (config) #interface fa0/0
R1 (config-if)#glbp 1 ip 192.168.1.3

R2 (config) #interface fa0/0
R2 (config-if) #glbp 1 ip 192.168.1.3

R1 (config-if) #glbp 1 priority 110
R1 (config-if) #glbp 1 preempt
Rl (config-if) #glbp 1 load-balancing [round-robin | weighted | host-dependant] ^GNHvKnV2

R1 (config) #interface fa0/0
R1 (config-if)#standby 1 ip 192.168.1.3

#R2 sera standby 
R2 (config) #interface fa0/0
R2 (config-if) #standby 1 ip 192.168.1.3

#rendre R1 active
R1 (config-if) #standby 1 priority 110
R1 (config-if) #standby 1 preempt ^DXyx4Swc

R1 (config) #interface fa0/0
R1 (config-if)#vrrp 1 ip 192.168.1.3

R2 (config) #interface fa0/0
R2 (config-if) #vrrp 1 ip 192.168.1.3

R1 (config-if) #vrrp 1 priority 110
R1 (config-if) #vrrp 1 preempt ^4G5PqKVI

HSRP(HotStandbyRouterProto.) ^1XSxc1KE

VRRP(Virtual Router Redundancy Protocol) ^omdQSUmk

GLBP(Gateway Load Balancing Protocol) ^XPWaSzJ9

Switch(config-if-range)# switchport mode trunk

PAGP et LACP
Switch(config-if-range)# channel protocol PAGP/LACP
Switch(config-if-range)#channel-group 1 mode ?
 
 active    Enable LACP unconditionally

 auto      Enable PAgP only if a PAgP device is detected

 desirable Enable PAgP unconditionally

 on        Enable Etherchannel only

 passive   Enable LACP only if a LACP device is detected

Switch(config)# interface Port-channel 1
Switch(config-if)# switchport mode trunk ^5PqeikJe

.1 ^l5tAjBCD

.2 ^ZIpwYKNk

> ^oN5FWDUn

"sir lport lkbir flpont racine dak li m9abl m3ah howa li ghaykoun blocke" ~Kakashi ^GMXZZPTC

STP(Spanning-Tree Protocol) ^xPyokqfN

Switch(config)# vtp domain ofppt.ma
Switch(config)# vtp password 123
Switch(config)# vtp mode ?
  client       Set the device to client mode.
  server       Set the device to server mode.
  transparent  Set the device to transparent mode. ^sxl0ELeW

vlan gestion ^9rxcAb5m



Switch(config)# spanning-tree vlan 100 priority <priorityvalue>

- Bach t rado l racine 3etih priority seghira 0 Ola 4096 Ola
8192 o mate nesach Default Priority hia 32768


Switch(config)# spanning-tree vlan 100,300 root primary
Switch(config)# spanning-tree vlan 200 root secondary


MLS1(config)#interface FastEthernet 0/1
MLS1(config-if)#spanning-tree vlan 1 cost 16


Switch(config)# spanning-tree mode {pvst | mst | rapid-pvst}


Switch(config)# Interface Fa0/1
Switch(config-if)# spanning-tree portfast
Switch(config-if)# spanning-tree bpduguard enable ^dM2w15Fe

mls(config)#int fa0/1
mls(config-if)#switchport trunk encapsulation dot1q
mls(config-if)#switchport mode trunk

mls(config)#int vlan 10
mls(config-if)#no sh
mls(config-if)#ip address 192.168.10.1 255.255.255.0
mls(config)#ip routing ^k0eylA5Q

DTP(Dynamic Trunking Protocol) ^15rfgRnA

Switch(config-if)# switchport nonegotiate ^YEz2GSkd

afficher config dtp ^Ad1ZAORT

switch# show dtp interface ^ItgUyr3z

+ Activer ou désactiver l'obsolescence statique pour le port sécurisé, ou  définir le temps ou le type d'obsolescence ^PI3M5HVr

switchport port-security maximum 1


switchport port-security violation ?
    shutdown(par defaut)  port passe immédiatement à l'état désactivé par erreur
    restrict  port supprime les paquets dont l'adresse source est inconnue. Un message syslog génèré.
    protect  port supprime les paquets avec des adresses source MAC inconnues. Aucun message Syslog n'est envoyé.


switchport port-security mac-address {static | dynamic | sticky} [mac-address]


switchport port-security aging time {absolute | inactivity} {aging_time(in second)} 
switchport port-security aging time off ^1WUfrwUC

OSPF ^jSWt9Or6

R0(config-router)# network 12.0.0.0 0.0.0.3 area 0 ^KmkLxCi0

ajouter reseau a OSPF ^jwOyvZEv

DHCP ^VUcOpRyo

ip dhcp excluded-address
ip dhcp pool {pool-name}
R1(dhcp-config)# network {address} [mask | / prefix-length]prefix-length]
R1(dhcp-config)# dns-server 172.16.1.254
R1(dhcp-config)# default-router <Gateway>
# HELPER (interface du reseau du pool)
R1(config-if)#ip helper-address <ip address-interface>

# DHCP show
show running-config | section dhcp
show ip dhcp binding
show ip dhcp server statistics
ipconfig /all


=> Command Protocol DHCP IPv6 “SLAAC ONLY”

R1 (config) # ipv6 unicast-routing
R1 (config) # interface g0/0
R1 (config-if) # no shutdown
R1 (config-if) # ipv6 enable
R1 (config-if) # ipv6 address 2001:10:10:A::1/64
R1 (config-if) # ipv6 address FE80::1 link-local

R1 (config-if) # ipv6 address 2001:10:10:C::1/64
R1 (config-if) # ipv6 nd other-config-flag
R1 (config-if) # ipv6 dhcp server LAN2 ^FMnZnVSl

BGP ^dQuhOCE6

Router(config)# router bgp 100

Router(config-router)# neighbor 20.20.20.2 remote-as 200


Router(config-router)# network 192.168.10.0 mask 255.255.255.0

show ip bgp
show ip bgp summary
show ip bgp neighbors
show ip bgp paths ^oClvgrYU

R0(config-router)# redistribute ospf 1 metric 1 ^fC9gNECv

R1(config-router)# router-id <router-id> ^7zHBy8zU

R(config-if)# ip ospf {1-255} area {0-255} ^uPbzaw8d

R1(config)# ipv6 router ospf (N° processus)
R1(config-rtr)# router-id X.X.X.X
R1(config)# interface (type interface)
R1(config-if)# ipv6 opsf {N° processus} area {N° area} ^KSdMckEf

- Le Dynamic Trunking Protocol (DTP) est utilisé sur les commutateurs Cisco 
pour négocier automatiquement la création de liens tronçonnés(trunk)
 entre switchs ^RbF591Pu

Role DTP:
 ^dVnTPVVC

Distance administrative:
DA = 110 ^oTccxkA9

access-list {access-list-number} {permit | deny |remark text} source [source-wildcard] [log] ^56dAHAhi

ip access-list access-list-number 69 deny 172.16.1.0 0.0.0.255  ^T9UEC8aM

router(config)# access-list {num} {permit | deny} {@machine | host | any} 0.0.0.0 ^SQMEAFZA

permit all or deny all ^JspHRI3R

ACL ^D1pn6gvU

DHCPv6 ^j3ejxfch

option o: other stateful config flag
option m: managed stateless config flag ^64c7VnvI

RIP:
DA = 120 ^2BPqY7gt

OSPF: DA = 110 ^P3HyBCdL

R1(config-router)# auto-cost reference-bandwidth <bandwidth-in-mbps>  ^FMLfS7sL

R0(config)# router ospf 1 ^gN1pf86m

R0(config-router)# network 11.0.0.0 0.0.0.3 area 0 ^Yw2x9hM9

ou ^ahgG5WqJ

R(config-if)# ip ospf priority {0-255} ^qkrbdR0c

creation pool dhcp :
R(config)#ipv6 dhcp pool Lan3
R(config-dhcpv6)#address prefix 2001:10:10:D::1/64
R(config-dhcpv6)#domain-name id.com
R(config-dhcpv6)#dns-server 2001:10:10:D::100

attribuer pool l interface:
R(config)#interface fa0/0
R(config-if)#ipv6 dhcp server Lan3

dhcpv6 sans-etat: 
kn5dmo b other-config-flag
 ^0NjNK8nt

PAT ^AvK7Z0Lf

Router(config)#ip nat inside source static <@ private> <@public>
R2(config)#interfaceSerial 0/0/0
R2(config-if)#ip nat inside
R2(config-if)#exit
R2(config)#interfaceSerial 0/1/0
R2(config-if)#ip nat outside
R2(config-if)#exit ^2gKOoPjr

R1# show access-lists ^3DJJeEqa

appliquer ACL sur lignes vty ^fpF9FgMx

R1(config-line)# access-class {access-list-number | access-list-name} {in | out} ^oGPaLsz4

statique: DA = 1 ^X8jSyGIE

R(config)#interface fa0/0
R(config-if)#ipv6 nd Managed-config-flag ^feBsaTps

dhcpv6 avec-etat: ^m2yqtG18

R(config)#interface fa0/0
R(config-if)#ipv6 nd other-config-flag ^jcl7oO39

CDP ^BoyAdxSF

VPN ^WV0dxvfh

S1(config)#vlan 10 
S1(config-vlan)#name data 
S1(config)#vlan 20 
S1(config-vlan)#name voix
S1(config)#vlan 10
 

S1(config)#vlan 10 
S1(config)#interface fa0/0
S1(config-if)#switchport access vlan 10
S1(config-if)#switchport voice vlan 20

R1(config)#ip dhcp excluded-address 192.168.10.1
R1(config)#ip dhcp excluded-address 192.168.20.1

R1(config)#ip dhcp pool LAN1
R1(dhcp-config)#network 192.168.10.0 255.255.255.0 
R1(dhcp-config)#default-router 192.168.10.1

R1(config)#ip dhcp pool VOICE
R1(dhcp-config)#network 192.168.20.0 255.255.255.0 
R1(dhcp-config)#default-router 192.168.20.1
R1(dhcp-config)#option 150 ip 192.168.20.1

R1(config)#telephony-service 
R1(config-telephony)#max-ephone 5
R1(config-telephony)#max-dn 5
R1(config-telephony)#ip source-address 192.168.20.1 port 2000
R1(config-telephony)#auto-reg-ephone 
R1(config-telephony)#auto assign 1 to 3

R1(config)#ephone-dn 1 
R1(config-ephone-dn)#number 1001

R1(config)#ephone-dn 1 
R1(config-ephone-dn)#mac-address @mac
R1(config-ephone-dn)#button {number 1}:{numero dn}
R1(config-ephone-dn)#button 1:1


coomandes dial-peer:: {paire de numérotation}:

R1(config)#dial-peer voice 1 voip
R1(config-dial-peer)#destination-pattern 1..
R1(config-dial-peer)#session target ipv4:172.16.20.1 ^SnU7YVCQ

commandes voip : ^Yh7WIa3Y

protocole permettant le partage de config
vlan entre differents switchs ^gGhQP0sJ

S1(config-if-vlan)# ip add 192.168.1.30 ^N6RjSwTG

S1(config)# interface vlan 30 ^3RqDShnB

MLS ^H0YDWyd8

vlan natif ^MNeNTfXX

S1(config-vlan)# switchport trunk native vlan 123 ^FtrfeR88

S1(config)# vlan 123 ^SVcYOW8n

S1(config-vlan)# switchport mode trunk ^oJ3rfwQg

(Cisco)PAGP ^mzq295Fx

(standard)LACP ^8fmjpJKl

R(config-if)#ip access-group {num} ^OpMZJRoQ

NAT ^UP37nCGC

R-SIEGE1(config)#ip access-list standard PAT
R-SIEGE1(config-std-nacl)#permit 172.16.10.1 0.0.0.255
R-SIEGE1(config)#ip nat inside source List PAT interface s1/1 overload ^6KWhUGlI

R-SIEGE1(config)#interface tunnel 1
R-SIEGE1(config-if)#ip address 172.16.0.1 255.255.255.252
R-SIEGE1(config-if)#tunnel mode gre ip
R-SIEGE1(config-if)#tunnel source se1/0
R-SIEGE1(config-if)#tunnel destination 44.168.0.2
 ^tz4CjYkY

VOIP ^pistZ24P

R-SIEGE2(config)#telephony-service 
R-SIEGE2(config-telephony)#max-ephone 10
R-SIEGE2(config-telephony)#max-dn 10
R-SIEGE2(config-telephony)#ip source-address 172.16.30.1 port 2000
R-SIEGE2(config-telephony)#auto-reg-ephone
R-SIEGE2(config-telephony)#auto assign 1 to 10


R-SIEGE2(config)#ephone-dn 1
R-SIEGE2(config-ephone-dn)#number 100
.......
R-SIEGE2(config)#ephone-dn 10
R-SIEGE2(config-ephone-dn)#number 110 ^ksZxm4Vw

def: ^xvvpjvHp

sur Switches Cisco (PVST) est active par defaut ^RvIcwPLf

+ Configurer root primary et secondary ^eJLU1hmh

+ interface access ^t9nbJt8g

+ Commands ^zin7OrxU

+ Configurer le « cost » STP d'une interface ^Jvcnh4Eu

+ Configurer Priority STP d'un switch ^ZA8k1VgX

Le protocole DTP permet de monter un lien 802.1Q entre deux
switchs ^g7t1rCdP

desactiver DTP ^K18JOPgY

PortSecurity ^3KkR22yY

+ nombre maximal d'adresses MAC autorisées sur un port ^z0h0O3Qa

+ définir configuration mac-address ^pwXzwr8C

+ définir le mode de violation de sécurité du port ^cCiM9tvn

cost ospf ^Uh0JqFaG

ajouter priorite ospf ^b2eWGVzX

desactiver mises a jour ospf ^iS34fTmm

OSPF v3 ^oXfIKDUH

R0(config-router)# passive-interface gig0/0 ^fy08mT65

Config OSPF ^eiGXPM12

affecter router-id ^GfWkl1UB

Ajouter routes OSPF au RIP ^uLHRrXUi

activer sur router ^CHUmZbB3

R#show cdp ^ku6vsc4W

R#show cdp Neighbor detail ^5EONJ3XT

R(config)#interface fa0/1 ^VnznkVPf

R(config-if)#cdp enable ^2b7xB0hE

R(config)#cdp run ^KI8Q3zZq

{nfse les commandes kytb9o 3la LLDP} ^Acse0tSs

commandes CDP supervision : ^lX8EiX7F

activer dans l'interface: ^pabKWGsw

SNMP ^C3mgaZ5I

config ^akxeaSTC

Router(config)# ip route 0.0.0.0 0.0.0.0 {@next-hop}
Router(config-router)# default-information originate ^Qo4a6SHl

creer vlan voice ^6SioP2qp


# Embedded files
128f445b5faabef838ac17cbd1073c7f923ffb59: [[Pasted Image 20231009225624_870.png]]
d837b303c5484bb1ec433ada63303786c41be39d: [[Pasted Image 20240201220257_042.png]]
76369cbc2242887021d45d9f7ea10fc28c132daf: [[Pasted Image 20240201220312_083.png]]
c3e05f9896cfafbfca3bbf00b5525cd66fdf360c: [[Pasted Image 20240202102327_790.png]]
9e732cb32a51ef59135dd51d37ad071a6a89b3e2: [[Pasted Image 20240208162636_276.png]]

%%
# Drawing
```compressed-json
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

IAA=
```
%%