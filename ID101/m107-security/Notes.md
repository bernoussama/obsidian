## Security objectives
--- 
- ***Disponibilité*** : exige qu’une ressource soit disponible et/ou fonctionnelle lorsqu' une entité autorisée la demande ; 

- ***Intégrité*** : exige que les actifs n’ont pas été modifié, détruit, falsifié, ou perdu d’une manière non autorisée ou accidentelle ; 

- ***Confidentialité*** : exige que les données ne soient pas divulguées aux entités à moins qu'elles n'aient été autorisées à accéder et à connaitre ces données.
![[Notes 2023-06-25 13.12.49.excalidraw]]

![[Pasted image 20230615102727.png]]

- ***Authenticité*** : exige d'être authentique et de pouvoir être vérifié, et digne de confiance. En d’autres termes, l’authenticité exige de vérifier que les identités fournies par les entités (utilisateurs ou processus) demandant accès à une ressource ne sont pas fausses et que ces entités sont bien ce qu’elles prétendent être ;

- **Contrôle d'accès**: exige que l'accès à un actif ou une ressource soit contrôlée pour assurer que l’accès n’est possible que pour les entités autorisées ;

- ***Non-répudiation*** : exige que les entités participantes à un évènement ou exécutant une action (tel que l’échange des messages , l’exécution des transactions, etc.) ne peuvent pas nier leur participation à cet évènement, ou l’exécution de cette action, respectivement. Cet objectif pourrait être atteint, en exigeant aux entités de fournir une preuve d’identité avant de participer à un évènement ou exécuter une action ;

- ***Traçabilité*** : exige de suivre les actions exécutées par une entité durant son accès à un actif et de journaliser des informations décrivant les actions exécutées (tel que la durée d’accès, la nature des actions, les données utilisées, etc.) et que les actions exécutées peuvent être attribuées uniquement à cette entité, qui peut alors être tenue responsable de ses actions

### Classification des attaques



![[attaques.excalidraw]]

#### Attaques passives:
- **Lecture du contenu des messages**
	- message (claire) non crypte 
- **analyse du Traffic**
	- message (masque)  crypte

#### Attaques actives
- mascarade (usurpation d’identité)
![[Notes 2023-06-24 22.54.57.excalidraw]]
- rejeu
![[Notes 2023-06-24 23.12.23.excalidraw]]
- modification des messages
![[Notes 2023-06-24 23.21.56.excalidraw]]
- déni de service
![[Notes 2023-06-24 23.28.22.excalidraw]]

#### Attaques internes

#### Attaques externes

> Mascarade = Spoofing





### access control
---
#### AAA
![[Pasted image 20230615103935.png]]


