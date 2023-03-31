### Permissions 
`min( max(ntfs) , max(partage) )`

### Role d'un OS
Un système d’exploitation gère les ressources de l’ordinateur telles que l'unité centrale de traitement, la mémoire, les lecteurs de disque et les entres sorties (I/O), crée une interface utilisateur et fournit des services aux logiciels. Les 3 principaux systèmes d’exploitation sont Windows, OS X et Linux. Ils ont été développés par Microsoft, Apple et la communauté open source.

### image d'installation windows
Le format Windows Imaging (**WIM**) est un fichier d' image de disque. Ce format a été développé par Microsoft et permet de déployer les versions de Windows depuis XP SP2 et Server 2008. Ce format est utilisé nativement pour les installations de Windows depuis Vista et Server 2008.

## RAID(Redundant Array of Independent Disk)
volumes à tolérance(disques dynamiques)

|        | Speed | Redundancy |
| ------ | ----- |    ---     |
| RAID0  | x     |            |
| RAID1  |       | x          |
| RAID5  |   x   |     x      |
| RAID10 |   x   |     x      |
| RAID6  |   x   |     x      |
 
### Cluster
En matière de stockage informatique, un cluster fait référence à un groupe de secteurs sur un disque dur qui sont traités comme une seule unité de stockage. Un secteur est la plus petite unité de stockage sur un disque dur qui peut être lue ou écrite à la fois, et un cluster est généralement composé de plusieurs secteurs contigus.

La taille d'un cluster est déterminée par le système de fichiers utilisé sur le disque, et elle varie en fonction de la taille du disque et de la configuration du système de fichiers. Par exemple, sur un disque formaté avec le système de fichiers NTFS utilisé dans Windows, la taille de cluster peut varier de 512 octets à 64 kilo-octets.

L'utilisation de clusters permet au système de fichiers de gérer et d'allouer efficacement l'espace sur le disque pour les fichiers. Lorsqu'un fichier est créé, il est alloué à un ou plusieurs clusters, en fonction de sa taille. Au fur et à mesure que les fichiers sont ajoutés, supprimés ou modifiés, le système de fichiers peut avoir besoin de ré-allouer des clusters pour maintenir une utilisation efficace de l'espace sur le disque.

Dans l'ensemble, l'utilisation de clusters dans le stockage de disque contribue à améliorer l'efficacité et les performances des opérations de stockage et de récupération de fichiers.


### Types de partitions:
Dans le contexte des systèmes d'exploitation et de la gestion de disques, une partition est une région continue d'un disque dur qui est définie pour stocker des données.

Une partition principale est une partition de disque qui peut être utilisée pour démarrer le système d'exploitation. Un disque dur peut contenir au maximum quatre partitions principales, chacune étant identifiée par une lettre de lecteur différente (par exemple C:, D:, E:, etc. sous Windows).

Une partition étendue, quant à elle, est une partition spéciale qui peut contenir plusieurs partitions logiques. Contrairement aux partitions principales, une partition étendue ne peut pas être utilisée pour démarrer le système d'exploitation. Les partitions logiques sont des sous-partitions de la partition étendue et sont également identifiées par des lettres de lecteur différentes.

En d'autres termes, une partition principale est une partition de disque autonome qui peut contenir des données ou être utilisée pour démarrer le système d'exploitation, tandis qu'une partition étendue est une partition spéciale qui peut contenir plusieurs partitions logiques mais ne peut pas être utilisée pour démarrer le système d'exploitation.

![[Pasted image 20230303172122.png]]

 ![[Pasted image 20230303172209.png]]
 
 
 ![[Pasted image 20230303172241.png]]

### Windows minimum requirements
The minimum requirements for Windows 10 include a relatively modern 1-gigahertz (GHz) processor, 1 gigabyte (GB) of RAM for 32-bit Windows or 2 GB for 64-bit, at least 32 GB of hard disk space since the May 2019 Update12, a graphics card that supports DirectX 9 or later with a WDDM driver and a display with a resolution of at least 800×600 pixels


Disques durs IDE (ATA) (Advanced Technology Attachment) 
IDE (Integrated Drive Electronics)

SATA est plus rapide que ATA en raison de plusieurs améliorations de conception qui ont été apportées à cette norme plus récente.

Tout d'abord, SATA utilise une connexion série plutôt qu'une connexion parallèle, ce qui signifie que les données sont transmises en série, une après l'autre, plutôt que simultanément sur plusieurs fils. Cela permet une transmission de données plus rapide et plus fiable.

