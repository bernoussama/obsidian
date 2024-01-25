## Les commandes Powershell 

I-Commades de Configuration Base de Serveur: 

Redémarrer le serveur :  

C:\>Restart-Computer 

Arrêter le serveur  

C:\> Stop-Computer  

Renommer l’ordinateur: 

C:\>Rename-Computer -NewName "TRI-DC" -Restart  

Configurer l’adresse IP :  

C:\>New-NetIPAddress –InterfaceIndex 12 –IPAdress 172.16.0.200 –PrefixLength 24 –DefaultGateway 172.16.0.1 

Ou bien 

C:\>New-NetIPAddress -InterfaceAlias "Ethernet" –IPAdress 172.16.0.200 –PrefixLength 24 –DefaultGateway 172.16.0.1  

 

C:\>Set-DNSClientServerAddresses –InterfaceIndex 12 –ServerAddresses 172.16.0.10,172.16.0.11  

Joindre le serveur au Domaine :  

C:\>Add-Computer –DomainName OFPPT.MA –Restart  

II-Commades de Configuration ADDS: 

Installer le rôle ADDS :  

C:\>Install-WindowsFeature -Name AD-Domain-Services -IncludeAllSubFeature -IncludeManagementTools  

Promouvoir le serveur en Contrôleur de domaine (Ajouter une nouvelle Forêt) :  

C:\>Install-ADDSForest -DomainName OFPPT.MA -InstallDns 

Promouvoir le serveur en Contrôleur de domaine (Ajouter un contrôleur dedomaine à un domaine existant ) :  

C:\>Install-ADDSDomainController -DomainName OFPPT.MA -InstallDns  

Promouvoir le serveur en Contrôleur de domaine (Ajouter un nouveau  domaine enfant ou supplémentaire) :  

C:\>Install-ADDSDomain -NewDomainName TRI.OFPPT.MA -ParentDomainName OFPPT.MA -DomainType ChildDomain -InstallDns  

 

Promouvoir le serveur en Contrôleur de domaine (Ajouter une nouvelle arborescence) :  

C:\>Install-ADDSDomain -NewDomainName TDI.LOCAL -ParentDomainName OFPPT.MA -DomainType TreeDomain -InstallDns  

Installer un Contrôleur de domaine en utilisant la méthode IFM  

C:\>NTDSUTIL 

C:\>Activate Instance NTDS  

C:\>IFM  

C:\>Create Sysvol Full E:  

III-Commades de Configuration des OU: 

Créer une Unité d’organisation :  

C:\>New-ADOrganizationalUnit -Name NTIC 

C:\>New-ADOrganizationalUnit -Name TRI -Path "ou=NTIC,dc=OFPPT,dc=MA"  

Afficher toutes les Unités d’organisatios: C:\>Get-ADOrganizationalUnit -Filter * | Format-Table  

Désactiver la protection contre la suppression accidentelle d’une unité d’organisation :  

C:\>Set-ADOrganizationalUnit -Identity "ou=TRI,ou=NTIC,dc=OFPPT,dc=MA" -ProtectedFromAccidentalDeletion $false  

Supprimer une Unité d’organisation :  

C:\>Remove-ADOrganizationalUnit –Identity "ou=TRI,ou=NTIC,dc=OFPPT,dc=MA" -Confirm:$false  

IV-Commades de Configuration des Utilisateurs et Ordinateurs: 

Créer un compte utilisateur :  

C:\>New-ADUser -Name TriUsr -Path "ou=TRI,ou=NTIC,dc=OFPPT,dc=MA" -AccountPassword (ConvertTo-SecureString -AsPlainText '123456' -Force) -Enabled $true  

Modifier les propriétés d’un utilisateur :   

C:\>Set-ADUser -Identity "cn=Triuser,ou=TRI,ou=NTIC,dc=OFPPT,dc=MA" -Department service -GivenName Prénom -Surname Nom -DisplayName "Prénom Nom" -UserPrincipalName "Triuser1@OFPPT.MA" -SamAccountName TriUser  

