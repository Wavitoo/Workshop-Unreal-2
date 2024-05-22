# Workshop Unreal Partie 2

## Prérequis pour installer Unreal Engine 4.24.3 :

Vous devez installer le launcher Epic Games sur votre système. Vous pouvez le télécharger depuis le site officiel d'Epic Games : [Epic Games Launcher](https://store.epicgames.com/fr/download).

**Configuration minimale requise pour Unreal Engine 4.24.3 :**

- Système d'exploitation : Windows 7/8/10 64-bit
- Processeur : Quad-core Intel or AMD, 2.5 GHz ou plus rapide
- Mémoire vive (RAM) : 8 GB
- Carte graphique (obligatoire) : DirectX 11 compatible (NVIDIA GeForce GTX 470 ou AMD Radeon HD 6870 ou équivalent)
- Espace disque : 20 GB d'espace libre

## Introduction

Si vous n'avez pas réaliser la partie 1 du workshop je vous invite à aller jeter un oeil [ici](https://github.com/Wavitoo/Workshop-Unreal-1).
Dans ce workshop nous allons nous initier à la programmation en Blueprint principalement et pour les plus rapide d'entre vous en Bonus du C++.

## Programmation en Blueprint

Si vous n'avez pas créer de projet je vous invite à aller voir le workshop mentionné ci-dessus afin de voir comment créer un projet.
Si vous avez déjà un projet en template Third Person vous pouvez le lancer.

Nous allons voir comment est faite l'interface et la programmation de notre personnage.
Dans le Content browser aller dans le dossier ThirdPersonBP > Blueprint > ThirdPersonCharacter.
Ouvrez votre fichier qui contient votre personnage.

Vous trouverez l'interface global de tous les actors du jeu similaire à celle-ci:

