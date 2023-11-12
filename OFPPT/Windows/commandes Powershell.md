# Atelier : Administration à l’aide du PowerShell

```
Administration Réseau Sous Windows
```
Pour réaliser cet Atelier pratique Installer Windows Server ‘’Installation minimal’’ sur une machine
virtuelle Hyper-V ou VMware. Puis créer un Point de contrôle pour répéter l’Atelier une autre fois
sans réinstaller Windows server

# Exercice N° 1 : Configuration de base

## 1. Redémarrer le serveur

PS C:\> Restart-Computer

## 2. Arrêter le serveur

## PS C:\> Stop-Computer

## 3. Renommer l’ordinateur

PS C:\> Rename-Computer -NewName "TRI-DC" - Restart

## 4. Configurer l’adresse IP

PS C:\> get-NetIPInterface

PS C:\> new-NetIPAddress –InterfaceIndex 12 –IPAdress 172.16.0.200 –PrefixLength 24 –
DefaultGateway 172.16.0.

PS C:\> Set-DNSClientServerAddresses – InterfaceIndex 12 –ServerAddresses
172.16.0.10,172.16.0.

## 5. Joindre le serveur au Domaine

PS C:\> add-Computer –DomainName Adatum.com –Restart

## 1. Convertir une installation minimale en une installation complète

PS C:\> get-WindowsFeature -Name *GUI* | Install-WindowsFeature -IncludeAllSubFeature -
IncludeManagementTools -Restart

## 1. Convertir une installation complète en une installation minimale

PS C:\> get-WindowsFeature -Name *GUI* | Remove-WindowsFeature -Restart

Ou :

PS C:\> get-WindowsFeature -Name *GUI* | Uninstall-WindowsFeature -Restart

# Exercice N° 2 : Installer et Configurer le Contrôleur de Domaine

## 1. Installer le rôle ADDS

PS C:\> Install-WindowsFeature -Name AD-Domain-Services -IncludeAllSubFeature -
IncludeManagementTools

## 2. Promouvoir le serveur en Contrôleur de domaine (Ajouter un contrôleur de

## domaine à un domaine existant)


PS C:\> Install-ADDSDomainController -DomainName Adatum.com -InstallDns

## 3. Promouvoir le serveur en Contrôleur de domaine (Ajouter un nouveau domaine

## enfant)

PS C:\> Install-ADDSDomain -NewDomainName khenifra.adatum.com -ParentDomainName
adatum.com - DomainType ChildDomain -InstallDns

## 4. Promouvoir le serveur en Contrôleur de domaine (Ajouter une nouvelle

## arborescence)

PS C:\> Install-ADDSDomain -NewDomainName contoso.com -ParentDomainName adatum.com -
DomainType TreeDomain -InstallDns

## 5. Promouvoir le serveur en Contrôleur de domaine (Ajouter une nouvelle Forêt)

PS C:\> Install-ADDSForest -DomainName adatum.com -InstallDns

## 6. Inscrire la console de schéma dans le registre

NB : par défaut la console schéma n’est pas disponible lors de l’installation d’active directory

PS C:\> regsvr32 schmmgmt.dll

## 1. Désinscrire la console de schéma du registre

PS C:\> regsvr32 - u schmmgmt.dll

# Exercice N° 3 : Gestion des Objets ADDS

## 1. Créer une Unité Organisationnelle

PS C:\> New-ADOrganizationalUnit NTIC
PS C:\> New-ADOrganizationalUnit -Name TRI -Path "ou=ntic,dc=adatum,dc=com"
PS C:\> New-ADOrganizationalUnit -Name MIR - Path "ou=ntic,dc=adatum,dc=com"
PS C:\> New-ADOrganizationalUnit -Name TMSIR - Path "ou=ntic,dc=adatum,dc=com"

## 2. Afficher toutes les Unités Organisationnelle

PS C:\> Get-ADOrganizationalUnit -Filter * | Format-Table

## 3. Afficher les sous unités organisationnelle d’une Unité organisationnelle

PS C:\> Get-ADOrganizationalUnit -Filter * -SearchBase "ou=ntic,dc=adatum,dc=com" |Format-
Table

## 4. Désactiver la protection contre la suppression accidentelle d’une unité

## organisationnelle

NB : Pa défaut les Unités Organisationnelle sont protégé contre la suppression

PS C:\> Set-ADOrganizationalUnit -Identity "ou=MIR,ou=ntic,dc=adatum,dc=com" -
ProtectedFromAccidentalDeletion $false

## 5. Supprimer une unité organisationnelle

PS C:\> remove-adorganizationalunit -Identity "ou=mir,ou=ntic,dc=adatum,dc=com" -Confirm:$false

