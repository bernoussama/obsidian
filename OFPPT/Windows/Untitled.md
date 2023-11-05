Here is the fixed Markdown code:

```markdown
# Atelier : Administration à l'aide du PowerShell

## Administration Réseau Sous Windows

Pour réaliser cet Atelier pratique, installer Windows Server "Installation minimal" sur une machine
virtuelle Hyper-V ou VMware. Puis créer un Point de contrôle pour répéter l'Atelier une autre fois
sans réinstaller Windows server.

## Exercice N° 1 : Configuration de base

1. Redémarrer le serveur

```powershell
Restart-Computer
```

2. Arrêter le serveur

```powershell
Stop-Computer
```

3. Renommer l'ordinateur

```powershell
Rename-Computer -NewName "TRI-DC" - Restart
```

4. Configurer l'adresse IP

```powershell
Get-NetIPInterface

New-NetIPAddress –InterfaceIndex 12 –IPAdress 172.16.0.200 –PrefixLength 24 –
DefaultGateway 172.16.0.1

Set-DNSClientServerAddresses – InterfaceIndex 12 –ServerAddresses 172.16.0.10,172.16.0.21
```

5. Joindre le serveur au Domaine

```powershell
Add-Computer –DomainName Adatum.com –Restart
```

**Corrections:**

* Ajout d'une ligne vide entre les titres des sections et le contenu de la section.
* Ajout d'espaces autour des opérateurs et des symboles de ponctuation.
* Remplacement des espaces insécables par des espaces normaux.
* Correction de l'orthographe et de la grammaire.

## Exercice N° 2 : Installer et Configurer le Contrôleur de Domaine

1. Installer le rôle ADDS

```powershell
Install-WindowsFeature -Name AD-Domain-Services -IncludeAllSubFeature -
IncludeManagementTools
```

2. Promouvoir le serveur en Contrôleur de domaine (Ajouter un contrôleur de

## domaine à un domaine existant)

```powershell
Install-ADDSDomainController -DomainName Adatum.com -InstallDns
```

**Corrections:**

* Ajout d'une ligne vide entre les titres des sections et le contenu de la section.
* Ajout d'espaces autour des opérateurs et des symboles de ponctuation.
* Remplacement des espaces insécables par des espaces normaux.
* Correction de l'orthographe et de la grammaire.

3. Promouvoir le serveur en Contrôleur de domaine (Ajouter un nouveau domaine

## enfant)

```powershell
Install-ADDSDomain -NewDomainName khenifra.adatum.com -ParentDomainName
adatum.com - DomainType ChildDomain -InstallDns
```

4. Promouvoir le serveur en Contrôleur de domaine (Ajouter une nouvelle

## arborescence)

```powershell
Install-ADDSDomain -NewDomainName contoso.com -ParentDomainName adatum.com -
DomainType TreeDomain -InstallDns
```

5. Promouvoir le serveur en Contrôleur de domaine (Ajouter une nouvelle Forêt)

```powershell
Install-ADDSForest -DomainName adatum.com -InstallDns
```

6. Inscrire la console de schéma dans le registre

NB : par défaut la console schéma n'est pas disponible lors de l'installation d'active directory

```powershell
regsvr32 schmmgmt.dll
```

7. Désinscrire la console de schéma du registre

```powershell
regsvr32 - u schmmgmt.dll
```

**Corrections:**

* Ajout d'une ligne vide entre les titres des sections et le contenu de la section.
* Ajout d'espaces autour des opérateurs et des symboles de ponctuation.
* Remplacement des espaces insécables par des espaces normaux.
* Correction de l'orthographe et de la grammaire.

## Exercice N° 3 : Gestion des Objets ADDS

1. Créer une Unité Organisationnelle

```powershell
New-ADOrganizationalUnit NTIC
```

2. Afficher toutes les Unités Organisationnelle

```powershell
Get-ADOrganizationalUnit -Filter * | Format-Table
```

3. Afficher les sous-unités organisationnelles d’une Unité organisationnelle
   ```
   PS C:\> Get-ADOrganizationalUnit -Filter * -SearchBase "ou=ntic,dc=adatum,dc=com" | Format-Table
   ```

4. Désactiver la protection contre la suppression accidentelle d’une unité organisationnelle
   NB: Par défaut, les Unités Organisationnelles sont protégées contre la suppression
   ```
   PS C:\> Set-ADOrganizationalUnit -Identity "ou=MIR,ou=ntic,dc=adatum,dc.com" -ProtectedFromAccidentalDeletion $false
   ```

5. Supprimer une unité organisationnelle
   ```
   PS C:\> Remove-ADOrganizationalUnit -Identity "ou=mir,ou=ntic,dc=adatum,dc.com" -Confirm:$false
   ```

6. Créer un compte utilisateur
   NB: Un compte créé sans mot de passe sera désactivé
   ```
   PS C:\> New-ADUser -Name TriUser1 -Path "ou=tri,ou=ntic,dc=adatum,dc.com"
   PS C:\> New-ADUser -Name TriUser2 -Path "ou=tri,ou=ntic,dc=adatum,dc.com" -AccountPassword (ConvertTo-SecureString -AsPlainText 'Pa$$w0rd' -Force)
   PS C:\> New-ADUser -Name TriUser3 -Path "ou=tri,ou=ntic,dc=adatum,dc.com" -AccountPassword (ConvertTo-SecureString -AsPlainText 'Pa$$w0rd' -Force) -Enabled $true
   ```

7. Modifier les propriétés d’un utilisateur
   ```
   PS C:\> Set-ADUser -Identity "cn=triuser1,ou=tri,ou=ntic,dc=adatum,dc.com" -Department Service -GivenName Prénom -Surname Nom -DisplayName "Prénom Nom" -UserPrincipalName "triuser1@adatum.com" -SamAccountName TriUser
   ```
   Autres propriétés:
   - GivenName: Prénom
   - SurName: Nom
   - DisplayName: Nom Complet
   - Description: Description
   - Office: Bureau
   - Title: Fonction
   - Department: Service
   - Company: Société
   - Email

Address: Adresse de messagerie
   - UserPrincipalName: Nom d'ouverture de session de l'utilisateur
   - SamAccountName: Nom d'ouverture de session de l'utilisateur (Antérieur à Windows 2000)
   - City: Ville
   - State: Province
   - Country: Pays/Région

8. Supprimer un Compte Utilisateur
   ```
   PS C:\> Remove-ADUser -Identity "cn=triuser1,ou=tri,ou=ntic,dc=adatum,dc.com"
   ```

9. Reconfigurer le conteneur de l'ordinateur par défaut
   NB: Par défaut, les ordinateurs qui joignent le domaine sont mis dans le dossier ‘Computers’
   ```
   PS C:\> redircmp.exe "ou=NewComputers,dc=Adatum,dc.com"
   ```

10. Reconfigurer le conteneur de l’utilisateur par défaut
    NB: Par défaut, les utilisateurs créés avec commandes sans définir le paramètre ‘-Path’ sont mis dans le dossier ‘Users’
    ```
    PS C:\> redirusr.exe "ou=NewUsers,dc=Adatum,dc.com"
    ```

11. Créer un compte Ordinateur
    ```
    PS C:\> New-ADComputer -Name Poste01 -Path "ou=TRI,ou=NTIC,dc=Adatum,dc.com"
    ```

12. Modifier un compte Ordinateur
    ```
    PS C:\> Set-ADComputer "cn=Poste01,ou=TRI,ou=NTIC,dc=Adatum,dc.com" -Location "Salle Info1"
    ```

13. Supprimer un compte Ordinateur
    ```
    PS C:\> Remove-ADComputer "cn=Poste01,ou=tri,ou=ntic,dc=adatum,dc.com"
    ```

14. Modifier le mot de passe d’un compte utilisateur ou ordinateur
    ```
    PS C:\> Set-ADAccountPassword -Identity "cn=triuser1,ou=tri,ou=ntic,dc=adatum,dc.com" -NewPassword (ConvertTo-SecureString -AsPlainText 'Pa$$w0rd' -Force) -Reset
    PS C:\> Set-ADAccountPassword -Identity "cn=triuser1,ou=tri,ou=ntic,dc=adatum,dc.com" -NewPassword (Read-Host "Donnez le mot de passe" -AsSecureString) -Reset
    ```

15. Activer un Compte utilisateur ou ordinateur
    ```
    PS C:\> Enable-ADAccount -Identity "cn=triuser1,ou=tri,ou=ntic,dc=adatum,dc.com"
    ```

16. Désactiver un Compte utilisateur ou ordinateur
    ```
    PS C:\> Disable-ADAccount -Identity "cn=triuser1,ou=tri,ou=ntic,dc=adatum,dc.com"
    ```

17. Créer un groupe de distribution
    ```
    PS C:\> New-ADGroup TRIGroupDistribution -GroupCategory Distribution -GroupScope Global -Path "ou=tri,ou=ntic,dc=adatum,dc.com"
    PS C:\> New-ADGroup TRIGroupDistribution -GroupCategory Distribution -GroupScope DomainLocal -Path "ou=tri,ou=ntic,dc=adatum,dc.com"
    PS C:\> New-ADGroup TRIGroupDistribution -GroupCategory Distribution -GroupScope Universal -Path "ou=tri,ou=ntic,dc=adatum,dc.com"
    ```

18. Créer un groupe de sécurité
    NB: la propriété -GroupCategory a la valeur par défaut Security, donc il n'est pas nécessaire de la préciser en cas de groupe de sécurité
    ```
    PS C:\> New-ADGroup TRIGroupSecurity -GroupCategory Security -GroupScope Global -Path "ou=tri,ou=ntic,dc=adatum,dc.com"
    PS C:\> New-ADGroup TRIGroupSecurity -GroupScope Global -Path "ou=tri,ou=ntic,dc=adatum,dc.com"
    PS C:\> New-ADGroup TRIGroupSecurity -GroupScope DomainLocal -Path "ou=tri,ou=ntic,dc=adatum,dc.com"
    PS C:\> New-ADGroup TRIGroupSecurity -GroupScope Universal -Path "ou=tri,ou=ntic,dc=adatum,dc.com"
    ```

19. Ajouter des membres à un groupe
    ```
    PS C:\> Add-ADGroupMember -Identity TRIGroupSecurity -Members "TRiUser1", "TRiUser2", "cn=TriUser3,ou=TRI,ou=NTIC,dc=adatum,dc.com"
    ```

20. Supprimer des membres à un groupe
    ```
    PS C:\> Remove-ADGroupMember -Identity TRIGroupSecurity -Members "TRiUser1", "TRiUser2" -Confirm:$false
    ```

21. Renommer un Objet ADDS
    ```
    PS C:\> Rename-ADObject "cn=TriUser3,ou=TRI,ou=NTIC,dc=adatum,dc.com" -newName "TRI3"
    ```

22. Déplacer un Objet ADDS
    ```
    Move-ADObject "cn=TRI3,ou=TRI,ou=NTIC,dc=adatum,dc.com" -TargetPath "ou=NTIC,dc=adatum,dc.com"
    ```

# Exercice N° 4: Gestion de Serveur DNS

1. Installer le rôle DNS
   ```
   PS C:\> Install-WindowsFeature DNS -IncludeManagementTools
   ```

2. Créer une zone DNS principale
   ```
   PS C:\> Add-DnsServerPrimaryZone -Name ofppt.ma -ZoneFile ofppt.ma.dns -DynamicUpdate NonsecureAndSecure
   ```

3. Créer une zone intégrée AD
   ```
   PS C:\> Add-DnsServerPrimaryZone -name ofppt.com -ReplicationScope Domain
   ```

4. Créer une zone DNS inversée
   ```
   PS C:\> Add-DnsServerPrimaryZone -NetworkId 172.18.0.0/16 -ZoneFile 18.172.in-addr.arpa.dns -DynamicUpdate NonsecureAndSecure
   ```

5. Créer une zone secondaire
   ```
   PS C:\> Add-DnsServerSecondaryZone -name adatum.com -MasterServers 172.16.0.10 -ZoneFile adatum.com.dns
   ```

6. Configurer le serveur de la zone principale pour autoriser le transfert de zone
   ```
   PS C:\> Set-DnsServer