Autres propriétés :  

-GivenName : Prénom -SurName : Nom  

-DisplayName : Nom Complet -Description : Description -Office : Bureau  

-Title : Fonction-Departement : Service 

-Company : Société-EmailAddress : Adresse de messagerie   

-UserPrincipalName : Nom d'ouverture de session de l'utilisateur-SamAccountName : Nom d'ouverture de session de l'utilisateur (Antérieur à Windows 2000)  

-City :Ville-State :Province  

-Country :Pays/Région  

Supprimer un Compte Utilisateur :  

C:\> Remove-ADUser -Identity "cn=Triuser,ou=TRI,ou=NTIC,dc=OFPPT,dc=MA" 

Créer un Compte Ordinateur :  

C:\>New-ADComputer -Name Poste01 -Path "ou=TRI,ou=NTIC,dc=OFPPT,dc=MA"  

Modifier un compte Ordinateur :  

C:\>Set-ADComputer "cn=Poste01,ou=TRI,ou=NTIC,dc=OFPPT,dc=MA" -Location "Salle Info1“ 

Supprimer un compte Ordinateur :  

C:\>Remove-ADComputer "cn= Poste01,ou=TRI,ou=NTIC,dc=OFPPT,dc=MA "  

Modifier le mot de passe d’un compte utilisateur ou ordinateur :  

C:\> Set-ADAccountPassword -Identity "cn=Triuser,ou=TRI,ou=NTIC,dc=OFPPT,dc=MA" -NewPassword (ConvertTo-SecureString -AsPlainText '123456' -Force) -Reset  

Activer un Compte utilisateur ou ordinateur :  

C:\>Enable-ADAccount -Identity "cn=Triuser,ou=TRI,ou=NTIC,dc=OFPPT,dc=MA"  

Désactiver un Compte utilisateur ou ordinateur :  

C:\>Disable-ADAccount -Identity "cn=Triuser,ou=TRI,ou=NTIC,dc=OFPPT,dc=MA"  

Renommer un Objet ADDS :  

C:\>Rename-ADObject "cn=Triuser,ou=TRI,ou=NTIC,dc=OFPPT,dc=MA" -NewName "TRI3"  

Déplacer un Objet ADDS :  

C:\>Move-ADObject "cn=Triuser,ou=TRI,ou=NTIC,dc=OFPPT,dc=MA" -TargetPath "ou= NTIC,dc=OFPPT,dc=MA "  

IV-Commades de Configuration des Groupes: 

Créer un groupe de Distribution :  

C:\>New-ADGroup "TRIGroupDistribution" -GroupCategory Distribution -GroupScope Global -Path "ou=Tri,ou=NTIC,dc=OFPPT,dc=MA" 

Ou Bien: 

C:\>New-ADGroup "TRIGroupDistribution"-GroupCategory Distribution -GroupScope DomainLocal -Path "ou=TRI,ou=NTIC,dc=OFPPT,dc=MA"  

Ou Bien: 

C:\>New-ADGroup "TRIGroupDistribution"-GroupCategory Distribution -GroupScope Universal -Path "ou=TRI,ou=NTIC,dc=OFPPT,dc=MA"  

Créer un groupe de Sécurity :  

C:\>New-ADGroup "TRIGroupSecurity" -GroupCategory Security -GroupScope Global -Path "ou=TRI,ou=NTIC,dc=OFPPT,dc=MA"  

Ou Bien: 

C:\>New-ADGroup "TRIGroupSecurity"-GroupCategory Security -GroupScope DomainLocal -Path "ou=TRI,ou=NTIC,dc=OFPPT,dc=MA"  

Ou Bien:  

C:\>New-ADGroup "TRIGroupSecurity"-GroupCategory Security -GroupScope Universal -Path "ou=TRI,ou=NTIC,dc=OFPPT,dc=MA"  

Ajouter des membres à un groupe :  

