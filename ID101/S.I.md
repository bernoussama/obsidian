
## Definitions:

### SI (Système d'information):
- Le système d’information est une représentation possible de n’importe quel système, notamment tout système humain organisé
- Le SI est le véhicule de la communication dans l’entreprise. Cette communication possède un langage dont les mots sont les données
- Le système d’information est le système de couplage entre le système opérant et le système de pilotage

### Système informatique
- ensembles de resources informatiques matérielles et logiciels permettant d’implémenter une partie du système d'information

### SI informatisé:
- sous ensemble du SI utilisant un système informatique

- Saisie : Saisie des données faisant partie du SI pour qu’elles aient une existence réelle.
- Mémorisation : Permet de retrouver la donnée ultérieurement (persistance) 
- Traitement : Permet d’accéder aux données, les mettre à jour et les mettre en forme.
- Communication : Permet la communication entre les différents acteurs internes et externes à l’entreprise.

![[Pasted image 20230316123113.png]]

*Toute entreprise peut être décomposée en 2 composantes principales :* 
- ***Un système de pilotage*** qui dirige l’entreprise. Il définit la stratégie de l’entreprise et veille à sa bonne application. 
- ***Un système opérant*** qui applique la stratégie fixée par le système de pilotage. Il effectue les tâches quotidiennes de l’entreprise. Le système d’information est le système qui permet la communication entre les acteurs du système de pilotage et ceux du système opérant.
![[Pasted image 20230316115202.png]]

![[Pasted image 20230316123521.png]]

### SI décisionnel
• les objectifs assignés au système opérant ; 
• l’affectation des ressources au système opérant ; 
• le contrôle des résultats obtenus ; 
• la régulation.

 | sur site | cloud   
-- | -- | --   
Avantages | - Vous avez la main sur la gestion de votre  infrastructure  - Proximité et accès physique aux équipements  - Choix et connaissance des différents équipements | - Budget : vous payez en fonction de vos  besoins  Installation et maintenance réalisée par un prestataire  - Flexibilité  - Continuité de service  
Inconvénients | Coûts élevés : installation, configuration, maintenance, etc. - besoin de personne interne qui peut y consacrer du temps - Pas ou peu de flexibilité | selon le pays d'hébergement soyez vigilant quant à la sécurité et la confidentialité de vos données - La connexion se fait obligatoirement par internet

## CH3
---
- L’étape de compréhension de l'existant:
	- Permet de construire un glossaire des termes utilisés
	- réalisée par des analystes

- L'étape de compréhension des besoins:
	- permet de recenser les besoins fonctionnels et non fonctionnels

- Le besoin "Le SI d'information à développer doit être sécurisé" fait partie
	- des besoins non fonctionnels

- Les acteurs qui participent à l'étape de conception du SI sont:
	- Les concepteurs
	- Les architectes de SI

- Les délivrables de l'étape de conception sont:
	- Modèles de données
	- Modèles de traitements

- La mise en oeuvre du SI consiste à:
	- Créer la base de données
	- Développer les modules applicatifs

- Les tests unitaires:
	- consistent à s'assurer du bon fonctionnement de chaque module applicatif
	- Consistent à s’assurer du bon fonctionnement d’un ensemble de modules applicatifs

- Le déploiement du SI:
	- Consiste à installer le nouveau SI dans l'environnement exploitation

- La maintenance corrective:
	- Est effectués lors de l'exploitation des applications
	- Effectuée par l'équipe de développement

- L'ajout d'une nouvelle fonctionnalité au SI est effectuée dans le cadre de:
	- La maintenance évolutive


## CH4
---
- client:
	 - machine besoin d'une resource et n'en dispose pas

- avantages architecture virtualisé:
	  - simplicité de déploiement
	  - simplicité admin 
  
- architecture centralise:
	  - utilise notion de mainframe
  
- middleware:
	  - charge de l’échange de resource entre les serveurs et clients
  
- architecture d'un si:
	 - répartition de resources logiciels sur les resources materiel
  
- architecture 3-tiers:
	  - utilise un seul serveur d'application
	  - présente difficulté d'utilisation de plusieurs technologies dans la logique applicative
  
- architecture n-tiers:
	- déploie la couche applicative sur plusieurs serveurs intermédiaires
	- permet l'utilisation de plusieurs technologies
  
- niveaux de composants logiciels:
	  gestion de données / logique applicative / presentation
  
- architecture orienté services:
	  se constitue d'un producteur et d'un consommateur
	  le consommateur découvre des services en consultant le repertoire des services
  
- Phases de construction SI:
	  phase de conception et développement
	  phase de d'exploitation et maintenance