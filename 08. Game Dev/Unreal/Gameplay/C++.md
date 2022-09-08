# C++ In Unreal

Documentation Unreal : https://docs.unrealengine.com/5.0/en-US/

## Ereurs Possibles

### Fichiers non visibles
Bug quand on ajoute des éléments dans un dossier et ils sont pas pris en compte dans l'Engine. Pour corriger ce bug, on ouvre le content Drawer => Ouvrir dans l'exporeur => Ouvrir la solution => Enlever le nom du dossier dans le #include de la classe.

Rebuild le projet et le relancer

Rider Link qui pose des problemes de compilations

### Erreur de compilation à cause de fichiers introuvables

Il faut supprimer le dossier binaries et intermediaries puis relancer le projet

## Basic

### Créer une nouvelle Classe (assimilée à un Blueprint, ceux d'Unreal)

Les éléments de code sont dans le Dossier C++ Classes sur Unreal dans le Content Drawer et clique droit New class.

Il faut choisir la classe parent (héritage) en suite, voici les principales (il en existe énormement)
* None : Classe classique
* [Actor](https://docs.unrealengine.com/5.0/en-US/unreal-engine-actors/) : C'est un objet qui peut être placé ou spawn dans le niveau, ils peuvent être crées et détruits
* [Pawn](https://docs.unrealengine.com/5.0/en-US/possessing-pawns-in-unreal-engine/): c'est un Actor qui peut être contrôlé et recevoir des inputs comme une voiture
* [Character](): C'est un Pawn qui peut marcher / Se déplacer.

La hiérarchie est donc AActor => APawn => ACharacter.

En gros, Actor si c'est pour le monde, Pawn si c'est ça peut être possédé par une IA ou le joueur ou intéragit et enfin character si y a du déplacement


### Implémenter dans le Monde
On peut ajouter une classe dans le monde avec un drag mais cela servir à rien, il faut l'associer à un blueprint. Pour cela, on selectionne la classe et on créer un Bleuprint basé sur cette classe. Les guidelines veulent que les blueprints soient mis dans un autre dossier que les classes C++ et commencent par :

BP_NameDuBlueprint

Ainsi, il peut être dans le monde.


## C++ Structure

Comme en C++, il y a le Header qui est le template, une pseudo interface de la classe, et l'implémentation le .cpp. En fonction de l'héritage de la classe, il peut avoir du code ou non présent dans la classe.

### Basic Function

* Constructor: default Class
* Begin Play : C'est appelé quand le jeu est commencé ou que l'objet est Spawn
* Tick : qui est appelé à chaque Frame
* SetpPlayerInputComponent: C'est lié au Input du Player (On utilise actions & accesss map)




## Components

Unreal fonctionne avec un système de Component, ce sont des objets que les actors peuvent attacher à eux même ou leurs enfants. Ils permettent de faire beaucoup de choses (Trigger, Visual, Vehicle input etc).

Plus d'informations : https://docs.unrealengine.com/5.0/en-US/components-in-unreal-engine/

les components se créent dans le Root pour tout ce qui est après Actor. Cela permet d'avoir accès au Transform et affecte dans tous les enfants. Le root doit donc contenir tous les enfants

#### Scene Components

C'est un actor component qui existe dans le monde. La position est défini par une class Transform (FTransform) avec la rotation, position, scale, etc. C'est possible de créer des hiérarchies à partir de la.

Liste de components:
* Static Mesh : Permet d'ajouter un Mesh à un actor
* UCapsule Component : Collider Capsule


#### Ajouter un Component en C++
Les components s'ajoutent dans le Constructor de la classe. Pour ajouter un component, il faut créer un root Component pour cela on peut se servir d'une capsule component pour les collisons 

https://docs.unrealengine.com/5.0/en-US/API/Runtime/Engine/Components/UCapsuleComponent/

Pour cela, on crée la variable dans le header commme ceci :
```UCapsuleComponent* capsuleComponent;```
