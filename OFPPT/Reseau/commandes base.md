Tâche | Commandes IOS
-- | --
Affichez l'état et la configuration des interfaces. | `S# show interfaces [interface-id]`
Affichez la configuration initiale actuelle. | `S# show startup-config`
Affichez la configuration courante.  | `S# show running-config`
Affichez les informations sur le système de fichiers Flash. |  `S# show flash`
Affichez l'état matériel et logiciel du système. |  `S# show version`
Affichez l'historique des commandes exécutées.  | `S# show history`
Affichez les informations IP d'une interface. | `S# show ip interface [interface-id]` OU `S# show ipv6 interface [interface-id]`
Affichez la table d'adresses MAC. |  `S# show mac-address-table` OU `S# show mac address-table`


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
`Switch (config) #interface vlan 1`
`Switch (config-if) #ip address 192.168.1.1 255.255.255.0`
`Switch (config-if) #no shutdown`

### affecter ip a interface
`Routeur (config) #interface fastEthernet 0/0`
`Routeur (config-if) #ip address 192.168.1.2 255.255.255.0`


