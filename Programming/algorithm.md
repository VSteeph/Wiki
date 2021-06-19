# Algorithmes

## Measurer l'efficacité/vitesse

Cela ne se mesure déjà pas par rapport à la vitesse en temps car tous les ordinateurs et les utilisations sont variés. Un algorithm se mesure d'une façon uniforme : Big O notation. Cela mesure la complexité Asymptotique d'un programe. C'est à dire déterminer l'augmentation de la vitesse de l'execution d'un programme quand la taille de l'input augmente vers l'infini (augmentation Asymptotique).

En gros, à quel point un algorithm va scale avec de la donnée.

Par exemple, trier un array d'une taille de 10, 1000, 1 millions, quel est l'évolution du runtime du programe.

Compter le nombre de lettres dans une string :

- Façon la plus simple, caractere par caractere et ajouter 1 à chaque caractere. Cet algorithm s'execute dans un temps linéaire basé sur le nombre de caracteres "n", donc O(n). L'augmentation du nombre de caractere est linéaire avec l'augmentation du runtime du programe.
- Si on store le nombre de caractere dans une variable Length au moment de la création de la string, savoir le nombre de caractere dans une string, il suffit de regarder la variable. Acceder la valeur d'une variable est considéré comme une opération constante asymptotique, c'est à dire 0(1). c'est à dire que le programme s'executera en constant time par rapport à l'input size.

La 2eme façon ne signifie pas que le code s'execute en 1 étapes, mais peu importe la taille de l'input, il n'y aura pas d'impact.

### Types d'asymptotique complexité
- O(n)², c'est tres lent et comme c'est exponentiel, cela tend à prendre beaucoup de temps. Cela pose problème principalement dans le Big Data mais pour des petites tailles d'input, il y a peu/pas de différence avec O(n) car il y a un build up de la fonction.

- O(log n), c'est illustré par trouver un élément dans un tableau trié (Binary search algorithm qui consiste à diviser un tableau en 2), cela veut dire que pour n = 8, cela donnera 3 itérations et pour n = 16 cela donnera 4 itérations.

- O(2^n) : plus lent algo possible quand on travaille avec la donnée

Ces types sont utilisés pour 2 façons : upper & lower bounds qui permettent de donner le temps minimum et le temps maximum qu'un algorithm peut mettre.

Le plus de temps : Big O => O( log n) => Binary search
Le moins de temps : Omega => Ω(1) => Binary Search
Quand les 2 cas sont équivalent : Theta => θ(1) => 2eme cas pour compter le nombre de caracteres dans une string

## Types d'Algorithmes
La force d'un algorithme dépend des besoins de l'utilisateurs, cela peut être la vitesse, la mémoire, la rapidité de coder. Il y a plusieurs types d'algorithm pour le même problème en fonction des besoins du programmer

### Sorting
Prenons comme un exemple, le fait de trier une liste de prix

#### Selection Sorting
C'est le cas où on test tous les éléments entre eux pour avoir le plus petit chiffre, il est placé au début de l'array puis le plus petit des éléments restants, en augmentant l'index toujours de 1. C'est très rapide à côté mais peu performant. O(n!)

#### Merge Sort
L'idée est de split l'array en élement indivisible (1 element) puis de regrouper par 2 par 4 en les sortant à ce moment la. Cela donne O(n Log n) qui est beaucoup plus intéressant.

#### Bubble Sorting


#### Spaghetti Sorting

### Graph Search
Un graph est un réseau de point connecté par des lignes (un peu comme une carte avec des villes connectés par des routes). Chaque ligne a un coût ou un poids.

#### Brute Force
Calculer toutes les possibilités de tous les chemins possibles et prendre le plus petit. O(n!)

#### Classic version (dijkstra's algorithm)
On commence au début (0), il évalue le coût de chaque node pour s'y rendre à partir du point A. cela commence par le point avec la value la plus faible et on vérifie toutes les lignes pour avoir la prochaine valeur la plus petite.

Ce qui donne :
- N(0) = 0
- N(1) = 0 + trajet
- N(2) = 0 + trajet 1 + trajet 2

et tous les chemins qui ont un poids plus fort pour aller dans une ville sont abandonnées. O(n²)

Il a été amélioré par la suite pour arriver à 0(n log n + 1)
