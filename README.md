# Workshop Unreal Partie 2

## Prérequis pour installer Unreal Engine 4.24.3 :

Vous devez installer le launcher Epic Games sur votre système. Vous pouvez le télécharger depuis le site officiel d'Epic Games : [Epic Games Launcher](https://store.epicgames.com/fr/download).

**Configuration minimale requise pour Unreal Engine 4.24.3 :**

- Système d'exploitation : Windows 7/8/10 64-bit.
- Processeur : Quad-core Intel or AMD, 2.5 GHz.
- Mémoire vive (RAM) : 8 GB.
- Carte graphique (obligatoire).
- Espace disque : 35-40 GB d'espace libre voir +.
- IDE : Visual Studio 2017 ou + (Conseillé) sinon VS code.

## Introduction

Si vous n'avez pas réaliser la partie 1 du workshop je vous invite à aller jeter un oeil [ici](https://github.com/Wavitoo/Workshop-Unreal-1).
Dans ce workshop nous allons nous initier à la programmation en C++ principalement et pour les plus rapide d'entre vous en Bonus vous pourrez faire des exercices en Blueprint.
Vous trouverez toute la doc donc vous aurez besoin [ici](https://docs.unrealengine.com/4.27/en-US/ProgrammingAndScripting/ProgrammingWithCPP/).
Nous devez assigner un IDE pour pouvoir compiler votre C++.
Aller dans Edit > Source Code > Votre IDE de votre choix.

## Programmation en C++

Créer un nouveau projet mais cette fois en C++ aller voir la partie 1 mentionné ci-dessus pour savoir comment créer un projet mais ça sera en C++ et en template blank.
Il faut savoir sur Unreal engine sur notre projet C++ on va quand même utiliser le blueprint ça sera un mix des deux.

## Exercice 1:

Aller dans C++ Classes, clique droit dans le content browser > New C++ Class > Character.

Pour aller dans C++ Classes appuyez sur le bouton qui se trouve juste à côté du Filter dans le Content Browser:

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/550eb640-b123-4df8-a089-16eb1a8c6088)

Nommez votre character PlayerCharacter.
Ensuite Create Class.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/5d1e2711-9df2-496c-83a8-90057ae8bcc7)

Vous verrez que directement après avoir créer votre character votre IDE sera ouvert avec le fichier .cpp et .h de votre character directement.
Pour ne pas oublier vous allez faire clique droit sur votre class character et créer un Blueprint avec.
Nommer le BP_PlayerCharacter.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/bd32402d-651f-4c0e-ada8-083ac6cf4591)

Ensuite vérfier que votre code compile bien.
Allez sur Unreal et vous verrez un bouton compile juste au dessus de votre viewport.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/d1c5c1ca-9424-450c-82d7-3d514dc96f71)

Vous verrez en bas à droite qu'il est en train de compiler votre code.
Si tout est bon ça sera marqué que la compilation est terminé.
A chaque changement de code ou création de fichier cpp vous devrez compiler pour assurer le bon fonctionnement.
Vous pouvez éviter de compiler à chaque fois en faisant Ctrl + Shift + B.

Dans le header vous allez créer une nouvelle catégorie protected.
Vous allez déclarer une variable qui est une class de UCameraComponent* Camera.

Dans le cpp, dans le constructeur vous allez créer la caméra dans votre personnage.
Pour pouvoir créer et attacher notre caméra on aura besoin du .h de la caméra qui est Camera/CameraComponent.h.
Vous allez utiliser la fonction CreateDefaultSubobject qui prendra UCameraComponent et en arguement on mettra le nom de la camera avec TEXT("").

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/39ddffce-00d1-477f-80f4-2e382bd59de1)

