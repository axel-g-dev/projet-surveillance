# Fiche Recette 4

**Script [code_sans_bdd.py](https://github.com/axel-g-dev/Projet-surveillance/blob/main/prog_de_test/code_sans_bdd.py)
 (macOS / OpenCV)**

---

## Informations générales

* **Objet du test :** Application de surveillance par webcam avec détection de mouvement et capture d’images
* **Objectif :**

  * Valider l’initialisation de la caméra via Streamlit
  * Vérifier le contrôle **Démarrer / Arrêter**
  * Contrôler la détection de mouvement en temps réel
  * Vérifier la sauvegarde automatique d’images lors d’un mouvement
  * Vérifier l’affichage des statistiques
* **Version / Build :** **v4.0 – Version Streamlit modulaire**
* **Environnement :**

  * Système : macOS
  * Bibliothèques : OpenCV (cv2), Streamlit, NumPy
  * Driver caméra : `cv2.CAP_AVFOUNDATION`
* **Référence du code :** Script Python audité (SurveillanceManager + interface Streamlit)

---

## 1. Protocole de test

|  ID | Démarche                                                                               | Comportement attendu                                                                                                                                | Résultat |  Validation |
| :-: | :------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------- | :------- | :---------: |
|  1  | **Lancement de l’application**<br>Commande : `streamlit run surveillance_streamlit.py` | L’interface Streamlit s’ouvre dans le navigateur. L’état est **Inactif**. Le message *“Cliquez sur Démarrer pour lancer la surveillance”* apparaît. |          | ☑ OK / ☐ KO |
|  2  | **Démarrage de la surveillance**<br>Clique sur **Démarrer**                            | La caméra s’initialise. Le statut passe à **En cours**. Le flux vidéo apparaît. La console affiche les logs `[CAMERA] OK`.                          |          | ☑ OK / ☐ KO |
|  3  | **Détection de mouvement**<br>Effectuer un mouvement devant la caméra                  | Des rectangles verts entourent les zones en mouvement. Un point vert apparaît en haut à gauche de l’image. Le compteur **Détections** augmente.     |          | ☑ OK / ☐ KO |
|  4  | **Capture automatique**<br>Maintenir un mouvement                                      | Une image est sauvegardée toutes les X secondes (selon `MIN_TIME_BETWEEN_PHOTOS`). Le compteur **Captures** augmente.                               |          | ☑ OK / ☐ KO |
|  5  | **Arrêt de la surveillance**<br>Clique sur **Arrêter**                                 | Le flux vidéo s’arrête. Le statut passe à **Inactif**. Les statistiques restent affichées.                                                          |          | ☑ OK / ☐ KO |
|  6  | **Vérification des fichiers**<br>Ouvrir le dossier de sauvegarde                       | Les fichiers `mouvement_YYYYMMDD-HHMMSS.jpg` sont présents et lisibles. Les images correspondent aux mouvements détectés.                           |          | ☑ OK / ☐ KO |

---

## 2. Bilan de test

### Évaluation qualitative

| Critère                 | Conforme | Acceptable | Non conforme |
| :---------------------- | :------: | :--------: | :----------: |
| Fonctionnalités         |     ☑    |      ☐     |       ☐      |
| Conformité aux attentes |     ☑    |      ☐     |       ☐      |
| Ergonomie utilisateur   |     ☑    |      ☐     |       ☐      |
| Stabilité globale       |     ☐    |      ☑     |       ☐      |

### Décision finale

* ☐ **VALIDÉ** – Le script peut être utilisé tel quel
* ☑ **REFUSÉ** – Il n'y a pas de lien, ni d'envoi à la BDD

---

## 3. Remarques et anomalies

### Anomalies identifiées

| Priorité | Description de l’anomalie                                                        | ID Issue |
| :------: | :------------------------------------------------------------------------------- | :------: |
|   Haute  | Envoi impossible à la base de données pour l'envoi de données (métadonnées)      |    01    |
---

## 4. Recommandations d’amélioration

> Faire un lien avec la base de données 

---

**Test effectué par :** Louna, Axel
**Date :** 09 / 12 / 2025

