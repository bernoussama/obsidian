```mermaid
graph TD
    U[Utilisateur] -->|Rechercher un espace| S[Système]
    U -->|Réserver un espace| S
    U -->|Annuler une réservation| S
    U -->|Payer une réservation| S
    U -->|Consulter l’historique| S
    A[Administrateur] -->|Ajouter un espace| S
    A -->|Modifier un espace| S
    A -->|Supprimer un espace| S
    A -->|Valider une réservation| S
    G[Gestionnaire d’espaces] -->|Vérifier la disponibilité| S
    G -->|Mettre à jour l’état des espaces| S
```
```mermaid
classDiagram
    class Utilisateur {
        +String id
        +String nom
        +String email
        +String motDePasse
        +String téléphone
    }
    class Espace {
        +String id
        +String type
        +int capacité
        +String localisation
        +String équipements
        +float tarif
    }
    class Réservation {
        +String id
        +String idUtilisateur
        +String idEspace
        +Date dateDébut
        +Date dateFin
        +String statut
        +float montant
    }
    class Paiement {
        +String id
        +String idRéservation
        +float montant
        +String méthode
        +String statut
    }
    class Administrateur {
        +String id
        +String nom
        +String email
        +String rôle
    }
    Utilisateur "1" --> "0..*" Réservation
    Espace "1" --> "0..*" Réservation
    Réservation "1" --> "1" Paiement
```
```mermaid
graph TD
    A[Début] --> B[Utilisateur se connecte]
    B --> C[Recherche un espace]
    C --> D{Afficher espaces disponibles}
    D -->|Sélectionner espace| E[Entrer dates]
    E --> F{Vérifier disponibilité}
    F -->|Disponible| G[Effectuer paiement]
    F -->|Non disponible| C
    G --> H{Valider paiement}
    H -->|Succès| I[Confirmer réservation]
    H -->|Échec| G
    I --> J[Envoyer notification]
    J --> K[Fin]
```
### diagramme de sequence
```mermaid
sequenceDiagram
    participant U as Utilisateur
    participant I as Interface
    participant S as Système
    participant DB as Base de données
    participant P as Service de paiement
    U->>I: Rechercher un espace
    I->>S: Demander disponibilités
    S->>DB: Récupérer espaces disponibles
    DB-->>S: Retourner résultats
    S-->>I: Afficher résultats
    U->>I: Sélectionner espace et dates
    I->>S: Vérifier disponibilité
    S->>DB: Confirmer disponibilité
    DB-->>S: Disponible
    S-->>I: Proposer paiement
    I->>P: Lancer paiement
    P-->>S: Confirmer paiement
    S->>DB: Enregistrer réservation
    S-->>U: Envoyer confirmation
```
## diagramme d'etat
```mermaid
stateDiagram
    [*] --> En_attente
    En_attente --> Confirmée : Paiement effectué
    En_attente --> Annulée : Annulation
    Confirmée --> Annulée : Annulation
    Confirmée --> Terminée : Fin de l’événement
    Annulée --> [*]
    Terminée --> [*]
```
## diagramme de composants
```mermaid
graph TD
    subgraph Frontend
        FE[Interface Utilisateur]
    end
    subgraph Backend
        BE[Logique Métier]
        API[API REST]
    end
    subgraph Base de données
        DB[PostgreSQL]
    end
    subgraph Services Externes
        P[Service de Paiement]
        N[Service de Notification]
    end
    FE --> API
    API --> BE
    BE --> DB
    BE --> P
    BE --> N
```
## diagramme de deploiement
```mermaid
deploymentDiagram
    device "Client" {
        artifact "Navigateur Web"
    }
    device "Serveur d’application" {
        artifact "Node.js/Express"
    }
    device "Serveur de base de données" {
        artifact "PostgreSQL"
    }
    device "Services Externes" {
        artifact "Stripe/Twilio"
    }
    "Navigateur Web" --> "Node.js/Express" : HTTPS
    "Node.js/Express" --> "PostgreSQL" : Connexion sécurisée
    "Node.js/Express" --> "Stripe/Twilio" : API
```
## diagramme de communication
```mermaid
sequenceDiagram
    participant U as Utilisateur
    participant I as Interface
    participant S as Système
    participant DB as Base de données
    U->>I: Rechercher espace
    I->>S: Vérifier disponibilité
    S->>DB: Récupérer données
    DB-->>S: Retourner données
    S-->>I: Afficher résultats
    I-->>U: Présenter espaces disponibles
```