De plus, SATA utilise un protocole de communication plus avancé, ce qui permet une meilleure gestion des erreurs et une optimisation des performances. SATA utilise également un cache en écriture en mode différé, qui stocke temporairement les données dans un tampon avant de les écrire sur le disque dur, ce qui permet d'optimiser les performances d'écriture.

Enfin, les câbles SATA sont plus minces et plus flexibles que les câbles ATA, ce qui permet de les installer plus facilement et de les utiliser dans des espaces restreints.

Toutes ces améliorations de conception permettent à SATA d'être plus rapide et plus fiable que ATA, offrant ainsi des performances supérieures pour les disques durs et les lecteurs optiques.

### NTFS vs FAT
NTFS (New Technology File System) et FAT (File Allocation Table) sont deux systèmes de fichiers utilisés dans Microsoft Windows. Voici quelques différences entre ces deux systèmes de fichiers :

1.  Taille maximale des fichiers : NTFS permet des fichiers de taille plus grande que FAT. Alors que FAT32 permet des fichiers jusqu'à 4 Go, NTFS permet des fichiers de taille maximale théorique de 16 exaoctets.
    
2.  Compression de fichiers : NTFS permet la compression de fichiers, tandis que FAT ne le permet pas.
    
3.  Sécurité des fichiers : NTFS prend en charge des autorisations plus avancées pour les fichiers et les dossiers, tandis que FAT ne prend en charge que des autorisations de base.
    
4.  Journalisation des fichiers : NTFS est un système de fichiers journalisé, ce qui signifie qu'il enregistre toutes les modifications apportées aux fichiers dans un journal. Cela permet de récupérer plus facilement les données en cas de panne de système ou de perte de données. FAT ne prend pas en charge la journalisation.
    
5.  Défragmentation : NTFS nécessite moins de défragmentation que FAT, car il organise mieux les données sur le disque dur.
    
6.  Compatibilité : FAT est plus compatible avec les systèmes d'exploitation plus anciens et les périphériques tels que les appareils photo numériques, les lecteurs MP3 et les consoles de jeu. NTFS n'est pas toujours pris en charge sur ces périphériques.
    
En général, NTFS est le système de fichiers recommandé pour les ordinateurs exécutant des versions plus récentes de Windows, car il offre des fonctionnalités avancées, une meilleure sécurité et une meilleure performance. Cependant, FAT peut être utile dans certaines situations, telles que la compatibilité avec des périphériques plus anciens.

### MBR vs GPT
![[Pasted image 20230304151955.png]]
![[Pasted image 20230304151903.png]]

### Volume dynamique
Un volume : est une unité de stockage constituée å paltir d'espace disponible sur un ou plusieurs disques
• Volume simple : est un volume dynamique qui englobe l'espace libre disponible d'un seul disque dur dynamique.
• Volumes fractionnés : Un volume fractionné est créé à partir de l'espace disque disponible provenant de plusieurs disques (jusqu'à 32 disques)
• Volume agrégé par bandes (RAID 0) : combme des zones de taille égale d'espace non alloué sur plusieurs disques. Les volumes agrégés fournissent un meilleur débit en répatissant les demandes d'E/S dans tous les disques configurés de l'ensemble
• Volumes en miroir (RAID 1) : Un volume en miroir est un volume å tolérance de pannes qui duplique les données sur deux disques physiques.

Voici la configuration matérielle minimale requise pour Windows 11 : •CPU : 1 GHz ou plus, 2 cœurs minimum, 64 bits •RAM : 4 Go ou plus •Disque : 64 Go ou plus •Carte mère : micrologiciel UEFI avec le démarrage sécurisé (Secure Boot) activé •Puce de sécurité TPM 2.0 •GPU : compatible DirectX 12 avec un pilote WDDM 2.

![[Pasted image 20230304152507.png]]

![[Pasted image 20230304152558.png]]

![[Pasted image 20230304152805.png]]
![[Pasted image 20230304152831.png]]


### Chipset
--- 
circuits intégrés sur la carte mère contrôlant les interactions entre le matériel d'une part et le processeur et la carte mère d'autre part.
Un chipset est un ensemble de circuits intégrés qui forment l’ensemble nécessaire pour fabriquer un appareil électronique tel qu’une carte mère d’ordinateur, qui contrôlent le flux de données et d’instructions entre l’unité centrale de traitement (CPU) ou le microprocesseur et les périphériques externes. Un chipset contrôle les bus externes, la mémoire cache et certains périphériques.