C:\>Add-ADGroupMember -Identity "TRIGroupSecurity" -Members "TRiUser1","TRiUser2","cn=TriUser,ou=TRI,ou=NTIC,dc=OFPPT,dc=MA"  

Supprimer des membres à un groupe :  

C:\>Remove-ADGroupMember -Identity TRIGroupSecurity -Members "TRiUser1","TRiUser2" Confirm:$false  

 

 

V-Commades de Configuration de DNS: 

Installer le rôle DNS :  

C:\>Install-WindowsFeature DNS -IncludeManagementTools  

Créer une zone DNS principale :  

C:\>Add-DnsServerPrimaryZone -Name ofppt.ma -ZoneFile ofppt.ma.dns -DynamicUpdate NonsecureAndSecure  

Créer une zone intégrée AD :  

C:\>Add-DnsServerPrimaryZone -name ofppt.com -ReplicationScope Domain  

Créer une zone DNS inversée :  

C:\>Add-DnsServerPrimaryZone -NetworkId 172.18.0.0/16 -ZoneFile 18.172.in- addr.arpa.dns - DynamicUpdate NonsecureAndSecure  

Créer une zone secondaire :  

C:\>Add-DnsServerSecondaryZone -name tdi.com -MasterServers 172.16.0.10 -ZoneFile tdi.com.dns  

Configurer le serveur de la zone principale pour autoriser le transfert de zone :  

C:\>Set-DnsServerPrimaryZone -Name tdi.com -Notify NotifyServers -SecondaryServers 172.16 .0.21 -NotifyServers 172.16.0.21 –SecureSecondaries TransferToSecureServers  

Transférer les enregistrements depuis la zone principale :  

C:\>Start-DnsServerZoneTransfer -Name tdi.com -FullTransfer  

Intégrer une zone principale à AD :  

C:\>ConvertTo-DnsServerPrimaryZone -Name ofppt.ma -ReplicationScope Domain  -Force 0  

Désintégrer une zone d’AD :  

C:\>ConvertTo-DnsServerPrimaryZone -Name ofppt.ma -ZoneFile ofppt.ma.dns -Force  

Supprimer une Zone :  

C:\>Remove-DnsServerZone -Name tdi.com -Confirm:$false -Force  

Créer une Zone Stub :  

C:\>Add-DnsServerStubZone -name tdi.com -MasterServers 172.16.0.10 -ZoneFile adatum.com.dns  

 

Créer une redirection Conditionnelle : 

C:\> Add-DnsServerConditionalForwarderZone -Name ofppt.net -MasterServers 172.16.10.10  

Créer un enregistrement A :  

C:\>Add-DnsServerResourceRecordA -ZoneName ofppt.ma -Name lon-client1 -IPv4Address 172.18.0.50 -createPtr 

C:\>Add-DnsServerResourceRecordA -ZoneName ofppt.ma -A -Name lon-client2 -IPv4Address 172.18.0.51 -createPtr  

Créer un enregistrement AAAA :  

C:\>Add-DnsServerResourceRecordAAAA -ZoneName ofppt.ma -Name lon-client1 IPv6Address 2001::1 

 C:\>Add-DnsServerResourceRecord -ZoneName ofppt.ma -AAAA -Name lon-client2 -IPv6Address 2001::2  

Créer un enregistrement MX :  

C:\>Add-DnsServerResourceRecordMX -ZoneName ofppt.ma -name "." -MailExchange lonmail2.ofppt.ma -Preference 10 

C:\>Add-DnsServerResourceRecord -ZoneName ofppt.ma -MX -name "." -MailExchange lonmail3.ofppt.ma -Preference 10  

Créer un enregistrement CNAME (Alias)  

C:\>Add-DnsServerResourceRecordCName -ZoneName ofppt.ma -Name www -HostNameAlias lon-client.ofppt.ma 

C:\>Add-DnsServerResourceRecord -ZoneName ofppt.ma -CName -Name www -HostNameAlias lon-client.ofppt.ma 

