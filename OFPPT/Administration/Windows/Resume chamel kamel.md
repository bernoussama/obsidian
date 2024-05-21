## Active Directory

Voici les associations entre les termes et les définitions de l'image que vous m'avez envoyée :

| Terme | Définition |
|---|---|
| **Domaine** | Le contexte dans lequel on crée des comptes d'utilisateurs, des comptes de groupes et des comptes d'ordinateurs. Il s'agit d'une limite de réplication. | **A** |
| **Catalogue global** | Héberge un jeu d'attributs partiel pour d'autres domaines dans la forêt. Prend en charge les requêtes pour les objets dans l'ensemble de la forêt. | **E** |
| **Contrôleurs de domaine** | Des serveurs qui hébergent la base de données Active Directory (NTDS.DIT) et SYSVOL. | **D** |
| **Schéma AD** | Agit en tant que modèle pour Active Directory DS en définissant les attributs et les classes d'objets. | **C** |
| **Unité d'organisation** | Conteneurs permettent de regrouper des objets dans un domaine. | **B** |

Voici une explication plus détaillée de chaque association :

**Domaine**

Un domaine est un ensemble de ressources informatiques, telles que des ordinateurs, des utilisateurs et des imprimantes, qui sont administrées de manière centralisée. Il est défini par une limite de réplication, ce qui signifie que les informations sur les objets d'un domaine ne sont répliquées que vers les contrôleurs de domaine de ce domaine.

Dans l'image, la définition de "domaine" correspond à la lettre **A**. La définition indique que le domaine est le contexte dans lequel on crée des comptes d'utilisateurs, des comptes de groupes et des comptes d'ordinateurs. Elle indique également que le domaine est une limite de réplication.

**Catalogue global**

Le catalogue global est une copie partielle de l'annuaire Active Directory. Il contient les attributs les plus importants des objets de tous les domaines d'une forêt. Le catalogue global est utilisé pour fournir des services d'annuaire aux utilisateurs et aux applications qui ne se trouvent pas dans le même domaine que les objets dont ils ont besoin.

Dans l'image, la définition de "catalogue global" correspond à la lettre **E**. La définition indique que le catalogue global héberge un jeu d'attributs partiel pour d'autres domaines dans la forêt. Elle indique également que le catalogue global prend en charge les requêtes pour les objets dans l'ensemble de la forêt.

**Contrôleurs de domaine**

Les contrôleurs de domaine sont des serveurs qui hébergent la base de données Active Directory (NTDS.DIT) et SYSVOL. La base de données Active Directory contient des informations sur les objets d'un domaine, tels que les comptes d'utilisateurs, les comptes de groupes et les comptes d'ordinateurs. SYSVOL contient des fichiers de configuration qui sont utilisés par les clients Windows.

Dans l'image, la définition de "contrôleurs de domaine" correspond à la lettre **D**. La définition indique que les contrôleurs de domaine hébergent la base de données Active Directory (NTDS.DIT) et SYSVOL.

**Schéma AD**

Le schéma AD est un modèle qui définit les attributs et les classes d'objets qui peuvent être utilisés dans Active Directory. Il est utilisé pour garantir que les objets d'un domaine sont cohérents et qu'ils peuvent être utilisés par les applications.

Dans l'image, la définition de "schéma AD" correspond à la lettre **C**. La définition indique que le schéma AD agit en tant que modèle pour Active Directory DS en définissant les attributs et les classes d'objets.

**Unité d'organisation**

Une unité d'organisation est un conteneur qui permet de regrouper des objets dans un domaine. Les unités d'organisation peuvent être utilisées pour organiser les objets par fonction, par département ou par tout autre critère.

Dans l'image, la définition de "unité d'organisation" correspond à la lettre **B**. La définition indique que les unités d'organisation permettent de regrouper des objets dans un domaine.

## DNS

### REQUETES DNS de résolution :
---
- ITIRATIVE : permet résolution partielle de l’espace de noms
- RECURSIVE : permet résolution complète de l’espace de noms

### UNITE D’ORGANISATION
---
- Organiser les objets (l’annuaire)
- Lier les GPO
- Déléguer le contrôle


- **GPO** 
	- **Etendue** : ensembles d’objets sur lesquels le GPO sera appliques
	- **L’Etendue peut être filtrée** : filtre de sécurité/ filtre WMI
	- **Filtre de sécurité** : permet de préciser les comptes sur lesquels le GPO sera appliqué