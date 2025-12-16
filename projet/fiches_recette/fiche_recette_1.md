# Fiche Recette 1

**Script [test_camera.py](https://github.com/axel-g-dev/Projet-surveillance/blob/main/prog_de_test/test_camera.py)
 (macOS / OpenCV)**

---

## Informations générales

* **Objet du test :** Script de surveillance par webcam avec détection de mouvement
* **Objectif :**

  * Valider l’initialisation de la caméra
  * Vérifier le mécanisme Start / Pause via la touche Entrée
  * Contrôler la détection de mouvement et l’enregistrement vidéo
* **Version / Build :** v1.0 – Premier jet
* **Environnement :**

  * Système : macOS
  * Bibliothèque : OpenCV (cv2)
  * Driver caméra : `cv2.CAP_AVFOUNDATION`
* **Référence du code :** Script Python audité (voir section Commentaires)

---

## 1. Protocole de test

|  ID | Démarche                                                                 | Comportement attendu                                                                                                                                            | Résultat |  Validation |
| :-: | :----------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------- | :---------: |
|  1  | **Lancement du script**<br>Exécuter la commande `python test_camera.py` | La fenêtre **"Surveillance"** s’ouvre. Le flux vidéo est visible. Le message **"PAUSE - Appuyez sur ENTREE"** apparaît à l’écran.                               |          | ☑ OK / ☐ KO |
|  2  | **Activation de la surveillance**<br>Appuyer sur la touche **Entrée**    | Le message de pause disparaît. La console affiche : `▶ Surveillance ACTIVE`.                                                                                    |          | ☑ OK / ☐ KO |
|  3  | **Détection de mouvement**<br>Effectuer un mouvement devant la caméra    | Des rectangles verts encadrent les zones en mouvement. Le message **"MOUVEMENT DETECTE"** apparaît en rouge.                                                    |          |☑ OK / ☐ KO |
|  4  | **Mise en pause**<br>Appuyer à nouveau sur **Entrée**                    | Le message **"PAUSE - Appuyez sur ENTREE"** réapparaît. La console affiche : `Surveillance EN PAUSE`. Aucun rectangle ne doit s’afficher malgré les mouvements. |          | ☑ OK / ☐ KO |
|  5  | **Arrêt du programme**<br>Appuyer sur **ESC**                            | La fenêtre vidéo se ferme correctement. Le script se termine sans erreur dans le terminal.                                                                      |          | ☑ OK / ☐ KO |
|  6  | **Vérification de l’enregistrement**<br>Consulter le dossier du script   | Le fichier **`surveillance.mp4`** est présent, lisible et correspond à la session enregistrée (vidéo accélérée due au framerate).                               |          | ☑ OK / ☐ KO |

---

## 2. Bilan de test

### Évaluation qualitative

| Critère                 | Conforme | Acceptable | Non conforme |
| :---------------------- | :------: | :--------: | :----------: |
| Fonctionnalités         |     ☑    |      ☐     |       ☐      |
| Conformité aux attentes |     ☑    |      ☐     |       ☐      |
| Ergonomie utilisateur   |     ☐    |      ☑     |       ☐      |
| Stabilité globale       |     ☐    |      ☑     |       ☐      |

### Décision finale

* ☐ **VALIDÉ** – Le script peut être utilisé tel quel
* ☑ **REFUSÉ** – Des corrections sont nécessaires avant validation

---

## 3. Remarques et anomalies

### Commentaires techniques

* L’image est inversée horizontalement (`cv2.flip(frame, 1)`) afin de corriger l’effet miroir sur macOS.

### Anomalies identifiées

| Priorité | Description de l’anomalie                                                                                        | ID Issue |
| :------: | :--------------------------------------------------------------------------------------------------------------- | :------: |
|   Haute  | Erreur possible lors de l’ouverture de la caméra si l’index est incorrect (0 vs 1)                              |          |
|  Moyenne | Sensibilité de détection trop élevée ou trop faible selon l’éclairage ; ajuster `threshold_value` et `min_area`. |          |


---

## 4. Recommandations d’amélioration

* Centraliser les paramètres caméra (index, FPS, seuils) dans une section de configuration.
* Ajouter un indicateur visuel de l’état (ACTIF / PAUSE) plus explicite à l’écran.
* Enregistrer également la vidéo en mode pause (optionnel, selon le besoin).
* Ajouter des logs horodatés pour faciliter le débogage.

---

**Test effectué par :** Louna, Axel
**Date :** 09 / 12 / 2025