## 6. Créer un compte utilisateur


NB : un compte créé sans mot de passe sera désactivé

PS C:\> New-ADUser - Name TriUser1 -Path "ou=tri,ou=ntic,dc=adatum,dc=com"
PS C:\> New-ADUser -Name TriUser2 -Path "ou=tri,ou=ntic,dc=adatum,dc=com" -AccountPassword
(ConvertTo-SecureString - AsPlainText 'Pa$$w0rd' -Force)
PS C:\> New-ADUser -Name TriUser3 -Path "ou=tri,ou=ntic,dc=adatum,dc=com" -AccountPassword
(ConvertTo-SecureString -AsPlainTex t 'Pa$$w0rd' -force) -Enabled $true

## 7. Modifier les propriétés d’un utilisateur

PS C:\> Set-ADUser -Identity "cn=triuser1,ou=tri,ou=ntic,dc=adatum,dc=com" - Department service -
GivenName Prenom -Surname Nom -DisplayName "Prenom Nom" - UserPrincipalName
"triuser1@adatum.com" - SamAccountName TriUser

Autres propriétés :

- GivenName : Prénom
- SurName : Nom
- DisplayName : Nom Complet
- Description : Description
- Office : Bureau
- Title : Fonction
- Departement : Service
- Company : Société
- EmailAddress : Adresse de messagerie
    - UserPrincipalName : Nom d'ouverture de
    session de l'utilisateur
    - SamAccountName : Nom d'ourture de
    session de l'utilisateur (Antérieur à Windows
    2000)
    - City : Ville
    - State : Province
    - Country : Pays/Région

## 8. Supprimer un Compte Utilisateur

PS C:\> Remove-ADUser -Identity "cn=triuser1,ou=tri,ou=ntic,dc=adatum,dc=com"

## 9. Reconfigurer le conteneur de l'ordinateur par défaut

NB : Par défaut les ordinateurs qui joignent le domaine sont mis dans le dossier ‘’Computers’’

PS C:\> redircmp.exe "ou=NewComputers,dc=Adatum,dc=com"

## 10. Reconfigurer le conteneur de l’utilisateur par défaut

NB : Par défaut les utilisateurs créés avec commandes sans définir le paramètre ‘’-Path’’ sont mis dans
le dossier ‘’Users’’

PS C:\> redirusr.exe "ou=NewUsers,dc=Adatum,dc=com"

## 11. Créer un compte Ordinateur

PS C:\> New-ADComputer - Name Poste01 -Path "ou=TRI,ou=NTIC,dc=Adatum,dc=com"

## 12. Modifier un compte Ordinateur

PS C:\> Set-ADComputer "cn=Poste01,ou=TRI,ou=NTIC,dc=Adatum,dc=com" - Location "Salle
Info1"

## 13. Supprimer un compte Ordinateur

```powershell
PS C:\> Remove-ADComputer "cn= Poste01,ou=tri,ou=ntic,dc=adatum,dc=com"
```

## 14. Modifier le mot de passe d’un compte utilisateur ou ordinateur

```powershell
PS C:\> Set-ADAccountPassword -Identity "cn=triuser1,ou=tri,ou=ntic,dc=adatum,dc=com" -
NewPassword (ConvertTo-SecureString - AsPlainText "Pa$$w0rd" -Force) - Reset

PS C:\> Set-ADAccountPassword -Identity "cn=triuser1,ou=tri,ou=ntic,dc=adatum,dc=com" -
NewPassword (read-host "donnez le PW" - AsSecureString) - Reset
```
## 15. Activer un Compte utilisateur ou ordinateur

PS C:\> Enable-ADAccount -Identity "cn=triuser1,ou=tri,ou=ntic,dc=adatum,dc=com"

## 16. Désactiver un Compte utilisateur ou ordinateur

PS C:\> Disable-ADAccount -Identity "cn=triuser1,ou=tri,ou=ntic,dc=adatum,dc=com"

## 17. Créer un groupe de distribution

PS C:\> New-ADGroup TRIGroupDistribution -GroupCategory Distribution -GroupScope Global -
Path "ou=tri,ou=ntic,dc=adatum,dc=com"

PS C:\> New-ADGroup TRIGroupDistribution -GroupCategory Distribution - GroupScope
DomainLocal -Path "ou=tri,ou=ntic,dc=adatum,dc=com"

PS C:\> New-ADGroup TRIGroupDistribution -GroupCategory Distribution - GroupScope Universal

- Path "ou=tri,ou=ntic,dc=adatum,dc=com"

## 18. Créer un groupe de security

NB : la propriété -GroupCategory a la valeur par défaut Security, alors il n’est pas nécessaire de la
préciser en cas de groupe de sécurité