Créer un enregistrement SRV :  

C:\>Add-DnsServerResourceRecord -Srv -ZoneName ofppt.ma -DomainName ofppt.ma -Name _sip._tcp -Priority 0 -Weight 0 -Port 5600 

Créer un enregistrement NS :  

C:\>Add-DnsServerResourceRecord -NS -ZoneName ofppt.ma -Name "." -NameServer lonsvr1.adatum.com  

 

 

 

 

VI-Commades de Configuration de DHCP: 

Installer le rôle DHCP : 

C:\>Install-WindowsFeature DHCP -IncludeManagementTools  

Autoriser le serveur DHCP dans AD :  

C:\>Add-DhcpServerInDC -DnsName lon-svr1.adatum.com -IPAddress 172.16.0.21  

Créer la délégation DHCP :  

C:\>Add-DhcpServerSecurityGroup  

Créer un étendu :  

C:\>Add-DhcpServerv4Scope -Name ofppt -StartRange 172.18.0.50 -EndRange 172.18.0.150 SubnetMask 255.255.255.0 

Ajouter une exclusion :  

C:\>Add-DhcpServerv4ExclusionRange -ScopeId 172.18.0.0 -StartRange 172.18.0.70 -EndRange 172.18.0.90  

Configurer les options de l'étendu :  

C:\>Set-DhcpServerv4OptionValue -ScopeId 172.18.0.0 -Router 172.18.0.1  

Ou Bien: 

C:\>Set-DhcpServerv4OptionValue -ScopeId 172.18.0.0 -OptionId 3 -Value 172.18.0.10  

 

PS C:\>Set-DhcpServerv4OptionValue -ScopeId 172.18.0.0 -DnsServer 172.18.0.10  

Ou Bien: 

C:\>Set-DhcpServerv4OptionValue -ScopeId 172.18.0.0 -OptionID 6 172.18.0.10  

Configurer les options de serveur :  

C:\>Set-DhcpServerv4OptionValue -ComputerName lon-svr1.adatum.com -OptionId 3 -Value 172.18.0.10  

Créer une réservation :  

C:\>Add-DhcpServerv4Reservation -ScopeId 172.18.0.0 -ClientId 00-f0-c4-55-44- 33 -IPAddress 172.18.0.60  

Configurer les options de réservation  

PS C:\>Set-DhcpServerv4OptionValue -ReservedIP 172.18.0.60 -Router 172.18.0.30  

 

 

 

 

 

 

VII-Commades de Configuration des GPO: 

Crèe une GPO :  

C:\>New-GPO -NAME “GPO01” 

Lier un GPO à un OU: 

C:\>New-GPLINK –Name “GPO01” -Target “ou=NTIC,dc=OFPPT,dc=MA"  

 

Les commondes linux 

Configuration DHCP 

Installation des packages 

Yum install dhcp 

Vérifier l'installation des packages :  

Rpm –aq ¡ grep dhcp 

Le chemain de fichier de configuration  

/etc/dhcp/dhcpd.conf 

la configuration du service DHCP 

vim /etc/dhcp/dhcpd.conf 

ddns-update-style interim; 

ddns-update on; 

subnet 192.168.1.0 netmask 255.255.255.0 {  

range192.168.1.10 192.168.1.100; 

option domain-name-servers 192.168.1.254;  

option domain-name "tri.lan"; 

option routers 192.168.1.1; 

option broadcast-address 192.168.1.255;  

default-lease-time 600; 

max-lease-time 7200;} ; 

configuration d’une reservation dhcp 

host client1 { 

hardware ethernet 08:00:27:5d:6f:02;  

fixed-address 192.168.1.25; } ; 

Redémarrer le service DHCP :  

systemctl restart dhcpd 

Configuration DNS 

Installer les packages :  

Yum install bind 

Vérifier l'installation des packages :  

Rpm –aq ¡ grep bind 