Evidemment le return pour cette fonction doit aller dans la variable Camera qu'on a créer dans le header.
Dès qu'on a créer cette caméra il faudra l'attacher à notre personnage donc il faut utiliser la fonction SetupAttachment(RootComponent).
Cette fonction fait partie de notre variable Camera.
Si on compile notre code on verra que dans le Blueprint de notre personnage qu'on a crée avant, on verra la caméra mais on ne pourra pas modifie sa position, sa rotation et autre.
Juste au dessus de votre déclaration de variable dans le .h vous allez utiliser la fonction UPROPERTY(EditAnywhere) qui vous permettra de la modifier.

Normalement si vous allez dans le Blueprint de votre personnage vous pourrez modifier la position de votre caméra.
Positionner la position de votre caméra au niveau de la tête environ a Z = 50.

Pour pouvoir bouger la caméra en jeu vous allez devrez activer l'option Use Pawn Control Rotation.

Dans votre code, toujours dans le constructeur vous allez activer la valeur bUsePawnControlRotation à true.
Elle fait partie de la class Camera.

Créer un fichier dans votre dossier Content.
Clique droit > Blueprint class > GameMode Base.
Appellez le BP_GameMode.
Ouvrez le fichier et dans Default Pawn Class mettez votre BP_PlayerCharacter.

Ensuite vous devez assigner votre gamemode :

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/7494e70e-51ef-47bd-9261-8ea975e9d075)

## Exercice 2:

Allez dans Edit > Project Settings > Input.
Vous allez créer un Action Mappings.

Nommez-le Jump avec la touche espace.

Ensuite deux Axis Mappings.
Un qui s'appelle MoveForward avec les touches Z et S.
Le scale de Z reste à 1 mais S sera à -1.
Voyez ça comme un axe, pour bouger vers le haut donc positivement c'est Z et pour bouger vers le bas donc négativement c'est S.
Le deuxième Axis Mappings sera MoveRight avec les touches Q et D.
Donc pour Q, son scale sera de -1 et D à 1.

Créer deux prototype dans le header qui se nommeront MoveForward et MoveRight qui prendront un float nommé InputValue.
Déclarer ces fonctions dans le cpp.

Dans la fonction SetupPlayerInputComponent.
Vous allez prendre la variable PlayerInputComponent pointer vers la fonction BindAction() qui prendra en argument le nom de l'action mappings donc "Jump", ensuite l'enum input donc quand on appuira sur la touche "IE_Pressed", this et la référence de la fonction Jump &ACharacter::Jump.

Vu que la c'était un action mappings on a utilisé BindAction() mais la on va utiliser BindAxis().
On va faire la même chose qu'on a fait pour Jump mais on enlève l'enum et au lieu que ça soit une référence de &ACharacter ça sera notre personnage directement donc &APlayerCharacter.

Pour les fonctions MoveForward() et MoveRight():

**- MoveForward():**

Vous allez créer une variable de type FVector avec le nom que vous souhaitez qui sera égal à la fonction GetForwardVector().
Et après la déclaration de cette variable on appelle la fonction AddMovementInput qui prendra en argument la variable qu'on vient de créer et l'argument de notre fonction.

**- MoveRight():**

La même que la fonction MoveForward() sauf pour la variable on utilisera la fonction GetActorRightVector().

Maintenant vous pouvez vous déplacer avec votre personnage.

## Exercice 3:

Vous allez créer deux nouveaux axis mappings Turn et LookUp.
Dans Turn ça sera Mouse X avec 1 de scale et dans LookUp Mouse Y avec une valeur de -1.
Si avec mouse X vous mettez -1 ça sera en inversé et pour mouse Y ça sera en inversé aussi.

Dès que vous avez créer les axis mappings créer les prototypes des fonctions dans le header.
Avec le nom de votre action mappings et les mêmes arguments que les fonctions qu'on a déjà faites.

Dans la fonction SetupPlayerInputComponent() on fait la même chose que pour les fonctions MoveForward() et MoveRight() sauf qu'on modifie le nom de l'axis mappings.
Pour la fonction Turn on va utiliser la fonction AddControllerYawInput() qui prend en argument la variable en argument de notre fonction.
Pour la fonction LookUp on va utiliser la fonction AddControllerPitchInput() qui prend en arguement la variable en arguement de notre fonction.

