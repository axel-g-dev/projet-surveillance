# Fiche Recette 3

**Script [page_web.py](https://github.com/axel-g-dev/Projet-surveillance/blob/main/prog_de_test/page_web.py)
 (macOS / OpenCV)**

-----

## Informations générales

  * **Objet du test :** Interface Web de Surveillance (POC Streamlit)
  * **Objectif :**
      * Valider l'affichage de l'interface graphique dans le navigateur
      * Tester les boutons interactifs (Démarrer / Arrêter)
      * Comprendre le cycle d'exécution de Streamlit vs boucle infinie Python
  * **Version / Build :** v3.0 – Intégration Web (Streamlit)
  * **Environnement :**
      * Système : macOS
      * Bibliothèque : `streamlit`, `opencv-python`
      * Driver caméra : `cv2.CAP_AVFOUNDATION`
  * **Référence du code / dépôt :** Script `page_web.py` appelant le module `code.py`

-----

## 1\. Protocole de test

|  ID | Démarche | Comportement attendu | Résultat |  Validation |
| :-: | :------- | :------------------- | :------- | :---------: |
|  1  | **Lancement du serveur Web**<br>Exécuter : `streamlit run page_web.py` | Le terminal affiche une URL (ex: `http://localhost:8501`). Une page web s'ouvre automatiquement dans le navigateur. | | ☑ OK / ☐ KO |
|  2  | **Vérification de l'interface**<br>Observer la page web chargée. | Le titre **"Surveillance vidéo"** est visible. Deux boutons **"Démarrer"** et **"Arrêter"** sont présents. | | ☑ OK / ☐ KO |
|  3  | **Action Démarrer**<br>Cliquer sur le bouton "Démarrer". | La variable `run` passe à `True`. La caméra s'initialise (la LED verte du Mac s'allume). | | ☑ OK / ☐ KO |
|  4  | **Vérification du flux vidéo**<br>Observer l'espace sous les boutons. | **Comportement actuel connu :** Une image s'affiche mais reste figée ou ne se rafraîchit pas en temps réel. Le flux n'est pas fluide. | | ☐ OK / ☑ KO |
|  5  | **Action Arrêter**<br>Cliquer sur le bouton "Arrêter". | La variable `run` passe à `False`. La tentative de lecture s'arrête. | | ☑ OK / ☐ KO |
|  6  | **Gestion des erreurs**<br>Vérifier le terminal pendant l'exécution. | Pas de "Traceback" ou d'erreur critique faisant crasher le serveur Streamlit. | | ☑ OK / ☐ KO |

-----

## 2\. Bilan de test

### Évaluation qualitative

| Critère                 | Conforme | Acceptable | Non conforme |
| :---------------------- | :------: | :--------: | :----------: |
| Fonctionnalités         |    ☐     |     ☐      |      ☑       |
| Conformité aux attentes |    ☐     |     ☑      |      ☐       |
| Ergonomie utilisateur   |    ☑     |     ☐      |      ☐       |
| Stabilité globale       |    ☐     |     ☑      |      ☐       |

> *Note : "Conformité aux attentes" est noté Acceptable car l'objectif était pédagogique (comprendre Streamlit) et non fonctionnel (avoir une vidéo fluide).*

### Décision finale

  * ☐ **VALIDÉ**
  * ☑ **REFUSÉ** (Le script nécessite une refonte de la boucle pour fonctionner avec Streamlit)

-----

## 3\. Remarques et anomalies

### Commentaires techniques

> Streamlit exécute le script de haut en bas à chaque interaction. Une boucle `while True` classique à l'intérieur d'un script Streamlit bloque souvent le rafraîchissement de l'interface (les boutons deviennent inactifs) ou ne rafraîchit l'image qu'une seule fois.

### Anomalies identifiées

| Priorité | Description de l’anomalie | ID Issue |
| :------: | :------------------------ | :------: |
| **Haute**| **Absence de rafraîchissement vidéo :** Le script affiche une image unique ou fige le navigateur car il manque une commande de rechargement (`st.rerun()`) ou une boucle gérée spécifiquement pour le web. | 01 |
| Moyenne  | **Persistance de la caméra :** Si on recharge la page, la caméra peut rester "occupée" par l'instance précédente si elle n'est pas libérée correctement. | 02 |

-----

**Test effectué par :** Louna et Axel

**Date :** 202\_ / \_\_ / \_\_