Configuration globale de service BIND :  

vim /etc/named.conf  

Declaration des zone 

Zone directe 

zone "tri.lan" IN {type master; 

file "tri.lan.zone"; 

allow-transfer { 192.168.1.253; }; 

allow-update { 192.168.1.253; }; 

notify yes;}; 

Zone inverse 

zone "1.168.192.in-addr.arpa" IN {type master; 

file "tri.lan.rev"; 

allow-transfer { 192.168.1.253; }; 

allow-update { 192.168.1.253; };  

notify yes;}; 

Configuration des fichiers des zones :  

/var/named/tri.lan.zone  

@ IN SOA Serv1.tri.lan. root.tri.lan. (  

2016 ; serial 

1D ; refresh 

1H ; retry 

1W ; expire 

3H; minimum ) ; 

@ 	IN 	NS 		Serv1.tri.lan 

Serv1  IN 	A 	 192.168.1.254 

@ 	IN	MX 	10 	mail.tri.lan. 

mail 	IN	CNAME 	Serv1.tri.lan. 

 

/var/named/tri.lan.rev 

@ IN SOA Serv1.tri.lan. root.tri.lan. (  

2016 ; serial 

1D ; refresh 

1H ; retry 

1W ; expire 

3H; minimum) ; 

@ 	 IN 	NS 		Serv1.tri.lan. 

254	 IN 	PTR 		Serv1.tri.lan. 

25 	IN 	PTR 		XP.tri.lan.  

Configuration de resolv.conf :  

vim /etc/resolv.conf  

# Generated by NetworkManager nameserver 192.168.1.254 

searchtri.lan  

Redémarrer le service DNS :  

systemctl restart bind 

Vérifier le bon fonctionnement de DNS :  

#nslookup 

Configuration NFS 

Installer les packages :  

Yum install nfs-utils 

Vérifier les packages :  

Rpm –aq ¡ grep nfs 

Créer un dossier partager :  

# mkdir /home/partage  

# chmod 777 /home/partage  

# touch /home/partage/fich  

# chmod 777 /home/partage/*  

Configuration du fichier :  

# vim /etc/exports  

/home/partage *(rw) 

Démarrer le services nfs: 

Systemctl restart nfs-server 

Montage de partage (Au niveau du client) : 

Créer un dossier de montage : 

# mkdir Bureau/montage  

# chmod 777 Bureau/montage  

Monter le partage :  

# mount -t nfs 192.168.1.254:/home/partage Bureau/montage  

Configuration SAMBA 

Installation des packages :  

Yum install samba 

Vérification des packages :  

Rpm –aq ¡ grep smb 

Configuration de SAMBA :  

# vim /etc/samba/smb.conf  

[partage] 

comment = Shared Folder 

path = /home/partage 

public = no 

writable = yes 

valid users = samba-1 

browseable = yes  

create mask = 0660 

directory mask = 0771 

Créer un nouvel utilisateur :  

# useradd samba-1  

# smbpasswd -a samba-1  

New SMB password: password 

Créer le dossier partager : 

# mkdir /home/partage  

# chmod 777 /home/partage  

Redémarrer le service SAMBA : 

Systemctl restart smb 

Configuration FTP 

Installer les packages :  

Yum install vsftp 

Vérifier les packages :  

Rpm –aq ¡ grep vsftp 

Configuration de fichier :  

/etc/vsftpd.conf 

Listen_port= 2121 : chenger le port d’ecute 

anonymous_enable=YES: autorise l’acces des anonymes. 

Anon_root=/var/ftp/pub :autorise l’acces anonymes dans fichier 

local_enable=YES: Permet aux utilisateurs locaux de se connecter. 

 

write_enable=YES: Autorise l'écriture de fichiers par les utilisateurs. 

local_umask=022: Définit les permissions par défaut  

Local_max_rate=1000000 : limite la bande bassent Mo/s 

connect_from_port_20=YES: Utilise le port 20  

