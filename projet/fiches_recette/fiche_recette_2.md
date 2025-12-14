# Fiche Recette 2

**Script [code_photo.py](https://github.com/axel-g-dev/Projet-surveillance/blob/main/prog_de_test/code_photo.py)
 (macOS / OpenCV)**

-----

## Informations générales

  * **Objet du test :** Script de surveillance continue avec capture automatique de photos
  * **Objectif :**
      * Valider la création automatique du dossier de sauvegarde
      * Vérifier la détection de mouvement sans action utilisateur (démarrage immédiat)
      * Contrôler la sauvegarde des fichiers images (.jpg)
      * **Confirmer l'anomalie d'écrasement des fichiers (doublons de seconde)**
  * **Version / Build :** v2.0 – Surveillance Photo
  * **Environnement :**
      * Système : macOS
      * Bibliothèque : OpenCV (cv2)
      * Driver caméra : `cv2.CAP_AVFOUNDATION`
  * **Référence du code :** Script Python d'enregistrement photo (voir section Commentaires)

-----

## 1\. Protocole de test

|  ID | Démarche                                                                                                 | Comportement attendu                                                                                                                                                                          | Résultat |  Validation |
| :-: | :------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------- | :---------: |
|  1  | **Vérification pré-lancement**<br>Vérifier que le dossier défini dans `SAVE_FOLDER` n'existe pas encore. | Le script doit avoir les droits d'écriture.                                        |          | ☑ OK / ☐ KO |
|  2  | **Lancement du script**<br>Exécuter la commande `python surveillance_photos.py`                          | La fenêtre **"Surveillance"** s’ouvre immédiatement. Le flux vidéo est visible. La console affiche : `Camera initialisée avec succès`. Le dossier de sauvegarde est créé automatiquement.     |          | ☑ OK / ☐ KO |
|  3  | **Détection de mouvement**<br>Effectuer un mouvement devant la caméra.                                   | Des rectangles verts encadrent le mouvement. Le texte **"mouvement"** apparaît. La console affiche en temps réel : `Photo sauvegardée : .../mouvement_YYYYMMDD-HHMMSS.jpg`.                   |          | ☑ OK / ☐ KO |
|  4  | **Test de saturation (Bug suspecté)**<br>Bouger continuellement pendant 3 secondes.                      | Le script tente de sauvegarder plusieurs images par seconde. **Vérifier dans le dossier :** Est-ce que toutes les images sont là, ou seulement une par seconde ? (Risque d'écrasement).       |          | ☑ OK / ☐ KO |
|  5  | **Arrêt du programme**<br>Appuyer sur la touche **ESC**.                                                 | La fenêtre se ferme. Le script s'arrête proprement avec le message `Arrêt demandé` dans la console.                                                                                           |          | ☑ OK / ☐ KO |
|  6  | **Vérification des fichiers**<br>Ouvrir le dossier de sauvegarde.                                        | Les fichiers `.jpg` sont lisibles. **Attention :** Vérifier si le nombre de fichiers correspond au nombre de logs "Photo sauvegardée" dans la console (Anomalie attendue).                    |          | ☐ OK / ☑ KO |

-----

## 2\. Bilan de test

### Évaluation qualitative

| Critère                 | Conforme | Acceptable | Non conforme |
| :---------------------- | :------: | :--------: | :----------: |
| Fonctionnalités         |    ☐     |     ☑      |      ☐       |
| Conformité aux attentes |    ☐     |     ☐      |      ☑       |
| Ergonomie utilisateur   |    ☐     |     ☐      |      ☑       |
| Stabilité globale       |    ☑     |     ☐      |      ☐       |

### Décision finale

  * ☐ **VALIDÉ** – Le script peut être utilisé tel quel
  * ☑ **REFUSÉ** – Des corrections sont nécessaires avant validation (Voir section 3)

-----

## 3\. Remarques et anomalies

### Commentaires techniques

  * **Absence d'interface :** Contrairement au premier script, celui-ci démarre la surveillance immédiatement sans attendre de confirmation (pas de mode "Pause").
  * **Chemin en dur :** La variable `SAVE_FOLDER = "/Users/axel/..."` empêchera le script de fonctionner sur un autre ordinateur sans modification manuelle du code, pas de renvoi vers la Base de Données.

### Anomalies identifiées

| Priorité | Description de l’anomalie                                                                                                                                                                                           | ID Issue |
| :------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :------: |
| **Critique** | **Perte de données / Écrasement :** Le nommage des fichiers (`%H%M%S`) n'a qu'une précision à la seconde. Si le script capture 10 images dans la même seconde, seule la dernière est conservée (les 9 autres sont écrasées). |    \#01   |
|  Moyenne | **Absence de contrôle :** L'utilisateur ne peut pas mettre en pause la surveillance pour régler sa caméra sans remplir son disque dur de photos inutiles.                                                             |    \#02   |
|  Faible  | **Portabilité :** Le chemin du dossier de sauvegarde est absolu et spécifique à un utilisateur. Utiliser un chemin relatif ou `os.path.expanduser("~")`.                                                              |    \#03   |

-----

## 4\. Recommandations d’amélioration

  * **Correction priorité 1 :** Ajouter un délai pour sauvegarder les photos et optimiser le stockage
  * **Interface :** Réintégrer la logique de "Start/Pause" avec la touche Entrée pour éviter de capturer l'utilisateur en train de s'installer.

-----

**Test effectué par :** Louna et Axel

**Date :** 202\_ / \_\_ / \_\_