PS C:\> New-ADGroup TRIGroupSecurity - GroupCategory Security - GroupScope Global - Path
"ou=tri,ou=ntic,dc=adatum,dc=com"

PS C:\> New-ADGroup TRIGroupSecurity -GroupScope Global -Path
"ou=tri,ou=ntic,dc=adatum,dc=com"

PS C:\> New-ADGroup TRIGroupSecurity -GroupScope DomainLocal -Path
"ou=tri,ou=ntic,dc=adatum,dc=com"

PS C:\> New-ADGroup TRIGroupSecurity -GroupScope Universal -Path
"ou=tri,ou=ntic,dc=adatum,dc=com"

## 19. Ajouter des membres à un groupe

PS C:\> Add-ADGroupMember -Identity TRIGroupSecurity -Members
"TRiUser1","TRiUser2","cn=TriUser3,ou=TRI,ou=NTIC,dc=adatum,dc=com"

## 20. Supprimer des membres à un groupe

PS C:\> Remove-ADGroupMember -Identity TRIGroupSecurity -Members "TRiUser1","TRiUser2" -
Confirm:$false

## 21. Renommer un Objet ADDS

PS C:\> Rename-ADObject "cn=TriUser3,ou=TRI,ou=NTIC,dc=adatum,dc=com" -newName "TRI3"

## 22. Déplacer un Objet ADDS

Move-ADObject "cn=TRI3,ou=TRI,ou=NTIC,dc=adatum,dc=com" -TargetPath "ou=
NTIC,dc=adatum,dc=com "


# Exercice N° 4 : Gestion de Serveur DNS

## 1. Installer le rôle DNS

PS C:\> Install-WindowsFeature DNS - IncludeManagementTools

## 2. Créer une zone DNS principale

PS C:\> Add-DnsServerPrimaryZone -Name ofppt.ma -ZoneFile ofppt.ma.dns -DynamicUpdate
NonsecureAndSecure

## 3. Créer une zone intégrée AD

PS C:\> Add-DnsServerPrimaryZone -name ofppt.com - ReplicationScope Domain

## 4. Créer une zone DNS inversée :

PS C:\> Add-DnsServerPrimaryZone -NetworkId 172.18.0.0/16 -ZoneFile 18.172.in-addr.arpa.dns -
DynamicUpdate NonsecureAndSecure

## 5. Créer une zone secondaire

PS C:\> Add-DnsServerSecondaryZone -name adatum.com -MasterServers 172.16.0.10 -ZoneFile
adatum.com.dns

## 6. Configurer le serveur de la zone principale pour autoriser le transfert de zone

PS C:\> Set-DnsServerPrimaryZone -Name adatum.com -Notify NotifyServers -SecondaryServers
172.16 .0.21 -NotifyServers 172.16.0.21 -SecureSecondaries TransferToSecureServers

## 7. Transférer les enregistrements depuis la zone principale

PS C:\> Start-DnsServerZoneTransfer -Name adatum.com -FullTransfer

NB : le paramètre -FullTransfer pour le transfère Complet (AXFR), sans ce paramètre ça sera un
transfère incrémental (IXFR)

## 8. Intégrer une zone principale à AD

PS C:\> ConvertTo-DnsServerPrimaryZone -Name ofppt.ma - ReplicationScope Domain -Force

## 9. Désintégrer une zone d’AD

PS C:\> ConvertTo-DnsServerPrimaryZone -Name ofppt.ma -ZoneFile ofppt.ma.dns -Force

## 10. Supprimer une Zone

PS C:\> Remove-DnsServerZone -Name adatum.com -Confirm:$false -Force

## 11. Créer une Zone Stub

PS C:\> Add-DnsServerStubZone -name adatum.com -MasterServers 172.16.0.10 -ZoneFile
adatum.com.dns

## 12. Créer une redirection Conditionnelle

PS C:\> Add-DnsServerConditionalForwarderZone -Name ofppt.net -MasterServers 1 7 2.1 6 .1 0.

## 13. Créer un enregistrement A


PS C:\> Add-DnsServerResourceRecordA -ZoneName ofppt.ma -Name lon-client1 -IPv4Address
172.18.0.50 -createPtr
PS C:\> Add-DnsServerResourceRecord -ZoneName ofppt.ma -A -Name lon-client2 -IPv4Address
172.18.0.51 -createPtr

## 14. Créer un enregistrement AAAA

PS C:\> Add-DnsServerResourceRecordAAAA -ZoneName ofppt.ma -Name lon-client1 -
IPv6Address 2001::
PS C:\> Add-DnsServerResourceRecord -ZoneName ofppt.ma -AAAA -Name lon-client2 -
IPv6Address 2001::

