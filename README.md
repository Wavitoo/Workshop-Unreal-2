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

Pour que ça soit plus à l'aise pour vous afin de tester les différents système que l'on va aborder.
Vous pouvez changer les input du personnage car pour le moment elles sont en W, A, S, D.
Allez dans Edit tout en haut à gauche de votre Unreal > Project Settings > Input dans la catégorie Engine > Axis Mappings.
Changer le MoveForward et le MoveRight.
Soit vous ajouter directement la touche ou vous changer celle existante.
Attention, si vous ajouter une touche spécialement pour le MoveRight si vous mettez la touche Q vérifiez bien que le scale soit négatif avec la valeur -1.0

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

Sur le côté gauche de l'interface vous trouverz  une window My Blueprint :

![variables_functions](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/889c3844-e6c0-4a0f-8c35-db2aaf656786)

Dans cette window se trouvera principalement les fonctions que vous voulez créer (qu'elle soit override ou créer par vous).
Les variables, les macros ou même les Interfaces si vous en implémenter pour faire un système d'intéraction par exemple.

Lorsque vous cliquez sur une variable dans la section variables, vous pouvez choisir son type.
Vous pouvez assigner un certain nombre de type sur une variable comme par exemple un énumération ou même un acteur en référence d'objet ou même en class.
Nous verrons plus tard plus profondément.

![liste_variable](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/02907503-9b75-4708-9976-16128ba68842)

Vous pouvez aussi changer une variable simple à une variable en tableau ou même une map (appellé dictionnary).
Juste à droite du type de variable vous avez une petit icône c'est en cliquant dessus que vous pouvez le changer. 

![single_array](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/1f05a2bc-8fdf-4262-8604-75e1a43e4fbe)

Lorsque vous cliquez sur une varible vous aurez une window Detail en haut à droite qui va apparaître où vous pourrez choisir le nom de votre variable,
votre type de variable comme vu au-dessus, sa value et d'autre option qu'on pourra voir plus tard.

![detail_global](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/861654da-267f-42e8-b733-50ca487fb026)

Comme vous le savez dans l'event graph il y a déjà du code implémenté de base qui est lié aux mouvements du personnage (VR, controller et clavier).
Il y a un "code de couleur" pour les différents nodes existants dans l'event graph actuel :

**- Nodes d'events (Rouge):**
Utilisés pour déclencher des actions lorsque certains événements se produisent. Par exemple, "Event Begin Play" pour lorsqu'on lance le jeu.

**- Nodes de fonctions (Bleu):**
Représentent des appels de fonctions, qui peuvent être soit des fonctions intégrées d'Unreal Engine, soit des fonctions définies par l'utilisateur.

Bien sûr il y en a d'autre comme les nodes de flow control pour les conditions etc...

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

Il est temps maintenant de toucher au visual scripting.

## Exercice 1

Vous allez créer 2 variables de types Float qui se nommeront : CurrentHealth et MaxHealth.
Pour créer une variable vous avez un + dans le panel des variables :

![new_var](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/37648e7e-118c-4a72-b67d-410a6273bc64)

Pour set la valeur des variables compilez votre programme et modifier la valeur directement dans le detail situé à droite dans Default value.

Ensuite vous allez créer une fonction nommé : SubstractHealth.
Pour créer une fonction vous avez un + dans le panel des fonctions :

![new_func](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/38d6877d-3561-4cd6-badc-23cb53df5c86)

Dès que vous avez créer la fonction vous la retrouverez dans le panel des Fonctions.
Si la fonction ne s'est pas ouverte directement vous pouvez double cliquer dessus dans le panel des Fonctions.

Dès que vous arrivez dans votre fonction vous aurez votre node d'entrée :

![function](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/3a30b533-2c25-4573-a4ae-20e15cb93fa6)

Sachant que notre fonction doit enlever de la vie à notre personnage il faudrait avoir la vie du personnage en argument.
Vous allez cliquer sur le node d'entrée de la fonction.
Dans le Detail de la fonction situé en haut à droite vous aurez plusieurs options comme : le nom de fonction, l'option pure qui fait que si
on ne prend pas d'entrée mais uniquement une sortie ça changera le type de node mais les options les plus importantes sont les Inputs et Outputs.
On a besoin de prendre en entrée la vie du personnage donc, on va créer un Input nommé Damage de type Float.

![function_opt](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/2387248d-c70e-4c91-b0ea-3506157d21fd)

Vous devrez avoir ça maintenant :

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/97f1f7ac-4f28-4e6f-a06d-d751f2b15cef)

