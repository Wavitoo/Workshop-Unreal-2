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

- Viewport: 

Le viewport d'un Blueprint d'acteur est une fenêtre de l'éditeur où vous pouvez voir et interagir avec les composants qui composent l'acteur.

- Construction Script :

Le script de construction s'exécute après la liste des composants lorsqu'une instance d'une classe Blueprint est créée. Il contient un graphe de nœuds qui est exécuté, permettant à l'instance de la classe Blueprint de réaliser des opérations d'initialisation.

- Event Graph :

L'Event Graph dans un Blueprint d'acteur est où vous définissez la logique de jeu qui s'exécute en temps réel pendant le jeu. C'est là que vous réagissez aux événements, contrôlez les animations, gèrez les interactions des joueurs, et bien plus encore. Voici quelques points clés sur l'Event Graph :

### Viewport

Lorsque vous cliqué sur la window Viewport vous pouvez voir voir personnage avec différents components :

![viewport](https://github.com/Wavitoo/Workshop-Unreal-1/assets/114447473/4e90c9d1-eb22-45d3-8248-beddf7c5c676)

Afin de voir précisément les components présents sur votre personnage, vous avez une window component situé en haut à gauche de l'interface :

![component](https://github.com/Wavitoo/Workshop-Unreal-1/assets/114447473/214b9dd9-872d-404d-92c7-59b0dc51ae13)

Comme vous pouvez le voir vous avez comme component :

- Capsule Component :

Le Capsule Component est utilisé comme la collision principale pour le personnage.
Il détermine la forme et la taille de la zone de collision autour du personnage, qui est généralement une capsule verticale.
Il sert principalement à détecter les collisions avec d'autres objets et déterminer les interactions physiques.

- Arrow Component :

Le Arrow Component est un composant de direction visuel qui indique l'orientation de l'acteur dans le monde.
Il sert de guide visuel pour l'orientation et le placement du personnage dans l'éditeur.

- Mesh :

Le Mesh Component est le composant qui contient le maillage squelettique ou statique du personnage, c'est-à-dire le modèle 3D visible.
Il représente visuellement le personnage dans le level.

- Camera Boom:
Le Camera Boom (également appelé Spring Arm Component) est un bras extensible qui maintient la caméra à une certaine distance du personnage.
Cela créer une distance ajustable entre la caméra et le personnage, tout en lissant les mouvements de la caméra.

- Follow Camera :

La Follow Camera est la caméra qui suit le personnage, attachée au Camera Boom.
Elle fournit la vue principale du jeu depuis laquelle le joueur voit et contrôle le personnage.

- Character Movement :

Le Character Movement Component est responsable de gérer la physique et les déplacements du personnage.
Il contrôle les mouvements du personnage, y compris la marche, la course, le saut, les interactions avec la gravité et les surfaces et d'autre.

### Event graph

## Contact
Si vous avez des questions ou besoin d'informations, veuillez me contacter à arslan.tetu@epitech.eu