Vous pouvez compiler et normal vous pouvez bouger votre caméra.
Si votre caméra ne bouge pas vérifiez bien que vous avez bien activé le Use Pawn Control Rotation dans votre caméra dans le Blueprint du personnage.

## Exercice 4:

Vous allez important un Skeletal mesh pour avoir un personnage.
Vous pouvez import celui qui est dans le repo.
Spoiler: il est immonde aucune texture dessus.
Pour l'import il y a le bouton dans le content browser:

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/5492e1e8-021d-4603-9a07-ec675ab4325d)

Si vous voulez utiliser des vrais skeletal mesh vous pouvez retrouvez des sk mesh du market place gratuit ici[https://www.unrealengine.com/marketplace/en-US/product/adventure-character] et ici [https://www.unrealengine.com/marketplace/en-US/product/stylized-male-character-kit-casual].

## Exercice 5:

Dans la catégorie public de votre hpp déclarer le prototype de votre fonction void SpawnActor().
Juste au dessus de votre prototype vous aller utiliser UFUNCTION() qui prendra en argument BlueprintCallable et Category = "Abilities".
Ce qui va nous servir à distinguer notre fonction en Blueprint car il existe déjà des fonctions SpawnActor.

Ensuite vous allez créer une variable TSubofClass où la classe sera AACtor avec le nom de l'actor qui va spawn.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/f242b920-25c3-4837-aa9d-200d76a86d05)

Au dessus de cette déclaration de variable vous allez mettre UPROPERTY() avec en argument EditAnywhere pour pouvoir référencer l'actor à spawn directement dans votre personnage.

Dernièrement une variable de type FTransform qui sera aussi en EditAnywhere pour pouvoir modifier la position où l'objet spawnera.

Dans votre header vous allez include : "Runtime/Engine/Classes/Engine/World.h".
Il faut savoir que les include doivent être avant le .generated sinon vous aurez des erreurs de compilations.

Dans votre fonction vous allez utiliser une variable de type FActorSpawnParameters.
Vous allez ensuite modifier la valeur de ce type avec SpawnCollisionHandlingOverride qui sera égal à l'enum ESpawnActorCollisionHandlingMethod qui appelera l'enum class avec ::, la class AdjustIfPossibleButAlwaysSpawn.
Ensuite on va récupérer notre monde avec GetWorld() qui va appeler la fonction SpawnActor avec la class Actor avec les signes inférieur et supérieur qui prendra en arguement l'actor a spawn, notre variable FTransform et la variable qu'on a déclaré dans la fonction.

Oubliez pas de compiler Shift + Ctrl + B ou compile directement sur unreal.
Si vous allez dans votre personnage et dans Class Default vous verrez qu'il y aura l'actor à spawn et la position.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/26ff1f49-15b1-4fc5-96c1-dbb1b0c9b018)

Dans votre Event graph de votre personnage vous allez appeler l'event Left Mouse Button.
Vous allez tirer le node Pressed et appeler votre fonction SpawnActor, vérifiez qu'elle est bien dans la catégorie Abilities.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/1b0b14ec-658e-47c6-b139-fda25e71f7d5)

Maintenant, créer un nouveau Blueprint Class de type actor et ajouter un Cube dedans avec le Add Component et activer l'option Simulate Physics avec votre cube sinon il sera sans gravité.
Assigner votre acteur dans votre personnage avec le nom que vous lui avez donné à votre Actor où il y a cube et choisissez la position où vous voulez qu'il spawn.
Ensuite lancez votre jeu et essayer votre code en appuyant sur clique gauche.

## Exercice 6:

