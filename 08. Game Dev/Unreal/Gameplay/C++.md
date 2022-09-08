# C++ In Unreal

Documentation Unreal : https://docs.unrealengine.com/5.0/en-US/

## Ereurs Possibles
Bug quand on ajoute des éléments dans un dossier et ils sont pas pris en compte dans l'Engine. Pour corriger ce bug, on ouvre le content Drawer => Ouvrir dans l'exporeur => Ouvrir la solution => Enlever le nom du dossier dans le #include de la classe.

Rebuild le projet et le relancer


## Créer une nouvelle Classe (assimilée à un Blueprint, ceux d'Unreal)

Les éléments de code sont dans le Dossier C++ Classes sur Unreal dans le Content Drawer et clique droit New class.

Il faut choisir la classe parent (héritage) en suite, voici les principales (il en existe énormement)
* None : Classe classique
* [Actor](https://docs.unrealengine.com/5.0/en-US/unreal-engine-actors/) : C'est un objet qui peut être placé ou spawn dans le niveau, ils peuvent être crées et détruits
* [Pawn](https://docs.unrealengine.com/5.0/en-US/possessing-pawns-in-unreal-engine/): c'est un Actor qui peut être contrôlé et recevoir des inputs comme une voiture
* [Character](): C'est un Pawn qui peut marcher / Se déplacer.

La hiérarchie est donc AActor => APawn => ACharacter.

En gros, Actor si c'est pour le monde, Pawn si c'est ça peut être possédé par une IA ou le joueur ou intéragit et enfin character si y a du déplacement


## Implémenter dans le Monde
On peut ajouter une classe dans le monde avec un drag mais cela servir à rien, il faut l'associer à un blueprint

