
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



### Iter-vlan

```
Router(config)#router rip
Router(config-router)# 
Router(config-router)# no auto-summary
```

### VTP

- Definition:
	- protocole de cisco pour la gestion centralise de vlan
 ```
 S(config)#vtp domain domain.com
 S(config)#vtp password password
 S(config)#vtp mode server/client
 S(config)#vtp version 2
```

## STP
> port bloque plus grand numero interface

- def:
	- protocole qui permet la redondance au niveau de la couche 2 en éliminant les boucles. 

#### commandes STP




## MLS



>*802.1Q is a standard defined by the Institute of Electrical and Electronics Engineers (IEEE) for virtual LAN (VLAN) tagging in Ethernet networks. It is also commonly referred to as VLAN tagging or simply "dot1q."*


 -- | Dynamique Automatique | Dynamique souhaitable | Trunk | Accès 
 -- | --------------------- | --------------------- | ----- | ----- 
**Dynamique Automatique** | Accès | Trunk | Trunc | Accès 
**Dynamique souhaitable** | Trunc | Trunc | Trunc | Accès 
**Trunk** | Trunc | Trunc | Trunc | Connectivité limitée 
**Accès** | Accès | Accès | Connectivité limitée | Accès