Vous allez include "Blueprint/UserWidget.h" dans le .h.
Dans la catégorie public, vous allez créer trois variables une pour votre vie et deux pour votre widget.
Une variable float pour la vie de votre personnage au dessus il y aura le UPROPERTY() avec les arguments EditAnywhere et BlueprintReadWrite.
Un TSubclassOf de UUserWidget qui sera la class de votre widget.
Et un pointeur de UUserWidget qui sera votre widget.
Au dessus de notre variable qui contiendra la class de notre widget le UPROPERTY() avec en argument EditAnywhere et Category = "UI".
On va déclarer le prototype de notre fonction :

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/0e027389-efaf-4056-856b-876e35495be4)

Dans votre cpp vous allez include : "Components/CapsuleComponent.h" afin de pouvoir utiliser la CapsuleComponent de votre personnage pour jouer avec les collisions.
Dans votre constructeur vous allez initialiser votre vie du personnage à 100 et attention c'est un float donc on oublie pas le .0f.
Dans la fonction BeginPlay on va récupérer notre CapsuleComponent avec la fonction GetCapsuleComponent() qui pointe sur la structure OnComponentBeginOverlap() et pas notre fonction.
La structure va appeler la fonction AddDynamic() qui aura en argument this et notre fonction OnBeginOverLap en référence.

Ensuite on va check si notre widget class est différent de nullptr.
Si c'est différent donc on va utiliser notre variable widget et pas la class qui sera égale à la fonction CreateWidget() qui prendra en arguement GetWorld() et notre class de widget.
Après il faudra afficher notre widget avec la fonction AddToViewport().

Dans votre gestionnaires de fichiers vous allez devoir trouver un fichier nommé : NomDeVotreProjet.Build.cs.
Dans le PublicDependencyModuleNames vous allez ajouter "UMG" afin de pouvoir utiliser les widgets.

Dès que c'est fait on va faire notre fonction OnBeginOverLap().
On va check si OtherActor continet le tag avec la fonction ActorHasTag("et vous mettez le tag que vous voulez").
Si c'est vrai on va enlever x points de vie à notre personnage.

Vous allez créer un dossier Widget dans Content et créer un UserInterface.
Clique droit > User Interface > Widget Blueprint.
Vous allez ajouter une progress bar dans votre UI configurez la comme vous le souhaiter.
Cherchez percent pour voir progress bar.
Vous allez voir un bouton Bind, cliquez dessus.
Ca sera pour récupérer la valeur et la set pour la progress bar.
Vous allez faire un cast to BP_PlayerCharacter.
Dans le object vous faites un get player character.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/7dbc1646-fd1f-40ea-9ed1-c1c33a2cad49)

Dans le As BP_PlayerCharacter vous allez chercher votre variable que vous avez créer dans votre C++ pour la vie de votre personnage.
Cette valeur vous allez faire un float / float.
Vous divisez cette valeur par 100 car la progress bar va de 0 à 1.
Vous mettez le résultat de cette opération dans le return value.

Vous allez créer un actor, ajouter un cube dedans et dans la catégorie collision, collision presset vous mettez OverlapAll.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/7d6de20c-5b36-4605-83ad-f0a29309fc96)

Comme ça votre personnage pourra passer à travers.
Dernière chose vous allez dans Class Default et cherchez tag et renseignez le tag que vous avez mis dans votre code C++.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/712935cb-30bb-4f4f-8b3a-6b0598ad7d60)

Glissez votre actor dans votre level vous devrez normalement perdre de la vie.

## Exercice 7:

Faites la même chose mais pour vous ajoutez de la vie.

## Exercice 8:

Dans cet exercice, vous allez créer une plateforme mobile.

Dans le Content browser aller dans C++ Classes > Nom de votre Projet > Clique Droit > New C++ Class > Actor.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/38cfb822-86a2-49a8-9eb6-03ee548d7eee)

Nommer votre fichier MovingPlatform.
Nous allons faire directement pour que la plateforme sur tous les axes ainsi qu'elle puisse tourner.
Dès que votre fichier est créé vous voyez qu'il y a un header et un cpp.