## 15. Créer un enregistrement MX

PS C:\> Add-DnsServerResourceRecordMX -ZoneName ofppt.ma -name "." -MailExchange lon-
mail2.ofppt.ma -Preference 10
PS C:\> Add-DnsServerResourceRecord -ZoneName ofppt.ma -MX -name "." -MailExchange lon-
mail3.ofppt.ma -Preference 10

## 16. Créer un enregistrement CNAME (Alias)

PS C:\> Add-DnsServerResourceRecordCName -ZoneName ofppt.ma -Name www -HostNameAlias
lon-client.ofppt.ma
PS C:\> Add-DnsServerResourceRecord -ZoneName ofppt.ma -CName -Name www -
HostNameAlias lon-client.ofppt.m

## 17. Créer un enregistrement SRV

PS C:\> Add-DnsServerResourceRecord -Srv -ZoneName ofppt.ma -DomainName ofppt.ma -Name
_sip._tcp -Priority 0 -Weight 0 -Port 5600

## 18. Créer un enregistrement NS

PS C:\> Add-DnsServerResourceRecord -NS -ZoneName ofppt.ma -Name "." -NameServer lon-
svr1.adatum.com

# Exercice N° 5 : Gestion de Serveur DHCP

## 1. Installer le rôle DHCP

PS C:\> Install-WindowsFeature DHCP - IncludeManagementTools

## 2. Autoriser le serveur DHCP dans AD

PS C:\> Add-DhcpServerInDC -DnsName lon-svr1.adatum.com -IPAddress 172.16.0.

## 3. Créer la délégation DHCP

PS C:\> Add-DhcpServerSecurityGroup

## 4. Créer un étendu

PS C:\> Add-DhcpServerv4Scope -Name ofppt -StartRange 172.18.0.50 -EndRange 172.18.0.150 -
SubnetMask 255.255.255.

## 5. Ajouter une exclusion


PS C:\> Add-DhcpServerv4ExclusionRange -ScopeId 172.18.0.0 -StartRange 172.18.0.70 -EndRange
172.18.0.

## 6. Configurer les options de l'étendu

PS C:\> Set-DhcpServerv4OptionValue -ScopeId 172.18.0.0 -Router 172.18.0.
PS C:\> Set-DhcpServerv4OptionValue -ScopeId 172.18.0.0 -OptionId 3 -Value 172.18.0.
PS C:\> Set-DhcpServerv4OptionValue -ScopeId 172.18.0.0 -DnsServer 172.18.0.
PS C:\> Set-DhcpServerv4OptionValue -ScopeId 172.18.0.0 -OptionId 3 -Value 172.18.0.

## 7. Configurer les options de serveur

PS C:\> Set-DhcpServerv4OptionValue -ComputerName lon-svr1.adatum.com -OptionId 3 -Value
172.18.0.

## 8. Créer une réservation

PS C:\> Add-DhcpServerv4Reservation -ScopeId 172.18.0.0 -ClientId 00-f0-c4- 55 - 44 - 33 - IPAddress
172.18.0.

## 9. Configurer les options de réservation

PS C:\> Set-DhcpServerv4OptionValue -ReservedIP 172.18.0.60 -Router 172.18.0.

# EFF #todo

42- `New-VM -Name "Server-DHCP" -MemoryStartupBytes 8GB -NewVHDPath "C:\Servers\VMs\Server-DHCP.vhdx" -NewVHDSizeBytes 100GB`
43- `install-addsdomain -NewDomainName "maroc-network.com" - ParentDomainName "maroc-info.com" -DomainType TreeDomain`
44- `Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools -restart`
45- `New-ADOrganizationalUnit -Name "GestionUsers" -Path "DC=maroc-info,DC=com"`
46- `new-AdGroup -name "GestionAdmin" -Path "ou=GestionUsers,dc=maroc-info,dc=com" -GroupCategory Distribution`
47- `New-ADUser -SamAccountName "e.employ1" -UserPrincipalName "employ1@Maroc-Network.com" -Name "employ1" -GivenName "employ1" -Surname "User" -Enabled $true -Path "OU=GestionUsers,DC=Maroc-Network,DC=com"`
48- `Rename-Computer -NewName "Server-DC" -Restart`
49- `New-NetIPAddress -InterfaceAlias Giga-Ethernet -IPAddress 10.10.1.9 -PrefixLength 24 -DefaultGateway 10.10.1.1` 
50- `Add-Computer -DomainName "Maroc-network.com"`
51- `Add-DhcpServerv4Scope -Name "Vlan-Gestion" -StartRange 10.10.1.10 -EndRange 10.10.1.100 -SubnetMask 255.255.255.0 -Description "Vlan-Gestion"`