Sachant que notre fonction doit enlever de la vie à notre personnage donc on va rester cliqué sur l'input qu'on a mit et on va le tirer.
Vous voyez quand vous le relâcher ça vous affiche de la liste qu'on a vu toute à l'heure avec le context sensitive et les nodes disponibles.
Vous allez soustraire le CurrentHealth - Damage.
Pour ça vous devez récupérer votre variable CurrentHealth.
Vous avez trois choix pour la récupérer :

- Clic droit dans l'Event graph :
Après avoir fait clique droit dans l'event graph vous pouvez écrire "get (nom_de_votre_variable)" et ça la récupèrera.

- Panel de variable :
Vous allez dans le panel des variables et vous allez glisser déposer votre variable et une petite liste sera affiché avec marque soit get ou set votre variable :

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/15475542-de1e-467e-ba67-d7f664c544bf)

- Panel de variable :
Vous pouvez glisser déposer votre variable comme vu au-dessus mais vous pouvez utiliser un raccourci.
Lorsque vous glisser votre variable dans l'event graph juste avant de la déposer rester appuyer sur Ctrl pour la get.
En revanche, si vous voulez la Set il faudra rester appuyer sur la touche Alt.

Maintenant que vous avez récupérer votre variable CurrentHealth vous pouvez tirer son node est appeler le node mathématique : float - float.
Vous pouvez juste appuyé sur la touche "-" dans la barre de recherche ça vous la mettra directement.

On voit que le node "float - float" dispose de deux entrées de type float.
On va vouloir mettre notre variable CurrentHealth sur la première entrée et notre input Damage sur le deuxième.
Dès qu'on a fait ça, on veut que le résultat de notre opération soit mis à jour.
Donc on a juste à Set notre variable CurrentHealth par le résultat de cette opération.
On va relier l'output du "float - float" dans le set du CurrentHealth :

![result](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/992298f5-fb15-4661-948c-385bd82b2903)

Si une de vos entrées n'est pas bonne (pas relié au bon endroit).
Ce que vous pouvez faire sur l'entrée vous faites Alt + Clic gauche et ça vous enlève le node connecté.
Et vous avez aussi avec le Ctrl + Clic gauche mais celui-ci il faudra rester appuyé c'est pour rediriger un node vers un autre endroit.

Maintenant que notre fonction SubstractHealth est faite comment fait-on pour la tester ?

## Exercice 2

Allez dans l'event Graph de votre personnage et pas votre fonction.
Vous allez appeler la fonction Begin Play et vous allez appuyer la fonction de débug "Print String".
Vous allez get votre variable CurrentHealth et la relié directement a l'entrée "In String" du print string.
On voit que ce n'est pas le même type mais on voit que Unreal fait le "cast de type" automatiquement.
Ensuite on veut appeler notre fonction SubstractHealth après notre print string et refaire un print string de notre currentHealth afin de voir si notre health s'est bien substract
et a été mis à jour.
Evidemment il faudra mettre une valeur dans l'entrée Damage de la fonction qu'on a crée.
Pour avoir les valeurs du print string lorsque vous lancé votre jeu vous allez voir dans votre Viewport dès que vous avez lancé le jeu des valeurs en bleu en haut à gauche.
Logiquement vous aurez votre vie initial et juste en dessous votre vie après le substract.

## Exercice 3

Maintenant que vous avez réalisé la fonction Substract et le débug.
Vous allez faire la fonction AddHealth qui redonnera de la vie à votre personnage.
N'hésitez pas à débug pour voir si cela marche bien.

### User Interface

On peut voir notre vie actuel via le débug mais maintenant on veut un affichage visuel en temps réel.
Nous allons maintenant créer un widget.
Dans Content créer un nouveau dossier nommé UI.
Faites clique droit dans le CB > User Interface > Widget Blueprint.
On va le nommer UI_MainHUD.
Ouvrez-le.
On va arriver sur une toute nouvelle interface.
En haut à gauche vous aurez la "Palette" pour avoir des "objets" différents à intégrer à votre UI.
On aura besoin d'une progress Bar.
Glisser déposer l'objet progress bar dans votre UI.