Dans le header vous allez créer un section private et vous allez utiliser la fonction UPROPERTY().
Dans le UPROPERTY vous allez mettre en argument EditAnywhere et Category="Moving".

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/e8c8860e-2721-4797-8b96-9c062964672b)

Cela va vous servir de faire une catégorie pour chaque déplacement sur chaque axe.
Vous allez ensuite appeler la structure FVector (comme type de variable) qui sera assigné à la vitesse de la plateforme.
Cette variable Fvector avec le nom que vous avez choisie sera égale aussi à un FVector en arguement (100,0,0).
Ensuite vous recréer le même UPROPERTY que vous avez fait au dessus.
Vous allez déclarer une variable pour la distance sur laquelle votre plateforme va bouger assigner lui une valeur.
Ensuite pour la dernière variable qui sera encore de type FVector pour la location d'où votre plateforme partira.

Vous allez créer le prototype de votre fonction MovePlatform qui prend en argument un float et le nom de la variable DeltaTime.
Ensuite vous allez créer deux autres prototypes de fonction une qui sera de type bool pour savoir si la plateforme doit revenir qui sera const et l'autre de type float pour récupérer la distance parcours qui sera aussi const.

Vous allez coder maintenant les fonctions récupérer la distance parcourue et si la plateforme doit retourner et la distance parcourue.
Il faut faire attention à la classe donc notre fonction dans le cpp sera de type :

void (Class)::NomDeFonction(type_var nom_var, ...)

Logiquement pour la fonction de la distance parcoure est :

float AMovingPlatform::NomDeVotreFonction() const.

Dans cette fonction vour allez utiliser une fonction qui est dans la structure FVector qui se nomme Dist().
Elle prendra deux argument la position de base et la position de l'acteur.
Sachant qu'elle est de type float ça veut dire qu'on doit return une valeur pour ensuite utiliser le résultat de cette fonction.

Pour la fonction pour que la plateforme revienne en arrière est :

bool AMovingPlatform::NomDeVotreFonction() const.

Vous allez utiliser la fonction GetDistanceMoved et la variable que vous avez créer dans le hpp pour la distance parcourue.
Son type est bool donc on veut aussi le résultat de cette fonction.

Dans la fonction BeginPlay assigner la position de start qui sera égal à la fonction GetActorLocation().

Maintenant pour la fonction pour bouger la plateforme qui est structuré comme ceci :

void AMovingPlatform::NomDeVotreFonction(float DeltaTime).

Dans cette fonction on doit faire une condition que si elle a déjà parcourue sa distance.
Elle va revenir en arrière donc :
Créer une variable de type FVector qui sera égale à votre variable vitesse de la plateforme.GetSafeNormal().
Ensuite on modifie la variable de la position de Start donc elle sera additionné à la variable qu'on vient de créer de FVector * sa distance parcourue.
Après on doit assigné sa nouvelle position avec la fonction SetActorLocation().
Ensuite vu que notre variable de vitesse est positive elle doit être maintenant négative afin d'aller dans la direction inverse.

Sinon, on recréer une variable de type FVector qui sera égale à la fonction GetActorLocation().
Cette variable sera additionné par (la vitesse de notre plateforme * le delta time).
Les parenthèses sont importants dans la phrase du dessus.
Enfin on assigne notre position avec SetActorLocation().

Maintenant il faut appeler notre fonction sinon elle ne fera rien.
Dans la fonction Tick on appelera notre fonction qui sert à bouger la plateforme avec l'argument.

Glisser déposer votre actor MovingPlatform dans le level et ajouter lui un cube avec Add Component.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/403fcf45-8d11-44bd-ab83-0114f0cafb5c)

Normalement vous verrez vos variables que vous avez assigné directement depuis le viewport.
Si vous avez bien réaliser votre code, votre plateforme doit bouger de gauche à droite et la vitesse dépend de ce que vous assigner en valeur.

## Exercice 9:

