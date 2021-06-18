# Vecteurs


## Distinction

Un vecteur est différent d'un Scalaire (Scalar). Un scalaire symbolse une quantité comme le temps ou la temperature, il a une magnitude mais pas une direction contrairement à un Vecteur

## Scalaire

On peut imaginer le principe comme un droite où chaque valeur est un point sur cette droite. Un point peut etre un entier ou un décimal allant de -oo à +oo.

### Direction

Le concept de direction peut s'appliquer à un monde à un dimension. On peut avoir une direction de -1 ou de 1 (soit à gaucher soit à droite), ce qui nous donne le **signed distance** qu'on peut traduire par sign(x). 
La direction peut aussi être à 0 dans le cas d'un élément statique.

Dans certains cas, quand on veut manipuler une direction par exemple, on peut passer 0 à 1 pour éviter les problèmes liés aux multiplications/divisions par 0,
car cela n'aura aucun impact sur la direction.


### Longueur / Distance

La longueur ou Magnitude est la valeur absolu du vecteur. Elle ne peut pas être négatif contrairement à la signed distance.

La longueur entre 2 points, c'est à dire la distance entre 2 points se calcule de la manière suivante :

distance(a,b) = abs(a - b) // Dans le cas de Vecteur2, Vecteur3,... Chaque élément est sosutrait à l'élément correspondant, exemple :

a - b = (a.x - b.x, a.y - b.y)

Dans le cas de la distance, il n'y a pas d'ordre de soustraction car la distance est la même dans un sens ou dans l'autre.

Nuance de langage, la distance est ce qui sépare 2 points alors que la longueur ou la magnitude concerne un seul point.

### Traduction du type d'opération

Soustraction/addition correspondent à un offset du vecteur (Ajout ou retrait au vecteur)

Division/multiplication corespondent à un scaling du Vecteur

## Vecteur2 & Vecteur 3


Pour faciliter la compréhension, on utilise des couleurs pour chaque axe :

Axe X (horizontal, abscisses) est en rouge
Axe Y (Vertical, ordonnées) est en vert 
Axe Z (Profondeur, applicate) est en bleu

La plupart des Game Engine sont gauchers contrairement aux mathématiques :

![Schema_Gaucher](/img/Math/LeftHandedAxis.png)

