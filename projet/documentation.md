# **Dossier de mini-projet**

## **Page de garde**

* **Titre du projet :** Vidéo surveillance
* **Noms des étudiants :** L.D. & A.G
* **Classe :** CIEL2
* **Année scolaire :** 2025-2026
* **Enseignant référent :** M. Boudjelaba

---
## Sommaire

- [**Dossier de mini-projet**](#dossier-de-mini-projet)
  - [**Page de garde**](#page-de-garde)
  - [Sommaire](#sommaire)
- [**1. Notice d'utilisation**](#1-notice-dutilisation)
  - [**1.1. Objectif du produit ou de l'application**](#11-objectif-du-produit-ou-de-lapplication)
  - [**1.2. Prérequis**](#12-prérequis)
  - [**1.3. Procédure d'utilisation**](#13-procédure-dutilisation)
    - [**Étape 1 : Montage du dossier partagé**](#étape-1--montage-du-dossier-partagé)
    - [**Étape 2 : Préparation de l'environnement et installation des librairies**](#étape-2--préparation-de-lenvironnement-et-installation-des-librairies)
    - [**Étape 3 : Test de connexion base de données**](#étape-3--test-de-connexion-base-de-données)
    - [**Étape 4 : Démarrage du système**](#étape-4--démarrage-du-système)
    - [**Étape 5 : Utilisation de l'interface**](#étape-5--utilisation-de-linterface)
    - [**Étape 6 : Arrêt du système**](#étape-6--arrêt-du-système)
  - [**1.4. Conseils et remarques**](#14-conseils-et-remarques)
- [**2. Fiche(s) de recette**](#2-fiches-de-recette)
  - [**Fiche recette n°1**](#fiche-recette-n1)
    - [**Étapes du test**](#étapes-du-test)
  - [**Fiche recette n°2**](#fiche-recette-n2)
    - [**Étapes du test**](#étapes-du-test-1)
  - [**Fiche recette n°3**](#fiche-recette-n3)
    - [**Étapes du test**](#étapes-du-test-2)
  - [**Fiche recette n°4**](#fiche-recette-n4)
    - [**Étapes du test**](#étapes-du-test-3)
- [**3. Rapport du projet**](#3-rapport-du-projet)
  - [**3.1. Introduction**](#31-introduction)
  - [**3.2. Cahier des charges**](#32-cahier-des-charges)
  - [**3.3. Analyse \& Conception**](#33-analyse--conception)
    - [**a) Diagramme de cas d'utilisation (SysML)**](#a-diagramme-de-cas-dutilisation-sysml)
    - [**b) Diagramme de séquence (SysML)**](#b-diagramme-de-séquence-sysml)
    - [**c) Diagramme de Classe**](#c-diagramme-de-classe)
    - [**d) Diagramme de Gantt**](#d-diagramme-de-gantt)
    - [**d) Planning des séances**](#d-planning-des-séances)
    - [**e) Fiche de suivi du projet**](#e-fiche-de-suivi-du-projet)
  - [**3.4. Réalisation**](#34-réalisation)
    - [**a) Description du travail effectué**](#a-description-du-travail-effectué)
    - [**b) Schéma réseau**](#b-schéma-réseau)
    - [**b) Schéma de base de données**](#b-schéma-de-base-de-données)
    - [**d) Compléments base de données**](#d-compléments-base-de-données)
  - [**3.5. Développement \& Tests**](#35-développement--tests)
    - [**a) Code développé (extraits pertinents)**](#a-code-développé-extraits-pertinents)
    - [**b) Tests unitaires**](#b-tests-unitaires)
  - [**3.6. Difficultés rencontrées**](#36-difficultés-rencontrées)
  - [**3.7. Conclusion \& perspectives**](#37-conclusion--perspectives)
- [**4. Annexes**](#4-annexes)
  - [**Annexe A : Structure du projet**](#annexe-a--structure-du-projet)
  - [**Annexe B : Configuration système**](#annexe-b--configuration-système)
  - [**Annexe C : Paramètres de détection**](#annexe-c--paramètres-de-détection)
  - [**Annexe D : Format des fichiers générés**](#annexe-d--format-des-fichiers-générés)
  - [**Annexe E : Lien vers le code source**](#annexe-e--lien-vers-le-code-source)
  - [**Annexe F : Captures d'écran**](#annexe-f--captures-décran)
  - [**Annexe G : Photos de la réalisation**](#annexe-g--photos-de-la-réalisation)

---

# **1. Notice d'utilisation**

## **1.1. Objectif du produit ou de l'application**

Système de vidéosurveillance temps réel pour PC portable intégré dans une architecture de surveillance distribuée. Le système capture automatiquement des images lors de détections de mouvement et synchronise les données avec un serveur Raspberry Pi 5 centralisé.

**Contexte :** Mini-Projet 1 - Tâche 1 (Vidéosurveillance)

**Fonctionnalités principales :**
- Analyse du flux vidéo par différence d'images
- Détection de mouvement par seuil et contours
- Capture automatique avec horodatage
- Stockage sur dossier partagé SMB
- Enregistrement du chemin de stockage des images dans une base MySQL distante
- Interface de monitoring Streamlit depuis un navigateur

## **1.2. Prérequis**

Pour faire fonctionner le système, l'environnement suivant est nécessaire :

**Matériel :**

  * **Ordinateur de surveillance :** MacBook (ou PC portable) avec Python installé
  * **Dispositif de capture :** Webcam intégrée ou caméra externe (ex : iPhone via Continuity Camera)
  * **Serveur central :** Raspberry Pi 5 (4 Go RAM, 32 Go stockage)
  * **Réseau :** Connexion stable entre l'ordinateur et le Raspberry Pi (Adresse cible : `192.168.4.1`)

**Logiciels et Environnement :**

  * **Langage :** Python 3.13.5 ou supérieur
  * **Éditeur de code :** VSCode (recommandé)
  * **Base de données :** Serveur MySQL actif sur le Raspberry Pi
  * **Système d'exploitation :** macOS (utilisé pour ce projet, backend AVFoundation) ou Windows/Linux

**Librairies Python et installation :**

Les bibliothèques suivantes sont requises pour le fonctionnement du script :

  * `streamlit` : Interface web de monitoring et widgets de contrôle
  * `opencv-python` : Capture vidéo, détection de mouvement et traitement d'image
  * `numpy` : Manipulation optimisée des matrices (utilisé par OpenCV)
  * `mysql-connector-python` : Connecteur officiel pour la communication avec la BDD

**Commande d'installation :**
Exécutez la commande suivante dans votre terminal (ou environnement virtuel) pour installer toutes les dépendances :

```bash
pip install streamlit opencv-python numpy mysql-connector-python
```

**Configurations particulières :**

  * **Accès au dossier partagé (SMB)**

      * **Chemin de montage local :** `/Volumes/recordings`
      * **Utilisateur :** `axel`
      * **Mot de passe :** `fi27^#COi5mlK##ZB3T4`

  * **Connexion Base de données (MySQL)**

      * **Serveur hôte :** `192.168.4.1` (Port 3306)
      * **Nom de la base :** `presence`
      * **Table cible :** `enregistrement`
      * **Utilisateur SQL :** `presence`


## **1.3. Procédure d'utilisation**

### **Étape 1 : Montage du dossier partagé**

**Via Finder :**
1. Ouvrir Finder
2. Menu Aller > Se connecter au serveur (Cmd+K)
3. Saisir : `smb://192.168.4.1/recordings`
4. Utilisateur : `axel`
5. Mot de passe : `fi27^#COi5mlK##ZB3T4`
6. Le dossier apparaît dans `/Volumes/recordings`

**Via terminal :**
```bash
mkdir -p /Volumes/recordings
mount -t smbfs //axel:fi27^#COi5mlK##ZB3T4@192.168.4.1/recordings /Volumes/recordings
```

**Vérification :**
```bash
ls -la /Volumes/recordings
touch /Volumes/recordings/test.txt && rm /Volumes/recordings/test.txt
```

### **Étape 2 : Préparation de l'environnement et installation des librairies**

```bash
cd /Users/axel/Desktop/surveillance_camera/
python3 -m venv venv
source venv/bin/activate
```
**Ensuite veuillez installer les librairies suivantes, si vous ne l'avez pas déjà fait :**

```bash
pip install streamlit opencv-python numpy mysql-connector-python
```

### **Étape 3 : Test de connexion base de données**

```bash
mysql -h 192.168.4.1 -u presence -p
# Mot de passe : *9RSSFr5bD0WO64qurDY
```

```sql
USE presence;
SELECT * FROM enregistrement ORDER BY id_log DESC LIMIT 5;
```

### **Étape 4 : Démarrage du système**

```bash
streamlit run code.py
```

L'interface s'ouvre automatiquement dans le navigateur à l'adresse `http://localhost:8501`

### **Étape 5 : Utilisation de l'interface**

**Barre latérale :**
- Cliquer sur "Démarrer" pour initialiser la caméra et lancer la surveillance
- Les statistiques s'affichent en temps réel (Détections, Captures, Durée)
- Cliquer sur "Arrêter" pour stopper la surveillance
- Cliquer sur "Ouvrir dossier" pour accéder aux captures

**Zone principale :**
- Flux vidéo en direct avec rectangles verts sur zones en mouvement 

### **Étape 6 : Arrêt du système**

**Via interface :**
- Clic sur "Arrêter" dans la sidebar

**Puis dans le terminal :**
- `Ctrl+C` 

**Désactivation environnement :**
```bash
deactivate
```

## **1.4. Conseils et remarques**

**Limites connues :**
- Le stockage Raspberry Pi est limité à 32 Go
- Le délai minimal entre captures est de 5 secondes
- La détection nécessite un éclairage stable

**Précautions d'utilisation :**
- Vérifier que le dossier partagé est monté avant le démarrage
- Vérifier la connexion réseau vers `192.168.4.1`
- Ne pas modifier les paramètres de détection sans comprendre leur impact

**Recommandations :**
- Surveiller l'espace disque disponible sur le Raspberry Pi
- Nettoyer régulièrement les anciennes captures
- Maintenir l'environnement virtuel à jour

**Configuration DEBUG :**
- `DEBUG = True` : Active les logs de connexion DB, sauvegardes, résolution caméra
- `DEBUG_MOTION = False` : Logs verbeux de détection (désactivé par défaut)
- Les messages apparaissent dans le terminal exécutant Streamlit

---

# **2. Fiche(s) de recette**

## **Fiche recette n°1**

* **Titre du test :** Test de détection de mouvement
* **Objectif du test :** Vérifier que le système détecte correctement les mouvements et capture les images
* **Préconditions :** 
  - Caméra initialisée
  - Dossier partagé monté
  - Connexion MySQL active

### **Étapes du test**

1. Lancer le système avec "Démarrer"
2. Passer la main devant la caméra
3. Observer le rectangle vert autour de la zone en mouvement
4. Attendre 5 secondes
5. Vérifier la présence de l'image dans `/Volumes/recordings`
6. Vérifier l'enregistrement dans la base MySQL

* **Résultat attendu :** Image capturée avec nom `mouvement_YYYYMMDD-HHMMSS.jpg` et enregistrement en base avec type "mouvement"
* **Résultat obtenu :** ………………………………………
* **Validation :** OK / KO

## **Fiche recette n°2**

* **Titre du test :** Test du délai anti-rafale
* **Objectif du test :** Vérifier que le système respecte le délai minimal de 5 secondes entre captures
* **Préconditions :** 
  - Système en cours d'exécution
  - Au moins une capture déjà effectuée

### **Étapes du test**

1. Effectuer un mouvement pour déclencher une première capture
2. Immédiatement après, effectuer un second mouvement
3. Observer les statistiques : "Détections" augmente mais pas "Captures"
4. Attendre 5 secondes
5. Effectuer un troisième mouvement
6. Vérifier que "Captures" augmente

* **Résultat attendu :** Pas de sauvegarde pendant les 5 secondes suivant la première capture
* **Résultat obtenu :** ………………………………………
* **Validation :** OK / KO

## **Fiche recette n°3**

* **Titre du test :** Test de connexion base de données
* **Objectif du test :** Vérifier l'enregistrement correct des métadonnées dans MySQL
* **Préconditions :** 
  - Serveur MySQL accessible sur 192.168.4.1
  - Base `presence` créée avec table `enregistrement`

### **Étapes du test**

1. Déclencher une capture
2. Se connecter à la base MySQL
3. Exécuter : `SELECT * FROM enregistrement ORDER BY id_log DESC LIMIT 1;`
4. Vérifier que le `file_path` correspond à l'image capturée
5. Vérifier que le `type` est "mouvement"
6. Vérifier que le `timestamp` correspond à l'heure de capture

* **Résultat attendu :** Enregistrement présent avec toutes les informations correctes
* **Résultat obtenu :** ………………………………………
* **Validation :** OK / KO

## **Fiche recette n°4**

* **Titre du test :** Test de sensibilité des paramètres
* **Objectif du test :** Vérifier que les paramètres THRESHOLD_VALUE et MIN_AREA filtrent correctement les faux positifs
* **Préconditions :** 
  - Système démarré dans un environnement stable

### **Étapes du test**

1. Observer le flux sans mouvement pendant 1 minute
2. Vérifier qu'aucune détection ne se produit
3. Déplacer un petit objet (< 15 cm)
4. Vérifier qu'aucune détection ne se produit
5. Passer devant la caméra
6. Vérifier qu'une détection se produit

* **Résultat attendu :** Aucun faux positif, détection correcte des mouvements humains
* **Résultat obtenu :** ………………………………………
* **Validation :** OK / KO

---

# **3. Rapport du projet**

## **3.1. Introduction**

Dans le cadre du projet de vidéosurveillance (Mini-Projet 1 – Tâche 1), le but est de créer un système de surveillance basé sur la détection de mouvement. Un PC portable équipé d’une webcam s’occupe de détecter les mouvements et de prendre les images, tandis qu’un Raspberry Pi 5 sert de serveur pour stocker et gérer les données.

Le principal défi est de détecter les mouvements de manière fiable, de capturer uniquement les images utiles et de les envoyer vers le serveur, tout en limitant les fausses alertes et l’espace de stockage utilisé.

## **3.2. Cahier des charges**

**Besoin principal :**
Mettre en place un système de vidéosurveillance automatisé pour détecter et enregistrer les événements de mouvement dans une zone surveillée.

**Fonctions attendues :**
- Installation et configuration de la caméra (logiciel)
- Développement Python du programme de surveillance
- Détection automatique de mouvement par analyse d'images
- Capture automatique avec horodatage
- Sauvegarde des photos dans un dossier partagé
- Enregistrement du chemin de stockage des images dans une base MySQL
- Interface de monitoring en temps réel
- Documentation logicielle complète

**Contraintes techniques :**
- Langage : Python 3.13.5
- Système d'exploitation : macOS
- Backend vidéo : AVFoundation (spécifique Mac)
- Serveur : Raspberry Pi 5 (4 Go RAM, 32 Go stockage)
- Base de données : MySQL sur Raspberry Pi `192.168.4.1`
- Stockage : Dossier partagé SMB avec authentification
- Format images : JPEG avec nom horodaté

**Contraintes matérielles :**
- MacBook Pro avec webcam intégrée (Index 1) ou iPhone via Continuity Camera (Index 0)
- Connexion réseau stable entre Mac et Raspberry Pi
- Espace disque suffisant pour le stockage des captures
- Ne pas stocker le flux vidéo 

## **3.3. Analyse & Conception**

### **a) Diagramme de cas d'utilisation (SysML)**

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

### **b) Diagramme de séquence (SysML)**

**Type :** Diagramme de séquence - Détection et capture

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
### **c) Diagramme de Classe**

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

### **d) Diagramme de Gantt**

*(À insérer : planning montrant les phases du projet : Installation environnement, Développement détection, Intégration base de données, Tests, Documentation)*

### **d) Planning des séances**

| Séance | Travail réalisé |
| ------ | --------------- |
| 1      | Installation de l'environnement Python, configuration du dossier partagé, tests de connexion MySQL |
| 2      | Développement de la classe DatabaseManager, création de la table enregistrement, tests d'insertion |
| 3      | Développement de la classe SurveillanceManager, implémentation de l'acquisition caméra |
| 4      | Implémentation de l'algorithme de détection de mouvement (preprocessing, détection, filtrage) |
| 5      | Optimisation des paramètres de sensibilité (THRESHOLD_VALUE, MIN_AREA, BLUR_KERNEL) |
| 6      | Développement de l'interface Streamlit, intégration des statistiques temps réel |
| 7      | Tests unitaires et tests d'intégration, validation des fiches de recette |
| 8      | Rédaction de la documentation, finalisation du rapport |

### **e) Fiche de suivi du projet**

| Tâche | Responsable | Avancement | Difficultés |
| ----- | ----------- | ---------- | ----------- |
| Installation caméra | L.D. | 100% | Choix de l'index caméra (iPhone vs webcam interne) |
| Développement Python | A.G. | 100% | Optimisation des paramètres de détection pour réduire les faux positifs |
| Base de données | L.D. | 100% | Gestion de la reconnexion MySQL en cas de perte réseau |
| Documentation | L.D., A.G. | 100% | - |
| Tests | L.D., A.G. | En cours | - |

## **3.4. Réalisation**

### **a) Description du travail effectué**

Le projet a été réalisé en plusieurs étapes successives :

**1. Configuration de l'environnement :**
- Installation de Python 3.13.5 et création d'un environnement virtuel
- Montage du dossier partagé SMB vers le Raspberry Pi avec authentification
- Installation des librairies : streamlit, opencv-python, numpy, mysql-connector-python

**2. Développement de la base de données :**
- Création de la table `enregistrement` sur MySQL du Raspberry Pi
- Structure : id_log, timestamp, type, file_path

**3. Développement de la classe DatabaseManager :**
- Méthode `connect()` : Connexion TCP vers `192.168.4.1:3306` avec vérification d'état
- Méthode `insert()` : Insertion paramétrée pour éviter l'injection SQL
- Méthode `close()` : Fermeture propre de la connexion

**4. Développement de la classe SurveillanceManager :**
- Initialisation de la caméra avec buffer double frame (frame_a, frame_b)
- Algorithme de détection : différence absolue, seuillage à 30, & extraction de contours
- Filtrage par surface minimale (1000 pixels)
- Système de temporisation anti-rafale (5 secondes)
- Annotation visuelle avec rectangles verts

**5. Développement de l'interface Streamlit :**
- Configuration de la mise en page (sidebar, zone principale)
- Boutons de contrôle (Démarrer, Arrêter, Ouvrir dossier)
- Affichage du flux vidéo en temps réel avec redimensionnement automatique
- Statistiques dynamiques (Détections, Captures, Durée)
- Gestion de l'état avec `session_state`

**6. Optimisation des paramètres :**
- THRESHOLD_VALUE = 30 : Équilibre entre sensibilité et faux positifs
- MIN_AREA = 1000 : Filtre les objets < 15 cm
- BLUR_KERNEL = 11x11 : Suppression du bruit webcam
- MIN_TIME_BETWEEN_PHOTOS = 5 : Évite la saturation du stockage, stocke une seulement photo toutes les 5 secondes s'il y a un mouvement

**Choix techniques justifiés :**
- **Streamlit** : Simple à mettre en place, rechargement à chaud, widgets natifs sans HTML/CSS
- **OpenCV** : Open source, support macOS natif, documentation exhaustive avec tutoriels communautaires massifs
- **Numpy** : Opérations vectorisées et plus simples
- **MySQL Connector** : Cconnecteur officiel permettant l’accès à la base de données, avec prise en charge des requêtes paramétrées et une gestion automatique des délais d’attente (timeouts)


### **b) Schéma réseau**

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
### **b) Schéma de base de données**

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


### **d) Compléments base de données**

**Table : enregistrement**

```sql
DROP TABLE IF EXISTS enregistrement;

CREATE TABLE enregistrement (
    id_log INT(11) NOT NULL AUTO_INCREMENT,
    timestamp TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    type VARCHAR(50) DEFAULT NULL,
    file_path VARCHAR(255) DEFAULT NULL,
    PRIMARY KEY (id_log)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;
```

**Exemple d'enregistrement :**
```
id_log: 1452
timestamp: 2025-12-02 14:32:04
type: mouvement
file_path: /Volumes/recordings/mouvement_20251202-143204.jpg
```

**Particularités :**
- `timestamp` : Mise à jour automatique (ON UPDATE CURRENT_TIMESTAMP)
- `type` : Toujours "mouvement" pour détections webcam
- `file_path` : Chemin absolu tel que vu depuis le Mac
- Moteur InnoDB : Fiabilité transactionnelle
- Charset utf8mb4 : Compatibilité internationale

## **3.5. Développement & Tests**

### **a) Code développé (extraits pertinents)**

**Configuration globale :**
```python
DEBUG = True
DEBUG_MOTION = False
SAVE_FOLDER = "/Volumes/recordings"
CAM_INDEX = 1
THRESHOLD_VALUE = 30
MIN_AREA = 1000
BLUR_KERNEL = (11, 11)
MIN_TIME_BETWEEN_PHOTOS = 5

DB_CONFIG = {
    'host': '192.168.4.1',
    'port': 3306,
    'user': 'presence',
    'password': '*9RSSFr5bD0WO64qurDY',
    'database': 'presence'
}
```

**Classe DatabaseManager :**
```python
class DatabaseManager:
    def __init__(self):
        self.conn = None

    def connect(self):
        if self.conn and self.conn.is_connected():
            return True
        try:
            self.conn = mysql.connector.connect(**DB_CONFIG)
            if DEBUG:
                print("[DB] Connexion OK.")
            return True
        except Exception as e:
            print("[DB] ERREUR:", e)
            return False

    def insert(self, event_type, path):
        if not self.connect():
            return False
        try:
            cursor = self.conn.cursor()
            query = "INSERT INTO enregistrement (type, file_path) VALUES (%s, %s)"
            cursor.execute(query, (event_type, path))
            self.conn.commit()
            cursor.close()
            if DEBUG:
                print(f"[DB] Ajout enregistrement OK → {path}")
            return True
        except Exception as e:
            print("[DB] ERREUR INSERT :", e)
            return False

    def close(self):
        if self.conn and self.conn.is_connected():
            self.conn.close()
            if DEBUG:
                print("[DB] Connexion fermée.")
```

**Classe SurveillanceManager - Méthode de détection :**
```python
def detect_motion(self, fa, fb):
    diff = cv2.absdiff(fa, fb)
    _, th = cv2.threshold(diff, THRESHOLD_VALUE, 255, cv2.THRESH_BINARY)
    dil = cv2.dilate(th, None, iterations=2)
    cnts, _ = cv2.findContours(dil, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
    return [c for c in cnts if cv2.contourArea(c) > MIN_AREA]
```

**Classe SurveillanceManager - Sauvegarde avec temporisation :**
```python
def save_picture(self, frame):
    now = time.time()
    if now - self.last_capture < MIN_TIME_BETWEEN_PHOTOS:
        return False
    self.last_capture = now
    ts = datetime.now().strftime("%Y%m%d-%H%M%S")
    filename = f"mouvement_{ts}.jpg"
    path = os.path.join(SAVE_FOLDER, filename)
    cv2.imwrite(path, frame)
    self.total_saved += 1
    self.db.insert("mouvement", path)
    if DEBUG:
        print("[SAVE] Photo:", path)
    return True
```

### **b) Tests unitaires**

**Test de la classe DatabaseManager :**
- Vérification de la connexion MySQL
- Test d'insertion d'un enregistrement
- Vérification de la fermeture propre

**Test de la classe SurveillanceManager :**
- Test d'initialisation de la caméra
- Test du prétraitement (conversion gris + flou)
- Test de détection de mouvement avec images synthétiques
- Test du système de temporisation

**Test d'intégration :**
- Test complet du cycle : détection → capture → enregistrement BDD
- Test de la gestion des erreurs réseau
- Test de la reconnexion automatique MySQL

## **3.6. Difficultés rencontrées**

**1. Choix de l'index caméra :**
- **Problème :** MacBook dispose de 2 caméras (iPhone Continuity Camera = Index 0, Webcam interne = Index 1)
- **Solution :** Test des deux indices et sélection de l'index 1 (webcam interne) pour stabilité et disponibilité permanente

**2. Optimisation des paramètres de détection :**
- **Problème :** Trop de faux positifs avec THRESHOLD_VALUE = 20 (détection du bruit numérique)
- **Solution :** Augmentation à 30 et combinaison avec MIN_AREA = 1000 pour filtrage double niveau

**3. Gestion de la reconnexion MySQL :**
- **Problème :** Perte de connexion après inactivité prolongée
- **Solution :** Vérification systématique avec `is_connected()` avant chaque opération et reconnexion automatique

**4. Saturation du stockage :**
- **Problème :** Génération de centaines d'images quasi-identiques lors d'un mouvement prolongé
- **Solution :** Implémentation du système de temporisation MIN_TIME_BETWEEN_PHOTOS = 5 secondes

**5. Performance de l'interface Streamlit :**
- **Problème :** Latence de rafraîchissement avec images haute résolution
- **Solution :** Redimensionnement automatique des frames (max 1200x675) avant affichage

## **3.7. Conclusion & perspectives**

**Bilan du projet :**

Le système de vidéosurveillance développé répond aux objectifs fixés dans le cahier des charges. L'architecture distribuée avec un MacBook Pro comme client de surveillance et un Raspberry Pi 5 comme serveur centralisé permet une séparation claire des responsabilités et une scalabilité future.

Les choix techniques se sont révélés pertinents :
- OpenCV offre des performances optimales pour la détection temps réel
- Streamlit permet un monitoring simple et efficace
- La base MySQL centralisée facilite la gestion des logs
- Le stockage sur dossier partagé évite la surcharge du réseau

Les paramètres de détection (THRESHOLD_VALUE = 30, MIN_AREA = 1000) offrent un bon équilibre entre sensibilité et faux positifs pour un environnement intérieur contrôlé.

**Perspectives d'amélioration :**

**Court terme :**
- Ajout d'un système de notification (email, Telegram) lors de détections
- Implémentation d'une page web de consultation des captures avec galerie
- Ajout de statistiques avancées (graphiques de détections par heure/jour)
- Mécanisme de nettoyage automatique des anciennes captures

**Moyen terme :**
- Intégration de plusieurs caméras dans le système
- Détection par intelligence artificielle (YOLO, MobileNet) pour distinguer humains/animaux/objets
- Enregistrement vidéo en plus des captures photo
- Système de zones de détection personnalisables

**Long terme :**
- Application mobile pour consultation à distance
- Stockage cloud avec chiffrement
- Reconnaissance faciale pour identification des personnes autorisées
- Intégration avec systèmes domotiques (alarme, éclairage)

---

# **4. Annexes**

## **Annexe A : Structure du projet**

```
surveillance_camera/
├── code.py                 # Script principal
├── venv/                   # Environnement virtuel
├── README.md               # Documentation
└── /Volumes/recordings/    # Dossier partagé (montage SMB)
    └── mouvement_*.jpg     # Images capturées
```

## **Annexe B : Configuration système**

**MacBook Pro :**
- Système : macOS
- Python : 3.13.5
- Caméra : Index 1 (webcam interne)

**Raspberry Pi 5 :**
- RAM : 4 Go
- Stockage : 32 Go
- IP : `192.168.4.1`
- Partage : SMB sur `/var/www/recordings`
- MySQL : Port `3306`, base `presence` et table `enregistrement`

## **Annexe C : Paramètres de détection**

| Paramètre | Valeur | Justification |
|-----------|--------|---------------|
| THRESHOLD_VALUE | 30 | Équilibre sensibilité/faux positifs pour intérieur |
| MIN_AREA | 1000 | Filtre objets < 15 cm, cible visage/torse humain |
| BLUR_KERNEL | 11x11 | Suppression bruit webcam sans dégrader contours |
| MIN_TIME_BETWEEN_PHOTOS | 5 sec | Évite saturation stockage, capture 12 phases/minute |
| CAM_INDEX | 1 | Webcam interne MacBook (0 = iPhone) |

## **Annexe D : Format des fichiers générés**

**Nom de fichier :**
```
mouvement_YYYYMMDD-HHMMSS.jpg
```

**Exemples :**
```
mouvement_20251213-093042.jpg
mouvement_20251213-152318.jpg
```

**Propriétés JPEG :**
- Qualité : 95% (défaut OpenCV)
- Résolution : 1280x720 (webcam MacBook)
- Taille : 150-300 Ko selon complexité scène

## **Annexe E : Lien vers le code source**

* **Le code source est disponible sur GitHub : [lien du projet](https://github.com/axel-g-dev/Projet-surveillance)**

## **Annexe F : Captures d'écran**

*(Insérer captures d'écran de l'interface Streamlit : vue démarrage, vue en cours de surveillance, vue des statistiques)*

## **Annexe G : Photos de la réalisation**

*(Insérer photos du setup : MacBook avec webcam, connexion Raspberry Pi, exemples de captures de mouvement)*
doc.md
Affichage de doc.md en cours...