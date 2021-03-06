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


### Longueur ou Magnitude & La distance

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

Un moyen simple de se representer un vecteur est de s'imaginer une fleche allant de l'origine (0,0) au point donné (x,y). Le vecteur peut donc signifier beaucoup de chose comme : 
* la distance
* Les coordonnées
* La direction
* Le mouvement

Les additions sont commutative (cela signifie qu'on peut inverser l'ordre des éléments) mais pad les soustractions, ni les divisons. Les multiplications peuvent l'être sauf dans le cas de matrices et de quaternion.

### Cacluler La longueur d'un vecteur

La magnitude d'un vecteur se calcule simplement. Pour cela, on utilise le théorème de Pythagore. Il est facile de créer un triangle rectangle avec l'abscisse et l'ordonéne. Le vecteur correspond à l'hypothénuse de ce triangle : 

<img src="/img/Math/Pythagore.png " width="100" height="140">

Exemple avec le vecteur(4,5) :

=> Sqr(4² + 4²) => sqr(16+9) => Sqr(25) => une longueur de 5

Le principe reste identique peu importe le nombre de dimension, c'est à dire qu'un vecteur3(2,3,4) aura comme longueur :

Sqr(2² +3² + 4²) (envion 5.3)

### Calculer la distance entre 2 vecteurs (Displacement entre 2 vecteurs)

Pour calculer le vecteur entre 2 vecteurs, il suffit de soustraire un vecteur au second :

VecteurA - VecteurB OU VecteurB VecteurA puis on calcule la longueur de ce vecteur comme vu ci-dessus.

Lorsqu'on veut comparer la distance entre 2 éléments, on peut garder l'élément au carré pour gagner en performance. C'est à dire faire le SqrMagnitude comme ceci:

Magnitude = X² + y²`

### Unit Vecteur (Normalized)

Les directions sont toujours des units vecteurs avec une longueur de 1. L'ensemble des possibles peut être signifier par un cercle avec un rayon de 1.

Transformer un vecteur à un vecteur avec une longueur de 1 est le processus de normalisation. On garde la direction mais pas le scale. Cela permet de manipuler plus facilement une direction pour lui donner une vitesse précise

Pour normaliser un vecteur, il suffit de le diviser par sa magnitude comme ceci:

Vecteur(x,y)/magnitude => (x/magnitude, y/magnitude), il est donc logique qu'on ne peut pas normaliser un vecteur qui a une longueur de 0 ou alors on retourne 0 sur tous les axes.

On peut aussi normaliser un vecteur étapes par étapes plutôt que d'utiliser les fonctions de la librairie pour récupérer la longueur et donc limiter le nombre de calcul/

### Displacement & Direction

C'est le vecteur qui permet d'aller de A à B. Il est donc différent de B vers A. Il s'obtient comme pour la distance, mais il y a un ordre précis selon le sens dans lequel on veut aller. Les éléments sont dans le sens inverse de le phrase, c'est à dire :

Pour obtenir le vecteur pour aller de A vers B, il faut faire B - A

Pour obtenir le vecteur pour aller de B vers A, il faut faire A - B

### Dot Product

Il y a plusieurs façons de multiplier les vecteurs:
* Dot Product
* Cross Product
* Component Wise

#### Component Wise
C'est pour scale un vecteur, on multiplie chaquun des components par le composant correspondant :

(a,b) \* (c,d) = (a \* c, b \*d)

#### Dot product
on peut appeller ça une projection Scalaire. C'est l'idée de projeter un vecteur sur le second. C'est representé par le fait de tracer une droite (angle droit) entre le point A et la droite de la direction de A. Le résultat est la longueur (signed distance car ça peut négatif) entre l'origine et le point.

<img src="/img/Math/Dot_Product.png " width="250" height="150">

Pour fonctionner, il faut qu'au moins une valeur soit normalisé et potentiellement les 2. Lorsque les 2 sont normalisés, plus le Dot product tend vers 1, plus les vecteurs pointent dans la même direction et plus il tend vers -1 plus ils sont oppoés, tandis qu'à 0, ils sont perpendiculaire.

<img src="/img/Math/Dot_Product2.png " width="250" height="150">

La formula est la même que celle pour calculer le SqrMagnitude :
dot(a,b) = (a.x * b.x + a.y * b.y)

Ce processus de projection permet aussi de transformer un vecteur sur un autre vecteur et donc un autre espace.

Le fait d'avoir un des 2 vecteurs non normalisés a certaines utiltiés aussi, exemple :

Une balle rebondit sur une surface et on veut savoir le volume du son d’impact. Plus la balle va vite, plus on veut que le son soit fort, et on veut aussi prendre en compte l’angle de l’impact.
On prend donc la normale pour avoir la direction de la surface et on fait le dot product du vecteur de la balle. On veut donc uniquement avoir la normal de normaliser pour pouvoir garder la vélocité du vecteur de la balle pour avoir une valeur plus importante.

#### Cross Product

Cross(VecteurA, VecteurB) retourne un vecteur perpendiculaire aux 2 fournis (sauf si les 2 sont dans la même direction). Par exemple, si on donne transform.forward & transform.up, cela va donner transform.right.

Par exemple, cela peut permettre d'obtenir la droite ou la gauche de la normal d'un objet et le forward du joueur. Si on veut une direction, il faut normaliser les 2 vecteurs (sauf si les 2 vecteurs fournis sont parfaitements perpendiculaires)

L'ordre impacte la direction du résultat.

## Spaces

Par défaut, on considère qu'on est dans une espace Orhographique, c'est  àdire que les axes X & Y sont perpendiculaires.

L'espace est le référentiel que chaque vecteur répresente. Par défaut, c'est l'origine du monde (0,0) mais un vecteur peut etre dans le referentiel d'un autre, c'est le concept de Parent-Enfants ou de World Space / Local Space.

Un espace est souvent représenté par les “Bases vector” (Vecteur de base) qui sont souvent normalisés et représentent les axes (équivalent de forward, right, up).

Selon le milieu on utilisera différent espace de base. Par exemple, un environnement 3D aura le World Space tandis qu'un Shader utilisera plutôt le Clip Space avec différentes couches :
Model Space => View Space => Projection Space => (Clip Space)

### Relativité des vecteurs

Un vecteur est relatif à son espace et à lui même. C'est à dire que si on veut ajouter ou enlever un vecteur à un autre, il faut le faire depuis celui la. C'est à dire.

Vecteur A + Vecteur B pour ajouter B au vecteur A ou encore transform.position+ transform.forward pour avoir la direction dans laquelle pointe un élément

### Convertir Un Vecteur entre

# Sources :  
https://www.youtube.com/channel/UC7M-Wz4zK8oikt6ATcoTwBA
