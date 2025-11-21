# README du Projet : Simulation de Ferme Top-Down 

Ce projet est une simulation de ferme vue de dessus (Top-Down) développée avec Unity (2D), intégrant un système d'IA animale et une gestion du temps.

---

## Configuration Requise

* **Moteur de Jeu :** Unity (Version 2021 LTS ou plus récente recommandée).
* **Langage de Scripting :** C#.
* **Architecture :** Utilisation des composants standard de Unity (Rigidbody2D, Animator, etc.).

---

## Fonctionnalités Implémentées

Le système de jeu de base et l'environnement sont entièrement fonctionnels.

### 1. Système de Temps et Cycle Jour/Nuit

* **Cycle Temporel :** Implémentation d'une horloge interne simple permettant l'alternance entre l'état **Jour** et l'état **Nuit**.
* **Synchronisation :** Le système fournit un indicateur (`IsNightTime`) pour synchroniser tous les comportements basés sur le temps (ex. : sommeil des animaux).

### 2. Animale Générique (`AnimalBehavior.cs`)

Le script `AnimalBehavior.cs` est **modulaire** et **réutilisable** pour toutes les espèces d'animaux (Poulet, Vache, etc.).

* **États d'Activité :** Les animaux alternent entre les états **Wandering** (Errance) et **Sleeping** (Sommeil).
* **Errance (Wandering) :** Mouvement aléatoire constant dans un rayon défini autour de leur position de départ.
* **Sommeil (Sleeping) :** Arrêt total du mouvement la nuit, déclenché par le cycle Jour/Nuit.
* **Audio et Animation :**
    * Lecture de sons spécifiques à intervalles aléatoires.
    * Pilotage de l'animation (`Idle`, `Walk`) via les paramètres booléens **`IsMoving`** et **`IsSleeping`**.
    * Rotation horizontale du sprite pour faire face à la direction du mouvement.
* **Fixes Critiques :** Résolution des problèmes de flux d'Animator et de seuil de vélocité pour garantir une animation fluide.

### 3. Contrôle de la Caméra (`CameraController.cs`)

* **Zoom Dynamique :** Utilisation de la molette de la souris pour zoomer avant/arrière, avec des limites de zoom (`minZoom`, `maxZoom`).
* **Panning (Déplacement) :** Déplacement de la caméra en cliquant et faisant glisser avec le bouton droit de la souris.
* **Limites de Carte :** Implémentation optionnelle de limites pour restreindre le mouvement de la caméra aux bornes de la carte.

### 4. Architecture de Projet

* **Prefabs :** Tous les animaux sont gérés en tant que **Prefabs** (modèles réutilisables).
* **Contrôleurs d'Animator :** Chaque espèce utilise son propre `Animator Controller` mais partage les mêmes paramètres booléens.

---

## Comment Faire Marcher la Simulation

Pour exécuter la simulation dans Unity :

1. **Ouvrir le projet :**  
   * Lancez Unity Hub.  
   * Cliquez sur **Add** et sélectionnez le dossier du projet.  
   * Ouvrez-le avec Unity **2021 LTS ou supérieur**.

2. **Charger la scène principale :**  
   * Rendez-vous dans le dossier `Assets/Scenes/`.  
   * Ouvrez la scène principale (par exemple `Ferme verte.unity`).

3. **Vérifier les éléments essentiels dans la scène :**  
   * La caméra doit contenir le script `CameraController.cs`.  
   * Les animaux doivent être présents dans la scène avec le script `AnimalBehavior.cs`.  
   * Le système de temps (cycle jour/nuit) doit être dans la hiérarchie.

4. **Lancer la simulation :**  
   * Appuyez sur le bouton **Play** dans Unity.  
   * Les animaux se déplaceront automatiquement et dormiront durant la nuit.  
   * Le zoom et le déplacement de la caméra fonctionneront immédiatement.

5. **Arrêter la simulation :**  
   * Cliquez de nouveau sur **Play** pour revenir au mode édition.

---

## Mise en Route (Quick Start)

Pour ajouter un nouvel animal fonctionnel à la scène :

1. **Préparation du Sprite :** Importez le sprite de l'animal et assurez-vous qu'il est découpé (`Sliced`).
2. **Création du GameObject :** Créez un nouvel objet avec les composants **Sprite Renderer**, **Rigidbody 2D** (Gravity Scale = 0), **Collider 2D**, **Audio Source** et le script **`AnimalBehavior.cs`**.
3. **Configuration de l'Animator :**
    * Créez un nouveau **Animator Controller**.
    * Créez les paramètres booléens **`IsMoving`** et **`IsSleeping`**.
    * Créez les clips d'animation (`_Idle`, `_Walk`) et configurez les transitions : `Entry` doit pointer vers l'état `Idle`.
4. **Création du Prefab :** Faites glisser l'animal de la hiérarchie vers le dossier `Prefabs`.
