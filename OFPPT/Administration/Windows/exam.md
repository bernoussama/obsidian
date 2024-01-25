Une entreprise de taille moyenne utilise un réseau Windows Server 2016 pour gérer ses ressources informatiques. Le réseau est composé d'un seul domaine « MarocArt.ma » avec un contrôleur de domaine (DC) principal et deux DC supplémentaires pour la redondance et la tolérance aux pannes. Les serveurs contrôleurs de domaine sont aussi des serveurs DNS.

Le serveur SRV1 est un serveur exécutant Hyper-V.

1. Donner la commande PowerShell à utiliser pour installer le service d’annuaire ADDS sur le premier contrôleur de domaine Server1.
2. Donner la commande PowerShell à exécuter pour promouvoir le serveur Server1 en contrôleur du domaine « MarocArt.ma », en installant le service DNS.
3. Donner les commandes PowerShell à exécuter pour créer l’unité d’organisation « USComputers » représentée dans l’image ci-dessous en activant la protection contre la suppression accidentelle.

1. Donner la commande PowerShell à exécuter pour créer un compte utilisateur pour MOUNIR dans l’unité d’organisation « USousTraitance » avec les informations suivantes :

|   |   |   |   |   |   |
|---|---|---|---|---|---|
|**Nom**|**Prénom**|**UPN**|**Date d’expiration**|**L’utilisateur doit changer le mot de passe à l’ouverture de session**|**L’utilisateur ne peut pas changer de mot de passe**|
|NEJJAR|MOUNIR|m.nejjar@MarocArt.ma|30/06/2023|Oui|Oui|

1. Donner la commande PowerShell à exécuter pour déplacer les comptes utilisateurs de l’unité « USousTraitance » vers l’unité « USUsers »
2. Donner la commande DOS à exécuter pour supprimer tous les comptes utilisateurs, de l’unité d’organisation « USUsers », qui ont expiré.
3. Donner la commande PowerShell à utiliser pour créer le groupe de sécurité universel « GUImpression » dans l’unité d’organisation « USUsers ».

Soit l’image ci-dessous, qui représente les GPO créés et appliqués sur les objets de l’entreprise :

- GPO1-AUTORISER_ACCES_NET : Autorise l’accès réseau aux utilisateurs.
- GPO2-INTERDIRE_PANNEAU_DE_CONFIGURATION : Interdit l’accès au panneau de configuration.
- GPO3-AUTORISER_PANNEAU_DE_CONFIGURATION : Autorise l’accès au panneau de configuration.

1. Donner la commande PowerShell à utiliser pour créer le GPO : « GPO2-INTERDIRE_PANNEAU_DE_CONFIGURATION ».
2. Référez-vous à l’image ci-dessus, Pourquoi les GPO : « Default Domain Policy » et « GPO1-AUTORISER_ACCES_NET » ne sont pas appliqués sur l’unité « USousTraitance ».
3. Que devez-vous faire pour autoriser l’accès réseau aux utilisateurs de l’unité « UMUsers » ?


---

1- `Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools`
2- `Install-ADDSDomainController -DomainName "MarocArt.ma" -InstallDns -Credential (Get-Credential) -Force:$true`
