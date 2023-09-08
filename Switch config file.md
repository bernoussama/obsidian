Current configuration : 609 bytes
!
version 12.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
service password-encryption
!
hostname S1
!
enable secret 5 $1$mERr$3HhIgMGBA/9qNmgzccuxv0
!
!
!
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
!
interface FastEthernet1/1
!
interface FastEthernet2/1
!
interface FastEthernet3/1
!
interface FastEthernet4/1
!
interface FastEthernet5/1
!
interface Vlan1
 no ip address
 shutdown
!
banner motd ^Chello sniba^C
!
!
!
line con 0
!
line vty 0 4
 password 7 08751918
 login
line vty 5 15
 password 7 08751918
 login
!
!
!
!
end