On va avoir dans le detail panel le + important à faire.
On peut choisir le nom de l'objet mais celui-ci sera modifié si vous utilisez celui-ci comme variable.
Sa taille sur l'axe X Y mais aussi sa position.

![detail_pb](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/03885d5e-c088-4c32-a228-1fddc7a79e30)

Le Anchors sera le plus important car votre objets sera fixe et référence aux valeurs de position de l'anchor que vous avez choisi.
On va choisir le Anchor situé en bas au milieu.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/2bff6532-bb6e-47a1-bd2e-f819e6a8a9cc)

Vous pouvez choisir la taille que vous voulez ainsi que sa position.

On voit que dans l'interface des Widgets on a tout en haut à droite un côté Designer et l'autre Graph.

On va rester du côté Designer pour le moment vous allez cliquer sur votre Progress bar et dans le Detail vous voyez dans la catégorie Percent que vous pouvez set le percent actuel de la progress bar.
Vous pouvez aussi dans le style modifié sa couleur.
A droite du Percent vous avez un bouton Bind.
Cliquez dessus et vous allez créer un binding afin qu'il affiche la vie de votre personnage.
Le but est d'afficher la vie de notre personnage.
Donc on doit récupérer notre personnage.
On va faire un cast de notre personnage, récupérer la fonction cast to (nom_de_votre_personnage).
Celui de base est ThirdPersonCharacter.
Cette fonction prend un Object en entrée qui est un acteur donc tirer et veut notre personnage donc le node get player character.
On a deux nodes d'exécution qui sont juste après le cast et si le cast a failed et on a toutes les infos de notre personnage que ça soit variable fonction ou autre.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/26631f60-32fc-4b7e-92ad-ce649235e5c5)

Si vous avez bien regarder dans votre designer la progress bar va de 0 à 1 en valeur.

## Exercice 4

Récupérer la valeur current et max de votre vie et faites l'opération nécessaire afin d'afficher correctement votre vie.
Le résultat de l'opération sera stocké directement dans le return node dans sa return value.

**Indice:**
Votre vie va de 0 à 100 pour le Current et le Max.
La pourcent va de 0 à 1.

## Exercice 5

Maintenant qu'on a créer notre widget il va falloir le créer et l'afficher.
Dans votre l'event graph de notre personnage dans le begin play on va implémenter le node "Create Widget", référencer dans la class le nom du widget que vous avez créer et en sortie
tirer le node bleu et faites add to viewport.
Faites attention que l'exec est bien relié.
Ensuite ajouté un node "Delay" d'une nombre de seconde que vous souhaitez et ensuite appellez la fonction SubstractHealth.
Vous pourrez voir en direct votre vie initial et après substract.

### Actors

Notre système de vie est utilisé que via le Begin play on veut l'essayer par exemple si on entre dans une zone.
Dans votre Content browser vous allez créer un dossier Blueprints.
Vous allez créer un actor.
Clique Droit > Blueprint Class > Actor.
Nommer le comme vous le souhaiter (sachant qu'il va soustraire la vie de votre personnage).

Ajouter un component de type Box Collision dessus.

Faites un clique droit sur votre Box Collision vous allez ajouter un event de type OnBeginOverlap.
Ce qui va être lorsque l'acteur va être en contact avec un autre acteur.

![begin_overlap](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/5ce94d77-237b-491a-9e70-37c2dfd34571)

Vous aurez un Event comme celui-ci apparu dans l'event graph :

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/46cb4e0f-3b74-4e6d-b4ee-0b2a8faa3616)

On veut que lorsque c'est notre personnage qui rentre dans cette zone lui enlevé de la vie.
On va check si l'actor qui est rentré dans cette zone est notre personnage.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/15be4f3d-ccc5-4a98-9be1-b1361f89f35e)

