# C++ In Unreal

Documentation Unreal : https://docs.unrealengine.com/5.0/en-US/

## Ereurs Possibles

### Fichiers non visibles
Bug quand on ajoute des éléments dans un dossier et ils sont pas pris en compte dans l'Engine. Pour corriger ce bug, on ouvre le content Drawer => Ouvrir dans l'exporeur => Ouvrir la solution => Enlever le nom du dossier dans le #include de la classe.

Rebuild le projet et le relancer

Rider Link qui pose des problemes de compilations

### Fichiers Intermediate Manquant
Aller dans le dossier du fichier, clique droit sur le .uproject et faire generate Visual Studio Project Files
![image](https://user-images.githubusercontent.com/58773222/189185601-573eea13-a388-493d-8bf5-9dd37f602cd5.png)

### Blueprints Not Updated

Il suffit d'appuyer sur le boutton compile du blueprint


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

En gros, Actor si c'est pour le monde, Pawn si c'est ça peut être possédé par une IA ou le joueur et enfin character si y a du déplacement. Il faut savoir qu'on peut piloter un pawn dans l'editeur en faisant clique droit "pilot"


### Implémenter dans le Monde
On peut ajouter une classe dans le monde avec un drag mais cela servir à rien, il faut l'associer à un blueprint. Pour cela, on selectionne la classe et on créer un Bleuprint basé sur cette classe. Les guidelines veulent que les blueprints soient mis dans un autre dossier que les classes C++ et commencent par :

BP_NameDuBlueprint

Ainsi, il peut être dans le monde.


## C++ 

### Structure

.h => Prorortpe/ Pseudo Interface de la classe
.cpp => Implémentation du Code

Le .h va récupérer tous les includes qui lui ont été ajouté (recursif) puis il va s'ajouter dans le fichier .cpp. Cela veut dire que plus il y a une chaine d'includes (poupée russe), plus la compilation va être longue et les fichiers lourd, Exemple : 

![image](https://user-images.githubusercontent.com/58773222/189181103-db3842d1-dc72-45b0-a6fa-d5be6b944962.png)

Cela signifie que UCapsuleComponent sera présent dans 4 endroits différents au lieu d'un seul qui est le Fichier de base. Pour empêcher cela, il existe le principe de Forward Declaration qui permet de référencer un élément dans le .h mais l'inclusion se fait dans le cpp ce qui permet d'alléger la compilation sans erreurs.

### Forward declaration 
Forward Declaration permet de declarer un identifier sans que l'objet ait une définition complete. Cela s'utilise quand on n'a pas besoin de l'élément. Par exemple, on veut juste déclarer une varaible ou quand quelque chose est en private. Dès que les autres scripts n'ont pas de raison et ne peuvent pas l'utiliser.

Pour cela, il faut déclarer le Include dans le fichier .cpp et ajouter le keyword "class" à l'élemetn en question par exemple :

.h
```
protected:
	virtual void BeginPlay() override;
	class UCapsuleComponent* CarCapsule;
```

Cela vient en complément avec #pragma once qui permet de ne pas duppliquer les dépendances dans le header.

### Template Function
Un template function s'adapte au type choisi donc on peut choisir un type particulier. C'est l'équivalent d'un générique en C#

Exemple dans Unreal
```
CreateDefaultSubobject<UCapsuleComponent>(TEXT("NomDeLObjet");
```

Cette fonction permet de créer un objet de type UCapsuleComponent avec un paramètre spécifiques. Cela vient de la classe UObject qui peut être instancié à partir de cette fonction juste en ayant un nom

### Operators

:: pour ce qui est dans un Namespace
. quand on a un objet instancié ou une reference vers un objet
-> pour les pointers

## C++ In Unreal

### Basic Function

* Constructor: default Class
* Begin Play : C'est appelé quand le jeu est commencé ou que l'objet est Spawn
* Tick : qui est appelé à chaque Frame
* SetpPlayerInputComponent: C'est lié au Input du Player (On utilise actions & accesss map)

Les fonctions sont déclarer avec le nom de la classe avant car cela sert de Forward declaration  pour les implémentations liées à l'objet Parent

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

Pour cela, on crée la variable dans le header et il faut ajouter la référence en include que ça soit dans le header ou en Forward declaration commme ceci:
```
#include "Components/CapsuleComponent.h"

UCapsuleComponent* capsuleComponent; // toujours un pointer car sinon c'est copié par value et pas par reference, on peut aussi utiliser une ref (Check C++)
```

Il faut faire attention à la distinction entre l'élément et le Component. Exemple, UStaticMesh et UStaticMeshComponent. L'un est le component qui prend en parametre un Static Mesh.

#### Utiliser un Component en C++

Pour créer un Component, on Utilise la fonction CreateDefaultSubobject<>() qui marche pour tous les UObjet et apres on peut l'assigner comme on souhaite comme en RootCompomenent par exemple.

```
Capsule = CreateDefaultSubobject<UCapsuleComponent>(TEXT("Car Capsule"));
RootComponent = Capsulse;
```

Si des Components sont déjà ajoutés via le Blueprint, ils vont etre en enfant du Root Component assigné en C++. Par contre, si on crée un élément en C++, il faut l'ajouter au RootComponent

```
MainMesh = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("Main Mesh"));
MainMesh->SetupAttachment((Capsule));
```

#### Configurer un Component en C++
Il est important de préciser que même en Public, on ne peut pas modifier les components en blueprint. Les utilisateurs n'auront donc pas accès à la fenetre Details pour les components.

Il est donc utile de créer des proprietés (UPROPERTY) pour qu'elles puissent être configurables dans le Blueprint

**UPROPERTY**
C'est un attribut qui permet de définir comment une variable va se comporter dans l'editeur et si on peut interagir avec en dehors du code. Cela se place comme un attribut en C# (donc avant la variable), on appelle ça des Metadata specifier. Cela permet de déterminer où est visible et modifiable la proprieété comme ceci :

```
UPROPERTY(VisibleAnywhere)
int Speed;
```	

Voici les différents modes :

* VisibleAnywhere : Read-only, apparait dans les properties d'une instance et de le blueprints
* VisibleInstanceOnly: Read-only Visible que dans l'instance
* VisibleDefaultOnly: Read-only Visible que dans l'editeur BluePrint
* EditAnywhere: Editable dans les proprietés d'une instance et le bluerpint
* EditInstanceOnly: Modifiable dans l'instance
* EditDefaultsOnly: Modifiable dans Blueprints 

#### Camera
La camera est divisé en plusieurs parties. Il y a d'abord le SpringArm qui permet de manipuler la caméra et enfin la Caméra. Le spring Arm permet de gérer les colisions avec le décor. Cela va rapprocher la caméra lors de collisions et la remettre à sa position lorsqu'il n'y a pas de colission.

https://docs.unrealengine.com/5.0/en-US/API/Runtime/Engine/GameFramework/USpringArmComponent/

Les changements de position sont sur le Spring Arm avec le Offset Et le Target Arm Length.


## Player
Par défaut, le joueur va contrôler un élément spécifique qui est configuré par Unreal. On peut changer ce qui est possédé par le joueur que cela soit dans les Settings ou dans les Details d'un Pawn dans l'onglet "Pawn", il y a le champ "Auto Possess Player", si on définit Player 0, le joueur prenant possession de l'objet des le début.

## Input
Les inputs se trouvent le Project Settings (Accesssible via le boutton settings ou le menu Edit). Dans la catégorie Engine, il y a le champ Input qui permet de créer des bindings et de faire des actions/Axis Mappings. Pas besoin de save dans les settings

Action Mappings c'est pour appui/release alors que l'axis c'est pour les inputs continu avec une range.

### Axis Mapping
On crée un Axis et on ajoute des axes avec une valeur. Par exemple: 
![image](https://user-images.githubusercontent.com/58773222/189237991-dbf002b7-4ee6-4a32-9973-054d48777a44.png)

#### Bind l'Axis en C++
Il suffit de créer une fonction pour traiter les inputs et la relier aux inputs. Le binding des inputs se fait avec cette fonction : SetupPlayerInputComponent qui est implémenté de base.
En suite, on y relie une fonction du code au nom de l'input exemple :

```
PlayerInputComponent->BindAxis(TEXT("Move Forward / Backward"), this, &ACarPawn::MoveCar);

void ACarPawn::MoveCar(float MoveValue)
{
	// Do Stuff
}

```

Il est important de préciser le nom de la classe pour pouvoir passer le parametre par référence (signature de la fonction)


## Movement
On utilise les Vectors pour representer les positions (FVector) et on a plusieurs fonctions en outils

**AddActorLocalOffset**
Cela prend un FVector en parametre et cela offset le transform de X en espace Local donc relatif. C'est à dire que la position par défaut est VectorZero

Exemple :
```
FVector currentLocation = FVector::ZeroVector;
currentLocation.X += MoveValue * 5.f;
AddActorLocalOffset(currentLocation);
```

Il est important d'utiliser le Delta Time pour éviter les Frame Rate car les Frame rate sont instables selon les ordinateurs et les conditions, on utilise donc le delta time pour avoir une vitesse constante selon les jeux (comme Unity)

On recupere le Delta time avec cette fonction : UGameplayStatics::GetWorldDeltaSeconds qui prend un parametre UObject* worldcontext, donc on peut emttre this comme reponse :
```
currentLocation.X += MoveValue * speed * UGameplayStatics::GetWorldDeltaSeconds(this);
AddActorLocalOffset(currentLocation);
```

AddActorLocalOffset prend en parametre un bool bsweep qui permet de check les trigger/collisions si elles sont activées :

"Whether we sweep to the destination location, triggering overlaps along the way and stopping short of the target if blocked by something. Only the root component is swept and checked for blocking collision, child components move without sweeping. If collision is off, this has no effect."

Pour que cela marchen il faut prendre en effet les collisions, par défaut c'est en mode Overlap. Il faut aussi activer block pour pouvoir avoir les collisions :
![image](https://user-images.githubusercontent.com/58773222/189485822-5e532517-ac1b-40f9-98f8-802086e73b1e.png)


## Rotation
Pour la Rotation, on utilise la fonction équivalente que pour la position AddActorLocalRotation qui prend en parametre un FRotator. Cela tourne un acteur par rapport à son référentiel Local (encore une fois, pas par rapport au monde ce qui est bien).

Un FRotator est la variable pour la rotation, elle permet d'avoir les rotations en degrée avec Pitch (Y), Yaw (X), Roll(Z) avec un fonctionnement en Quaternion en background (Surement?).
Valeur de base : FRotator::ZeroRotator

## BakedIn Movement

### AddMovementInput
C'est une fonction existante dans Unreal, elle a la signature suivante :

AddMovementInput(FVector WorldDirection, float ScaleValue, bool bForce)

WordlDirection est le vector de Direction par rapport au monde contrairement à AddActorLocalOffset
ScaleValue correspond à la vitesse, à quel point on scale le Vector
bForce permet de forcer un déplacement.

Cela se combine bien avec ces fonctions :

* GetActorForwardVector Vector Forward
* GetActorRightVector vector right
* IsMoveInputIgnored qui permet de savoir si les inputs du joueur sont ignorés

Pour la rotation, on utilise :

* AddControllerPitchInput: Axe Y haut en bas
* AddControllerRollInput: Roule en mode Boule qui roule
* AddControllerYawnInput : Horizontal


## Extra

### Autres fonctions Unity

* TEXT permet de générer un FNAME par rapport à une string

### Debugging 

```
UE_LOG(LogTemp, Warning, TEXT("Non"));
UE_LOG(LogTemp, Warning, TEXT("The float value is: %f"), YourFloat);
UE_LOG(LogTemp, Warning, TEXT("The integer value is: %d"), YourInteger);
UE_LOG(LogTemp, Warning, TEXT("The vector value is: %s"), *YourVector.ToString());
GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Red, TEXT("This is an on screen message!"));
GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Red, FString::Printf(TEXT("Some variable values: x = %f, y = %f"), x, y));
```

https://unrealcommunity.wiki/logging-lgpidy6i

| Verbosity Level | Printed in Console? | Printed in Editor's Log? |                      Notes                       |
|-----------------|---------------------|--------------------------|--------------------------------------------------|
| Fatal           | Yes                 | N/A                      | Crashes the session, even if logging is disabled |
| Error           | Yes                 | Yes                      | Log text is coloured red                         |
| Warning         | Yes                 | Yes                      | Log text is coloured yellow                      |
| Display         | Yes                 | Yes                      | Log text is coloured grey                        |
| Log             | No                  | Yes                      | Log text is coloured grey                        |
| Verbose         | No                  | No                       |                                                  |
| VeryVerbose     | No                  | No                       |                                                  |

## Optimization

Les Fnames sont 2 fois plus léger qu'un string, ils sont donc préférables quand on peut s'en servir
