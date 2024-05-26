## Setup
```sh
fortigate# config system admin
fortigate(admin)# edit admin
fortigate(admin)# set password 123456
fortigate(admin)# end

fortigate# config system interface
fortigate(interface)# show
# afficher les interfaces dispo
fortigate(inter)# edit port1
# editer config port1
fortigate(port1)# set type physical
fortigate(admin)# set ip 192.168.1.99
fortigate(admin)# set allowaccess ping http htps ssh
fortigate(admin)# end
fortigate(admin)# config system global
fortigate(global)# set cfg-save ?
automatic
manual
revert
fortigate(gloabl)# set cfg-save automatic
```