On voit que l'output de notre égal est un booléan.
On va utiliser un branch qui est la même chose qu'un if.
Vous pouvez appuyer sur clique gauche + la touche B pour faire appraître un branch directement ou écrire if dans la barre de recherche.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/0fad8efc-0b17-4bb8-a36b-a091fae43970)

Si cela est vrai donc on va cast vers notre personnage et appeller la fonction SubstractHealth.

## Exercice 6

Faites entièrement l'actor pour vous substract votre vie et lorsque c'est terminé, implémenter le dans votre level et tester.
Si vous voulez voir votre box collision pendant que vous êtes en jeu.
Sélectionner votre box collision et dans le detail chercher le Hidden In Game et décocher le.

## Exercice 7

Faites le même Actor mais pour vous ajouter de la vie.

### Vectors

Sur Unreal on utilise des variable vecteur pour la position des acteurs présents dans notre level.
Créer un Blueprint BP_Elevator dans votre dossier Blueprints.

Vous allez ajouter un component "Cube" afin d'avoir un objet visuel pour voir si le système fonction.
Vous pouvez resize le cube directement dans le viewport de votre fichier.
Vous allez créer une variable de type Vector qui s'appelle StartLocation.
Vous l'initialiser avec le get actor location avec le begin play.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/095dc201-2ea7-4630-a0fc-3f5b71e43f98)

Ensuite vous allez créer deux custom event : EndLocation et StartLocationEvent.
Vous allez ensuite utiliser une timeline.

La timeline dans Unreal Engine est un outil très utile, cela permet de créer et de manipuler des animations et des variations de valeurs de manière visuelle.
Vous allez double cliquer sur votre timeline.
Vous tomberez sur ça :

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/f0a43519-2b06-4ea5-a501-2affecde8714)

C'est des tracks, celles qu'on va le plus utiliser c'est les float tracket et les vector track.
Vous avez une length, le temps dont vous voulez que votre timeline agit.
La on va utiliser une vector track car on manipule un vector.
Comme on fait un ascenseur donc va agir sur l'axe Z.
Dès que vous avez appuyé sur le vector track vous aurez les coordonées avec des cadenas on voudra lockk tous les axes excepté l'axe Z (bleu).

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/7eee135a-c852-4aa2-b721-f80b5959d22d)

On va faire un clique droit et ajouter une key dans notre timeline.
Comme c'est le début son temps et sa valeur seront de 0.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/44e64b32-6e93-454c-acfc-411a31287f44)

Ensuite vous allez créer une autre et dernière key.
Vous allez mettre le temps que vous avez référencer dans la length dans le time.
Et pour la value ça sera le nombre d'unité que vous voulez que votre ascensceur monte.

Vous pouvez retourner dans l'event graph.
et juste après votre timeline avec le node exec faire un SetActorLocation.
Vous allez get la variable Vector que vous avez créer au début et et l'ajouter avec le vector output de la timeline.
Vérifier bien que ça soit une opération "vector + vector" sinon vous pourrez pas ajouter les variables ensemble.
Le résultat de cette opération vous pouvez la relié à la New Location du SetActorLocation.

Pour les custom event que vous avez créer au début le custom event "EndLocation" sera relié au "Play from Start" de la timeline et le StartLocationEvent sera relié au Reverse From End.
Dernière chose à faire on a fait des custom event mais on n'appelle pas nos évènements.
Donc dans le begin play où on set notre StartLocation on va appeller la fonction EndLocation.

Glissez votre acteur dans votre level afin de voir si cela marche bien.
Si ça ne marche pas vérifiez dans votre component si votre Cube est bien en Movable dans le Detail panel.

## Exerice 8

Réaliser une plateforme qui se déplace de gauche à droite.

**Indice:**
- Utiliser une Timeline.
- L'axe de gauche à droite est l'axe X ou Y cela dépend de votre positionnement actuel et ce que vous voulez faire avec des obstacles par exemple.

### Interface

Nous allons utiliser maintenant un Blueprint Interface afin de réaliser un système d'interaction.

**Qu'est-ce qu'un Blueprint Interface ?**

## Bonus

Vous pouvez commencer à développer votre jeu pour le prochain workshop.
Vous avez le champ libre pour le type de jeu.

## Contact
Si vous avez des questions ou besoin d'informations, veuillez me contacter à arslan.tetu@epitech.eu