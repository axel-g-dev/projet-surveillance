## a) Diagramme de cas d’utilisation (SysML)

```mermaid
flowchart LR
    U[Utilisateur]

    U --> UC1[Démarrer la surveillance]
    U --> UC2[Arrêter la surveillance]
    U --> UC3[Visualiser le flux vidéo]
    U --> UC4[Consulter les statistiques]
    U --> UC5[Accéder aux images capturées]

    UC1 --> UC6[Initialiser la caméra]
    UC1 --> UC7[Analyser les images]
    UC7 --> UC8[Détecter un mouvement]
    UC8 --> UC9[Capturer une image]
    UC9 --> UC10[Enregistrer les données]

```

---

## b) Diagramme de séquence (SysML)

**Type :** Diagramme de séquence – Détection et capture

```mermaid
flowchart TD
    A([Démarrer surveillance]) --> B[Initialiser la caméra]
    B --> C{Caméra opérationnelle ?}

    C -- Non --> Z[Afficher une erreur et arrêter]
    C -- Oui --> D[Lire deux images successives]

    D --> E[Prétraiter les images]
    E --> F[Comparer les images]
    F --> G[Appliquer un seuillage]
    G --> H[Rechercher des zones en mouvement]

    H --> I{Mouvement détecté ?}
    I -- Non --> J[Afficher le flux vidéo]
    I -- Oui --> K{Délai minimal écoulé ?}

    K -- Non --> J
    K -- Oui --> L[Capturer une image]
    L --> M[Stocker l’image]
    M --> N[Enregistrer les informations en base]

    J --> O[Lire une nouvelle image]
    O --> D
```

---

## c) Diagramme de classes

```mermaid
classDiagram
    class DatabaseManager {
        -connexion
        +connect()
        +insert(type, file_path)
        +close()
    }

    class SurveillanceManager {
        -camera
        -image_precedente
        -image_courante
        -temps_derniere_capture
        -nb_detections
        -nb_captures
        +initialiser_camera()
        +analyser_images()
        +detecter_mouvement()
        +capturer_image()
        +arreter()
    }

    SurveillanceManager *-- DatabaseManager : utilise
```

---

## d) Schéma réseau

```mermaid
flowchart LR
    Mac[💻 MacBook <br/>192.168.4.X]
    Cam[📷 Webcam interne<br/>Index 1]
    Net[🌐 Wi-Fi]
    Pi[🍓 Raspberry Pi 5<br/>192.168.4.1]

    MySQL[(🗄️ MySQL Server<br/>Port 3306)]
    DB[📂 Base : presence<br/>Table : enregistrement]

    SMB[📁 Partage SMB<br/>Port 445]
    Folder[🗃️ /var/www/recordings]
    Mount[💾 Monté sur Mac<br/>/Volumes/recordings]
    Auth[🔐 id : axel / 
    password : fi27^#COi5mlK##ZB3T4]

    Mac --> Cam
    Mac --> Net --> Pi

    Pi --> MySQL --> DB
    Pi --> SMB --> Folder
    Folder --> Mount
    SMB --> Auth
```

---

## e) Schéma de base de données

```mermaid
erDiagram
    PRESENCE {
        DATABASE presence
    }

    ENREGISTREMENT {
        INT id_log PK
        TIMESTAMP timestamp
        VARCHAR type
        VARCHAR file_path
    }

    PRESENCE ||--o{ ENREGISTREMENT : contains
```

---

