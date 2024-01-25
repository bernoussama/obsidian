
1. Définir un système serveur et un système client
2. Citez les éditions de WINDOWS SERVER 2016
3. Quelle est la différence entre une installation minimale et une installation complète
4. Donnez la commande powershell à utiliser pour modifier le nom d'une machine
5. Donnez la commande powershell à utiliser pour attribuer :
	- *adresse : 192.168.1.2/24
	- *paserelle :192.168.1.254
1. Donner lacommande powershell pour configurer l'adresse du serveur DNS
2. Donner la commande à utiliser pour afficher la configuration ip
3. Citez les outils à utiliser pour gérer un serveur Core
4. Donner la définition d'Hyper-V
5. Quelle est la différence entre une mémoire fixe et dynamique
6. Quelle est la différence entre un disque fixe et dynamique
7. Donner la commande powershell à utiliser pour installer le service Hyper-V
8. Donner la commande powershell à utiliser pour créer un switch virtuel nommé: switch0
9. Donner la commande powershell à utiliser pour créer la machine virtuelle VM1 avec disque VHDX de taille 40GO 2GO de RAM et lier cette machine au switch : switch0

# Reponses
1. Un système serveur est un ordinateur ou un logiciel conçu pour fournir des services, des ressources ou des fonctionnalités à d'autres ordinateurs, appelés clients, dans un réseau. Le serveur répond aux demandes des clients et facilite la communication, le partage de données, ou l'accès à des ressources spécifiques.

2. Les éditions de Windows Server 2016 sont les suivantes :
   - Windows Server 2016 Standard
   - Windows Server 2016 Datacenter
   - Windows Server 2016 Essentials
   - Windows Server 2016 MultiPoint Premium
   - Windows Server 2016 Storage Server

3. La différence entre une installation minimale et une installation complète de Windows Server 2016 réside dans la quantité de composants installés :
   - Une installation minimale, appelée "Server Core," installe uniquement l'essentiel du système d'exploitation sans interface utilisateur graphique (GUI). Elle est destinée aux serveurs nécessitant une empreinte légère et une sécurité accrue.
   - Une installation complète inclut l'interface utilisateur graphique (GUI) et une gamme plus étendue de fonctionnalités, ce qui la rend plus adaptée à des scénarios où l'administration via une interface utilisateur est nécessaire.

4. Pour modifier le nom d'une machine en PowerShell, utilisez la commande suivante :
   ```powershell
   Rename-Computer -NewName "NouveauNom"
   ```

5. Pour configurer une adresse IP statique en PowerShell, utilisez les commandes suivantes pour définir l'adresse IP et la passerelle :
   ```powershell
New-NetIPAddress -InterfaceAlias "Nom de l'interface" -IPAddress 192.168.1.2 -PrefixLength 24
Set-NetIPInterface -InterfaceAlias "Nom de l'interface" -Dhcp Disabled
Set-NetIPInterface -InterfaceAlias "Nom de l'interface" -DefaultGateway 192.168.1.254
   ```

6. Pour configurer l'adresse du serveur DNS en PowerShell, utilisez la commande suivante :
```powershell
Set-DnsClientServerAddress -InterfaceAlias "Nom de l'interface" -ServerAddresses "192.168.1.2"
```

7. Pour afficher la configuration IP en PowerShell, utilisez la commande suivante :
   ```powershell
Get-NetIPAddress
   ```

8. Les outils à utiliser pour gérer un serveur Core incluent #PowerShell, RSAT, Server Manager (à distance), sconfig, et diverses commandes en ligne.

9. #Hyper-V est une technologie de virtualisation de Microsoft qui permet de créer et de gérer des machines virtuelles sur un serveur physique. Il permet d'exécuter plusieurs systèmes d'exploitation sur une seule machine physique.

10. La différence entre la mémoire fixe et dynamique dans Hyper-V est la suivante :
   - Mémoire fixe : La mémoire allouée à la machine virtuelle est réservée et ne peut pas être partagée avec d'autres machines virtuelles. Cela garantit une allocation de mémoire constante mais peut gaspiller de la mémoire lorsque la machine virtuelle n'en a pas besoin.
   - Mémoire dynamique : La mémoire allouée à la machine virtuelle peut être partagée avec d'autres machines virtuelles en fonction de leurs besoins. Cela permet d'optimiser l'utilisation de la mémoire, mais la machine virtuelle peut ne pas avoir accès à une quantité fixe de mémoire en permanence.

11. La différence entre un disque fixe et dynamique dans Hyper-V est la suivante:
   - Disque fixe : Un disque dur virtuel de taille fixe alloue tout l'espace disque lors de sa création. Il garantit des performances constantes mais utilise immédiatement tout l'espace alloué sur le disque physique, même s'il n'est pas utilisé par la machine virtuelle.
   - Disque dynamique : Un disque dur virtuel de taille dynamique augmente progressivement sa taille à mesure que la machine virtuelle écrit des données, mais il ne prend que l'espace physique nécessaire. Cela permet d'économiser de l'espace disque, mais les performances peuvent être légèrement inférieures aux disques fixes.

12. Pour installer le service Hyper-V en PowerShell, utilisez la commande suivante :
   ```powershell
Install-WindowsFeature -Name Hyper-V -IncludeManagementTools -Restart
   ```

13. Pour créer un switch virtuel nommé "switch0" en PowerShell, utilisez la commande suivante :
   ```powershell
New-VMSwitch -Name switch0 -SwitchType Internal
   ```

14. Pour créer une machine virtuelle nommée "VM1" avec un disque VHDX de 40 Go, 2 Go de RAM et la lier au switch "switch0" en PowerShell, utilisez les commandes suivantes :
   ```powershell
New-VM -Name VM1 -MemoryStartupBytes 2GB -BootDevice VHD -VHDPath "Chemin_VHDX" -SwitchName switch0
   ```

Assurez-vous de personnaliser les noms, les tailles et les chemins selon vos besoins spécifiques.