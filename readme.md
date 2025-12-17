# Système de Vidéosurveillance par Détection de Mouvement

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-Python-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![MySQL Connector](https://img.shields.io/badge/MySQL%20Connector-Python-4479A1?style=for-the-badge&logo=mysql&logoColor=white)

![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white)
![Raspberry Pi](https://img.shields.io/badge/Raspberry%20Pi-A22846?style=for-the-badge&logo=raspberrypi&logoColor=white)
![macOS](https://img.shields.io/badge/macOS-MacBook-000000?style=for-the-badge&logo=apple&logoColor=white)

---

## Objectif du projet

Ce projet est un système de vidéosurveillance temps réel basé sur la détection de mouvement.

Un ordinateur portable (MacBook) analyse le flux vidéo via OpenCV, détecte les mouvements, capture automatiquement des images, puis :
- stocke les images dans un dossier partagé SMB
- enregistre les métadonnées dans une base de données MySQL hébergée sur un Raspberry Pi 5
- permet un suivi en temps réel via une interface web Streamlit

Projet réalisé dans le cadre du Mini-Projet CIEL2 – Année scolaire 2025–2026.

---

## Fonctionnalités principales

- Détection de mouvement par différence d’images
- Capture automatique d’images horodatées
- Limitation volontaire du nombre de captures
- Stockage centralisé sur serveur distant
- Enregistrement des événements en base de données
- Interface web de supervision en temps réel

---

## Structure du projet

```txt
SURVEILLANCE_CAMERA/
├── __pycache__/
│   └── code.cpython-313.pyc
│
├── .venv/                  # Environnement virtuel Python
├── venv/                   # (ancien environnement, non utilisé)
│
├── bdd_sql/
│   └── bdd.sql              # Script SQL de création de la base
│
├── env/                     # Variables d’environnement (si utilisées)
│
├── prog_de_test/            # Scripts de tests et prototypes
│   ├── older_codes/         # Anciennes versions / essais
│   ├── code_photo.py        # Capture automatique de photos
│   ├── code_sans_bdd.py     # Version Streamlit sans base de données
│   ├── page_web.py          # Prototype interface web Streamlit
│   └── test_camera.py       # Test basique de la caméra
│
├── projet/                  # Documentation du mini-projet
│   ├── fiches_recette/      # Fiches de tests et validations
│   │   ├── fiche_recette_1.md
│   │   ├── fiche_recette_2.md
│   │   ├── fiche_recette_3.md
│   │   ├── fiche_recette_4.md
│   │   ├── fiche_recette_5.md
│   │   └── fiche_recette_modele.md
│   │
│   ├── images/              # Schémas et captures d’écran
│   │   ├── bdd.png
│   │   ├── detection_page_web.png
│   │   ├── dossier_recordings_partage.png
│   │   ├── page_web.png
│   │   ├── smb.png
│   │   └── SysML.png
│   │
│   ├── diagrammes.md        # Diagrammes (SysML, séquence, classe)
│   └── documentation.md    # Documentation complète du projet
│
├── .gitignore
├── a_faire.md               # Liste des tâches restantes
├── a_rendre.md              # Éléments à rendre
├── code.py                  # Script principal (version finale)
└── README.md                # Présentation du projet

````

---

## Lancement rapide

### Préparation de l’environnement

```bash
python3 -m venv venv
source venv/bin/activate
```

### Installation des dépendances

```bash
pip install streamlit opencv-python numpy mysql-connector-python
```

### Démarrage de l’application

```bash
streamlit run code.py
```

Interface accessible via l’adresse locale :

```
http://localhost:8501
```

---

## Architecture générale

* Poste client : MacBook avec webcam
* Serveur central : Raspberry Pi 5

  * Base de données MySQL (base `presence`)
  * Dossier partagé SMB (`recordings`)
* Interface utilisateur : Streamlit via navigateur web

---

## Documentation détaillée

La documentation complète du projet est disponible dans le dossier `projet/` :

* Documentation générale : `projet/documentation.md`
* Fiches de recette et tests : `projet/fiches_recette/`
* Diagrammes techniques : `projet/diagrammes.md`
* Captures d’écran : `projet/images/`

---

## Auteurs

* Louna D.
* Axel G.

Classe CIEL2 – Année scolaire 2025–2026
Enseignant référent : M. Boudjelaba

## État du projet

Version finale fonctionnelle et validée (v5.0)