chroot_local_user=YES: Restreint les utilisateurs locaux à leur répertoire personnel. 

userlist_enable=YES: Active l'utilisation du fichier user_list 

listen=NO: Désactive l'écoute sur IPv4.  

local_umask=022 : Définit les permissions par défaut  

Créer un nouvel utilisateur :  

# useradd user-ftp  

# passwd user-ftp  

Modifier les dossiers partager : 

# chmod 777 /home/user-ftp/  

# touch /home/user-ftp/Fich  

# chmod 777 /home/user-ftp/*  

Modifier SELinux : 

# setsebool ftp_home_dir on  

Redémarrer le service FTP : 

Systemctl restart vsftpd 

Configuration SSH 

Installation de packages :  

Yum install openssh 

Vérification des packages :  

Rpm –aq ¡ grep ssh 

Configuration de fichier :  

# vim /etc/ssh/sshd_config  

Port 22 

ListenAddress 192.168.1.254  

Protocol 2 

PermitRootLogin yes  

Redémarrer le service SSH :  

Systemctl restart sshd 

 

 

Configuration http (Apache) 

Installer les packages : 

Yum install httpd 

Vérifier les packages :  

Rpm –aq ¡ grep http 

exemple d'un fochier HTML :  

# vim /var/www/html/index.html  

<html> 

<center><font size='+2' color='blue'>HTTP sous Fedora</font></center> 

<hr>Welcome to HTTP Server. Opening doore to new opprtunites. Mind Wide Open. 

<p>Quik links: 

<br><a href='helloworld.html'>A small page</a> 

<br><a href='copyrights.html'>Copyroghts</a> 

<br><a href='image.html'>Image page</a> 

<br><a href='cscoptlogo177x111.html'>Image</a> 

</html> 

Redémarrer le service HTTP :  

Systemctl restart httpd 

Configuration TELNET 

Installer les packages : 

Yum install telnet 

Vérifier les packages :  

Rpm –aq ¡ grep telnet 

Configuration de fichier :  

# vim /etc/xinetd.d/telnet  

service telnet{ 

flags = REUSE  

socket_type = stream  

wait = no  

user = root 

server = /usr/sbin/in.telnetd  

log_on_failure += USERID  

disable = no 

port = 23}  

Redémarrer le service telnet :  

Systemctl restart xinetd 

 

 

  Les commonde linux de base 

 

Configuration NETWORKS 

Vim /etc/network/interfaces 

Dynamique DHCP 

Auto eth0 

Iface eth0 inet DHCP 

Static adresse  

auto eth0 

iface eth0 inet static 

    address 192.168.1.10 

netmask 255.255.255.0 

    gateway 192.168.1.1 

    dns-nameservers 8.8.8.8 8.8.4.4 

configuration par commonde 

# nmcli connection modify eth0 ipv4.addresses 192.168.1.10/24 ipv4.getway 192.168.1.1 

ipv4.dns 192.168.1.254 … 

Redémarrer le service network : 

#Systemctl restart network 

Arite  l’interfacenetwork 

Nmcli connection up/down eth0 

 

Configuration HOSTNAME 

configuration Par le fichier 

vim /etc/hostname 

computer1 

configuration par commonde  

hostnamectl set-hostname computer1 

commonde de base  

cree un dossier  

#mkdir dossier1 

cree un utilisateur 

#useradd user1 

cree un group 

#groupadd group1 

ajouter utilisateur a un group 

#usermod -aG group1user1 

ajouter password a un utilisateur 

#passwd user1 

changer les droit d’un fichier 

#chmod {les droit} {le chemain de fichier} 

 

mountage d’un fichier 

#mount {chemain de fichier} 

 {point de mountge } 

change la proprietaire et le group 

#chown {proprietair} : {group} {chemain de fichier} 

la securite linux 

autorise un service au firewall 

#firewall-cmd --permanent --add –service={nom service} 

autorise un service sous selinux 

setsebool –p {nom service} 

 

 

 

 