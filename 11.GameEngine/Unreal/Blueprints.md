# Blueprints

Les blueprints sont le visual Code d'Unreal. Ils permettent de développer des fonctionnalités du jeu, ils peuvent être en complément du C++ ou en remplacement. Ils sont un peu plus riche qu'un simple visual Code car ils contiennent beaucoup d'informations comme la hiérarchie, les éléments d'un objet. C'est l'équivalent d'un Prefab d'Unity avec la possibilité d'y ajouter des scripts.

Pour la navigation, on a plusieurs onglets comme pour le reste d'Unreal si une fenêtre est manquante, on peut l'ajouter avec le Menu > Fenêttre ou alors la trouver dans My Blueprint pour l'event Graph. Enfin, on peut toujours rénitialiser le layout dans le pire des cas.

## Les différents Blueprint

Il y a plusieurs types de blueprint, on peut y accéder dans le menu avec cette icône :
![image](https://user-images.githubusercontent.com/58773222/188317774-b97485f7-ad58-49f6-bfff-f4d00bce9bc9.png)

On y trouve les blueprints de base, la possibilité de créer des blueprint ,les gamemode mais aussi le BluePrint level qui est général au niveau. Le blueprint Level a pour nom GameMap, cela signifie bien que c'est l'ensemble du niveau.

## Blueprint Level
Il est un peu plus particulier qu'un autre blueprint car il est général au niveau. De ce fait, il propose différents outils en fonction de la sélection lors qu'il est ouvert. Si on veut utiliser un objet dans ce blueprint, il faut le preselectionner. Si la selection n'apparait pas, il faut aller le sélectionner.


## Event Graph

C'est un sytème d'event. On crée un event qui va déclencher une chaine de logique. L'event peut être un input, un event appelé par un autre objet ou les ticks qui correspondent au Frame. Chaque box est appelé un node, on peut les rechercher avec clic droit et taper le nom ou alors en draggant une fleche dans le vide.

## Debugging
Pour débugger, il faut lancert le jeu et associer le blueprint à l'instance in game de son choix
![image](https://user-images.githubusercontent.com/58773222/188307501-f7924897-6159-403e-bfe6-386def6c04d7.png)

Il y aussi des nodes permettant d'afficher des données à l'écran comme Print String ou encore Log String pour mettre les informations dans les logs.

Lorsqu'on est ingame, Unreal met aussi beaucoup de commandes à disposition pour pouvoir débugger son code. On accède à la commande avec '²' et on peut écrire des commandes comme :

* t.maxFPS x pour limité les FPS à x (0 = uncapped)

## Créer une variable
Pour créer une variable, il suffit d'aller dans l'onglet MyBluePrint et de cliquer sur le signe "+" à côté de Variables. Suite à cela, on peut cliquer sur la variable pour modifier ses parametres comme son type, si on veut qu'elle puisse être modifié dans l'editeur ou uniquement par blueprints/code.

![image](https://user-images.githubusercontent.com/58773222/188307659-4af72a8e-c427-4e97-acd3-0291e03e82d9.png)


## les Différents nodes

### Create Widget
Cela permet de créer une widget de son choix sur l'écran. On choisit le widget avec la class

### Cast
Cela permet de spécifier un type d'élément