Implémenter la rotation dans votre actor MovingPlatform.
Dans votre header au lieu que ça soit un FVector ça sera un FRotator et la fonction sera du même prototype que la fonction pour bouger la plateforme.
Oublier pas d'ajouter le UPROPERTY mais cette fois avec une catégorie différente avec Rotation.
Dans la fonction pour tourner votre plateforme au lieu d'utiliser GetActorLocation() et SetActorLocation() vous allez utiliser directement pour la rotation.

## Exercice 10:

Modifier les axes vector de votre actor afin que cela marche comme un ascenseur de haut en bas.

## Exercice 11:

Modifier les axes rotator de votre actor afin qu'il puisse tourner.
Si il y a des bugs de collision allez dans votre blueprint de votre personnage.
Ouvrez l'event graph appeller l'event tick.
Appeller deux fois la fonction MoveUpdateComponent et pour ces deux nodes en target ça sera le character movement et pour la rotation vous faites un get actor rotation.

## Exercice 12:

Maintenant que vous avez fait un actor pour bouger la plateforme en continue faites pour que ça soit directement.
Faites une "porte" un grand cube qui s'ouvrira en de gauche à droite comme un décalage.

## Exercice 13:

Faites la même chose mais pour une porte de garage de haut en bas.

## Bonus

## Programmation en Blueprint

Ouvrez votre fichier qui contient votre personnage.

### Event graph

Vous pouvez voir dans l'event graph vous avez déjà du code existant.
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

Une Interface Blueprint est un ensemble d'une ou plusieurs fonctions, uniquement le nom, sans implémentation qui peuvent être ajoutées à d'autres Blueprints.
Tout Blueprint auquel l'Interface est ajoutée est garanti de posséder ces fonctions.
Les fonctions de l'Interface peuvent recevoir une fonctionnalité dans chacun des Blueprints qui l'ont ajoutée. Cela correspond essentiellement au concept d'une interface en programmation générale, qui permet à différents types d'objets de partager et d'être accessibles via une interface commune.
En résumé, les Interfaces Blueprint permettent à différents Blueprints de partager des données entre eux et de s'envoyer des données.

Dans le dossier Blueprints créer un dossier Interface.
Dans le dossier Interface vous allez ajouter un Blueprint Interface situé dans Blueprints > Blueprint Interface.
Nommer votre fichier BPI_Interact.
Ouvrer votre BPI et renommer la fonction Interact.
Allez dans votre blueprint du personnage et appuyer sur Class Settings.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/d29eea4e-126b-4829-a4b7-dd8cf1f4f76a)

Ensuite, ajouter votre Interface via le bouton Add dans la catégorie Interfaces.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/7be72119-f6d9-4fa5-85d0-368ea94cdf50)

Vous verrez que vous aurez une nouvelle catégorie Interfaces dans le panel My Blueprint.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/a21dfa51-4353-4aad-b3d4-964e87cd71c3)

Vous allez maintenant implémenter le système d'interaction.
Vous pouvez soit appeler la touche directement de l'envent graph comme par exemple la touche E.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/40757f69-2320-4755-b1a8-6949de9daef8)

Sinon vous pouvez faire un nouveau action mapping dans le Edit > Project Settings > Input > Action Mapping > +.
Vous devrez donner un nom à votre Action mapping et lui assigner une touche.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/8031af9d-8cd9-4bb9-a635-f0e421c882c0)

Dans votre Event Graph du personnage appeler soit votre Action Mapping en mettant son nom ou juste la touche de clavier que vous souhaitez utiliser.
On va utiliser un For each loop.
On voit qu'en entrée il prend un array.
On va lui assigner la fonction Get Overllaping Actors.
On va ensuite tirer la Array element du for loop et chercher le node "Does Implement Interface".
Dans l'entrée Interface on va renseigner notre Interface BPI_Interact.
En sortie de ce node on va faire un if et si cela est vrai on va faire la fonction Interact (Message).
Si vous ne la trouvez pas tirer le Array element du for loop et taper la fonction Interact (Message).