![interface_actor](https://github.com/Wavitoo/Workshop-Unreal-1/assets/114447473/a3c69be1-9b34-4c53-95fa-651c17ec30fa)

Vous aurez 3 différentes window :

**- Viewport:**

Le viewport d'un Blueprint d'acteur est une fenêtre de l'éditeur où vous pouvez voir et interagir avec les composants qui composent l'acteur.

**- Construction Script:**

Le script de construction s'exécute après la liste des composants lorsqu'une instance d'une classe Blueprint est créée. Il contient un graphe de nodes qui est exécuté, permettant à l'instance de la classe Blueprint de réaliser des opérations d'initialisation.

**- Event Graph:**

L'Event Graph dans un Blueprint d'acteur est où vous définissez la logique de jeu qui s'exécute en temps réel pendant le jeu. C'est là que vous réagissez aux événements, contrôlez les animations, gèrez les interactions des joueurs, et bien plus encore. Voici quelques points clés sur l'Event Graph :

### Viewport

Lorsque vous cliqué sur la window Viewport vous pouvez voir voir personnage avec différents components :

![viewport](https://github.com/Wavitoo/Workshop-Unreal-1/assets/114447473/4e90c9d1-eb22-45d3-8248-beddf7c5c676)

Afin de voir précisément les components présents sur votre personnage, vous avez une window component situé en haut à gauche de l'interface :

![component](https://github.com/Wavitoo/Workshop-Unreal-1/assets/114447473/214b9dd9-872d-404d-92c7-59b0dc51ae13)

Comme vous pouvez le voir vous avez comme component :

**- Capsule Component:**

Le Capsule Component est utilisé comme la collision principale pour le personnage.
Il détermine la forme et la taille de la zone de collision autour du personnage, qui est généralement une capsule verticale.
Il sert principalement à détecter les collisions avec d'autres objets et déterminer les interactions physiques.

**- Arrow Component:**

Le Arrow Component est un composant de direction visuel qui indique l'orientation de l'acteur dans le monde.
Il sert de guide visuel pour l'orientation et le placement du personnage dans l'éditeur.

**- Mesh:**

Le Mesh Component est le composant qui contient le maillage squelettique ou statique du personnage, c'est-à-dire le modèle 3D visible.
Il représente visuellement le personnage dans le level.

**- Camera Boom:**
Le Camera Boom (également appelé Spring Arm Component) est un bras extensible qui maintient la caméra à une certaine distance du personnage.
Cela créer une distance ajustable entre la caméra et le personnage, tout en lissant les mouvements de la caméra.

**- Follow Camera:**

La Follow Camera est la caméra qui suit le personnage, attachée au Camera Boom.
Elle fournit la vue principale du jeu depuis laquelle le joueur voit et contrôle le personnage.

**- Character Movement:**

Le Character Movement Component est responsable de gérer la physique et les déplacements du personnage.
Il contrôle les mouvements du personnage, y compris la marche, la course, le saut, les interactions avec la gravité et les surfaces et d'autre.

### Event graph

Vous pouvez voir dans l'event graph vous avez déjà du code existant.
Le code existant est lié au mouvement du personnage avec le clavier, la VR et la manette.

Si vous faites un clique droit de l'event graph vous verrez une liste déroulante qui apparaîtra:

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/a851c04f-cbfc-4588-ba92-b40076a13cab)

Vous pouvez voir tous les nodes disponibles pour le blueprint.
Vous pouvez écrire directement le node que vous souhaitez chercher.

Il y aussi une cache qui peut coché ou décoché qui est le context sensitive.

**Qu'est-ce que c'est le context sensitive ?**

Le Contexte sensitive est un filtrage intelligent.
Lorsque Context Sensitive est activé, l'éditeur de Blueprints filtre automatiquement les nodes disponibles en fonction du contexte actuel, c'est-à-dire ce qui est pertinent et utilisable à partir de la situation ou du type de node que vous utilisez.
En revanche, si vous le désactivez vous aurez juste une liste de tous les nodes disponibles.

Maintenant on va voir le node basique qui sera présent sur presque tout nos actors.

![begin_play](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/edd4400b-91d6-4e0f-8455-28b8e4573194)

Le node Event Begin Play dans Unreal Engine est un élément essentiel des Blueprints, utilisé pour initier des actions ou des scripts lorsque le jeu commence ou lorsqu'un acteur (un objet dans le jeu, tel qu'un personnage ou un objet interactif) est créé (spawné).

**- Fonctionnalité:**
Déclenchement initial : Ce node est activé automatiquement au début de la partie, immédiatement après le chargement de la scène et l'initialisation de tous les objets dans le jeu.
Usage commun : Utilisé pour configurer des éléments initiaux tels que les variables, les états des objets, les animations de démarrage, la génération d'autres objets ou tout autre logique qui doit être exécutée au début de la partie.

**- Emplacement:**
Blueprints : Il est disponible dans tous les types de Blueprints, y compris les Blueprints d'acteurs, les Blueprints de niveau, les Blueprints de composants, etc.

**- Caractéristiques:**
Pas d'entrées : Il faut savoir que ce node ne prend pas d'entrées car il est déclenché automatiquement.
Sortie unique : Il dispose d'une seule broche de sortie (exec), que vous connectez à d'autres nodes pour exécuter des actions au début du jeu.

Sur le côté gauche de l'interface vous trouverz  une window My Blueprint :

![variables_functions](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/889c3844-e6c0-4a0f-8c35-db2aaf656786)

Dans cette window se trouvera principalement les fonctions que vous voulez créer (qu'elle soit override ou créer par vous).
Les variables, les macros ou même les Interfaces si vous en implémenter pour faire un système d'intéraction par exemple.

Lorsque vous cliquez sur une variable dans la section variables, vous pouvez choisir son type :

![liste_variable](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/02907503-9b75-4708-9976-16128ba68842)

Vous pouvez assigner un certain nombre de type sur une variable comme par exemple un énumération ou même un acteur en référence d'objet ou même en class.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/861654da-267f-42e8-b733-50ca487fb026)

Vous pouvez aussi changer une variable simple à une variable en tableau ou même une map (appellé dictionnary).
Juste à droite du type de variable vous avez une petit icône c'est en cliquant dessus que vous pouvez le changer. 

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/1f05a2bc-8fdf-4262-8604-75e1a43e4fbe)



## Contact
Si vous avez des questions ou besoin d'informations, veuillez me contacter à arslan.tetu@epitech.eu