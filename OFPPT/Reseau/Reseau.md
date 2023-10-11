
> **!! `S2(config)#no ip domain-lookup` !!**

Tâche | Commandes IOS
--------------------------------------------------- | --------------
Affichez l'état et la configuration des interfaces. | `S# show interfaces [interface-id]`
Affichez la configuration initiale actuelle. | `S# show startup-config`
Affichez la configuration courante.  | `S# show running-config`
Affichez les informations sur le système de fichiers Flash. |  `S# show flash`
Affichez l'état matériel et logiciel du système. |  `S# show version`
Affichez l'historique des commandes exécutées.  | `S# show history`
Affichez les informations IP d'une interface. | `S# show ip interface [interface-id]` OU `S# show ipv6 interface [interface-id]`
Affichez la table d'adresses MAC. |  `S# show mac-address-table` OU `S# show mac address-table`
afficher config stp | `S# show spanning-tree`


Type d'erreur |  Description
-- | --
Erreurs en entrée | Nombre total d'erreurs. Elles comprennent les trames incomplètes, trames géantes, pas de mémoire tampon, CRC, trame, débordement et comptes ignorés.
Trames incomplètes|  Paquets éliminés car ils sont inférieurs à la taille de paquet minimale définie pour le support. Par exemple, toute trame Ethernet inférieure à 64 octets est considérée comme incomplète.
Trames géantes | Paquets éliminés car ils sont supérieurs à la taille de paquet maximale définie pour le support. Par exemple, toute trame Ethernet supérieure à 1518 octets est considérée comme «géante».
CRC | Les erreurs CRC sont générées lorsque la somme de contrôle calculée ne correspond pas à la somme de contrôle reçue.
Erreurs en sortie | Somme de toutes les erreurs ayant empêché la transmission finale des datagrammes vers l'interface examinée.
Collisions | Nombre de messages retransmis à cause d'une collision Ethernet.
Collisions tardives | Collision se produisant après la transmission de 512 bits de la trame.

### affecter ip a vlan
```
Switch (config) #interface vlan 1
Switch (config-if) #ip address 192.168.1.1 255.255.255.0
Switch (config-if) #no shutdown
```
### affecter ip a interface
```
Routeur (config) #interface fastEthernet 0/0
Routeur (config-if) #ip address 192.168.1.2 255.255.255.0
```

#### password command :
```
Switch(config)# enable password 123
Switch(config)# enable secret 123
```
#### Encrypt all passwords
```
Switch(config)# service password-encryption
```

### banner 
```
R1(config)# banner motd $ this is a banner! $
```

## Telnet
```
Switch(config)# line vty 0 15
Switch(config-line)# password 123
Switch(config-line)# login
```
#### SSH config
```
R1(config)# line vty 0 4
R1(config)# password ofppt
R1(config)# login

R1(config)# ip domain-name ofppt.ma
R1(config)# crypto key generate rsa general-keys modulus 2048
R1(config)# username admin secret SuperSecretPassword
R1(config)# ip ssh version 2

R1(config)# line vty 0 4
R1(config)# transport input ssh
R1(config)# login local

# IF SWITCH
S1(config)# int vlan 99 # vlan 99 in this case is vlan gestion
S1(config-if)# ip address 192.168.99.10 # vlan 99 in this case is vlan gestion
```

 ```bash
ssh -l <username> <ip address(vlan gestion)>

telnet <ip address(vlan gestion)>
```
## RIP
```
Router(config)#router rip
Router(config-router)# 
Router(config-router)# no auto-summary
```

# MLS
```
mls(config)#int fa0/1
mls(config-if)#switchport trunk encapsulation dot1q
mls(config-if)#switchport mode trunk

mls(config)#int vlan 10
mls(config-if)#no sh
mls(config-if)#ip address 192.168.10.1 255.255.255.0
mls(config)#ip routing
```

# VTP(Vlan Trunking Protocol)
```
vtp domain ofppt.ma
vtp password 123
vtp mode server/client
```
# Etherchannel
```
Switch(config-if-range)# switchport mode trunk
# 
Switch(config-if-range)#channel-group 1 mode ?
 
 active    Enable LACP unconditionally

 auto      Enable PAgP only if a PAgP device is detected

 desirable Enable PAgP unconditionally

 on        Enable Etherchannel only

 passive   Enable LACP only if a LACP device is detected

Switch(config)# interface Port-channel 1
Switch(config-if)# switchport mode trunk
```

# FHRP(First-hop redundancy protocol)
## HSRP(HotStandbyRouterProto.)
```
R1 (config) #interface fa0/0
R1 (config-if)#standby 1 ip 192.168.1.3

R2 (config) #interface fa0/0
R2 (config-if) #standby 1 ip 192.168.1.3

R1 (config-if) #standby 1 priority 110
R1 (config-if) #standby 1 preempt
```
## VRRP(Virtual Router Redundancy Protocol)
```
R1 (config) #interface fa0/0
R1 (config-if)#vrrp 1 ip 192.168.1.3

R2 (config) #interface fa0/0
R2 (config-if) #vrrp 1 ip 192.168.1.3

R1 (config-if) #vrrp 1 priority 110
R1 (config-if) #vrrp 1 preempt
```
## GLBP(Gateway Load Balancing Protocol)
```
R1 (config) #interface fa0/0
R1 (config-if)#glbp 1 ip 192.168.1.3

R2 (config) #interface fa0/0
R2 (config-if) #glbp 1 ip 192.168.1.3

R1 (config-if) #glbp 1 priority 110
R1 (config-if) #glbp 1 preempt
Rl (config-if) #glbp 1 load-balancing [round-robin | weighted | host-dependant]
```

STP
```
Switch(config)# spanning-tree vlan 100 priority <priorityvalue>
- Bach t rado l racine 3etih priority seghira 0 Ola 4096 Ola
8192 o mate nesach Default Priority hia 32768
Switch(config)# spanning-tree vlan 100,300 root primary
Switch(config)# spanning-tree vlan 200 root secondary

Switch(config)# spanning-tree mode pvst
Switch(config)# spanning-tree mode rapid-pvst
Switch(config)# Interface Fa0/1
Switch(config-if)# spanning-tree portfast
Switch(config-if)#spanning-tree bpduguard enable
```
![[Pasted image 20231010040123.png]]
desactiver DTP
```
switchport nonegotiate
show dtp interface
```