**Que font les nodes qu'on a ajouté ?**

**- For Each Loop :**
Une boucle "For Each" en Blueprint (similaire à d'autres langages de programmation) itère sur chaque élément d'un tableau (array).
Pour chaque élément, elle exécute un ensemble de nodes connectés.

**- Does Implement Interface :**
Le node "Does Implement Interface" vérifie si un objet spécifique implémente une certaine interface Blueprint. En d'autres termes, il détermine si l'objet a ajouté cette interface et, par conséquent, s'il contient les fonctions définies par l'interface. C'est utile pour assurer qu'un objet possède certaines fonctionnalités avant de tenter de les utiliser.

**- Interact (Message) :**
En Blueprint, les interfaces peuvent définir des fonctions ou des événements appelés "Messages". L'interaction (Message) d'une interface envoie un message ou appelle une fonction définie par l'interface sur un objet cible. Cela permet de déclencher des comportements spécifiques sur des objets qui implémentent cette interface, même si les objets sont de types différents. Le message "Interact" est souvent utilisé pour des actions communes comme l'interaction du joueur avec des objets dans le jeu.

## Exercice 9

Créer un actor et ajouter lui l'interface BPI_Interact.
Ajouter une forme que vous voulez en component et on va lui créer un trigger (lorsque le joueur sera dans une zone proche à l'objet).
Ajouter une sphere collision et augmenter son radius.
Quand le joueur rentre dans la zone (OnActorBeginOverlap) vous allez mettre un print string "Ready to interact".
Quand le joueur sort de la zone (OnActorEndOverlap) vous allez mettre un print string "Cannot interact anymore".

### Interaction

Nous allons créer un blueprint lorsque le joueur sera dans la zone afin de voir un message qui apprait sur l'écran pour dire qu'il peut interagir.
Dans le dossier UI créer un widget blueprint.
Nommer le UI_InteractPrompt.
Changer la façon dont on verra votre widget par Desired au lieu de Full Screen.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/7e336ca1-9f5b-469c-b81b-b55695c5f08f)

Supprimer le canvas panel et ajouter une Vertical box.
Dans cette vertical box ajouter un texte qui contiendra [votre touche] Intéragir.
Vous pouvez augmenter la taille du texte, rajouter des outlines et d'autres si vous le souhaiter.

Retournez dans votre actor que vous avez créer pour l'interface.
Ajouter un component "Widget" à votre actor et assigner votre UI dans dans le Widget Class.

![image](https://github.com/Wavitoo/Workshop-Unreal-2/assets/114447473/366e76e1-0397-458a-a276-f53e5d3c4a9d)

Ensuite positionner bien votre texte jusqu'à ce que vous soyez satisfait et dès que vous avez terminé changé le Space, de World à Screen.
Dernière chose à faire avec le widget enlever sa visibilité dans le detail panel.


## Exercice 10

Normalement vous avez ajouter les print string lorsque le joueur rentre dans la zone et sort de la zone.
Vous pouvez supprimer les print string et get le Widget disponible dans vos variables.
Si il entre dans la zone (OnActorBeginOverlap) un set visibility à true et si il sort False.

## Exercice 11

Faites un nouvel actor qui sera comme une porte de garage donc il s'ouvrira par le haut ou sur la gauche.
Faites des custom event pour pouvoir rappeller vos fonctions après.

**Indice :**
Utiliser une timeline et regarder dans le Viewport général pour les axes.

## Exercice 12

Dans l'actor qui réçoit l'interface vous allez créer une variable qui aura comme type l'actor que vous avez créer en object reference.
Faites un get et appelez votre fonction pour ouvrir la porte.
Normalement lors de l'appuie de la touche que vous avez assigné la porte s'ouvrira.

## Contact
Si vous avez des questions ou besoin d'informations, veuillez me contacter à arslan.tetu@epitech.eu