# Fiche Recette 5

**Script [code.py](https://github.com/axel-g-dev/Projet-surveillance/blob/main/code.py)
(macOS / OpenCV / Streamlit / MySQL)**

---

## Informations générales

* **Objet du test :** Interface Web de Surveillance Vidéo avec détection de mouvement
* **Objectif :**

  * Valider l’affichage de l’interface graphique Streamlit dans un navigateur
  * Tester les boutons interactifs (Démarrer / Arrêter)
  * Vérifier la détection de mouvement par OpenCV
  * Valider l’enregistrement des captures et des événements en base de données
  * Vérifier la limitation volontaire des captures pour réduire la charge système
* **Version / Build :** v5.0 – Version finale
* **Environnement :**

  * Système : macOS (tests) / Raspberry Pi (cible)
  * Bibliothèques : `streamlit`, `opencv-python`, `numpy`, `mysql-connector-python`
  * Caméra : USB / intégrée via `cv2.VideoCapture`
* **Référence du code / dépôt :** Script unique `code.py`

---

## 1. Protocole de test

|  ID | Démarche                                                                              | Comportement attendu                                                                                                            | Résultat                                           | Validation |
| :-: | :------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------- | :--------: |
|  1  | **Lancement du serveur Web**<br>Exécuter : `streamlit run code.py`                    | Le terminal affiche une URL locale (ex : `http://localhost:8501`) et la page s’ouvre dans le navigateur.                        | La page Streamlit se lance correctement.           |    ☑ OK    |
|  2  | **Vérification de l’interface**<br>Observer la page web chargée.                      | Le titre de l’application est visible. La sidebar affiche les boutons **Démarrer** et **Arrêter** ainsi que les statistiques.   | Interface conforme, lisible et stable.             |    ☑ OK    |
|  3  | **Action Démarrer**<br>Cliquer sur le bouton "Démarrer".                              | La caméra s’initialise, le statut passe à **En cours** et le flux vidéo démarre.                                                | Caméra activée, flux vidéo visible.                |    ☑ OK    |
|  4  | **Vérification du flux vidéo**<br>Observer l’image affichée.                          | Le flux vidéo se rafraîchit de manière continue dans l’interface.                                                               | Flux fluide et mis à jour en temps réel.           |    ☑ OK    |
|  5  | **Détection de mouvement**<br>Provoquer un déplacement devant la caméra.              | Les zones de mouvement sont détectées et encadrées.                                                                             | Détection cohérente, sans faux positifs excessifs. |    ☑ OK    |
|  6  | **Capture automatique**<br>Maintenir un mouvement devant la caméra.                   | Une image est enregistrée uniquement si un mouvement est détecté, avec un intervalle minimum de 5 secondes entre deux captures. | Captures espacées, limitation respectée.           |    ☑ OK    |
|  7  | **Enregistrement en base de données**<br>Consulter la base MySQL après une détection. | Une entrée est ajoutée dans la table avec le type d’événement et le chemin du fichier image.                                    | Insertion confirmée sans erreur.                   |    ☑ OK    |
|  8  | **Statistiques temps réel**<br>Observer les compteurs.                                | Les compteurs de détections, de captures et la durée s’actualisent en temps réel.                                               | Statistiques correctes et cohérentes.              |    ☑ OK    |
|  9  | **Action Arrêter**<br>Cliquer sur le bouton "Arrêter".                                | Le flux vidéo s’arrête et la caméra est libérée.                                                                                | Arrêt propre sans crash.                           |    ☑ OK    |
|  10 | **Gestion des erreurs**<br>Observer le terminal pendant l’exécution.                  | Aucune erreur critique ou traceback bloquant.                                                                                   | Aucune anomalie détectée.                          |    ☑ OK    |

---

## 2. Bilan de test

### Évaluation qualitative

| Critère                     | Conforme | Acceptable | Non conforme |
| :-------------------------- | :------: | :--------: | :----------: |
| Fonctionnalités             |     ☑    |      ☐     |       ☐      |
| Conformité aux attentes     |     ☑    |      ☐     |       ☐      |
| Ergonomie utilisateur       |     ☑    |      ☐     |       ☐      |
| Stabilité globale           |     ☑    |      ☐     |       ☐      |
| Intégration base de données |     ☑    |      ☐     |       ☐      |
| Performance système         |     ☑    |      ☐     |       ☐      |

### Décision finale

* ☑ **VALIDÉ**
* ☐ **REFUSÉ**

---

## 3. Remarques et anomalies

### Commentaires techniques

> La version v5.0 respecte le cycle d’exécution de Streamlit grâce à l’utilisation de `st.session_state` et de zones dynamiques (`st.empty()`).
> La détection de mouvement est réalisée via OpenCV et les captures sont volontairement limitées à une image toutes les 5 secondes afin d’éviter une surcharge CPU, disque et base de données, notamment sur Raspberry Pi.
> Le lien avec la base de données MySQL est opérationnel : chaque capture génère une entrée persistante avec le type d’événement et le chemin du fichier.

### Anomalies identifiées

| Priorité | Description de l’anomalie                           | ID Issue |
| :------: | :-------------------------------------------------- | :------: |
|   Basse  | Aucune anomalie bloquante constatée lors des tests. |    00    |

---

**Test effectué par :** Louna et Axel

**Date :** 09 / 12 / 2025

