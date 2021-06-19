# Data Structured
Arrays, List ou structures selon les langages. Il y a des spécificités selon les types et les langages. Ce sont à la base de beaucoup chose comme les strings, le dernier character permet de stop la string.

Il est aussi possbile de créer des multidimensional Arrays, c'est à dire une grille (Colonne + ligne), on appelle ça une matrix (grosso modo, un array d'array). On peut avoir des matrices d'autant de dimensions, chaque dimension étant uen couche d'array.

## Arrays
Un array est un chunk continu de mémoire, qui est divisible en élément de même tailles qui sont referencés par des entiers continus (1 based ou 0 based index, c'est à dire qui commence 0 ou à 1, en général 0)

L'avantage est qu'on peut accéder à tout moment à n'importe quel élément d'un array. C'est possible en calculant la prochaine adresse.

On prend l'adresse de l'array et on ajoute la taille de l'element * l'index, ce qui donne
```
array_addr + elem_size * (i - first_index) // ce qui permet d'avoir une base 1 ou 0
```
C'est pour cela qu'on utilise des éléments à même taille.

### Multi-Dimensional Arrays
Ce sont des tableaux dans des tableaux souvent écrit par int[x][y]. Pour calculer l'adresse, on utilise le même procédé mais à 2 échelles.

| 0,0 | 0,1 | 0,2 | 0,3 |
|-----|-----|-----|-----|
| 1,0 | 1,1 | 1,2 | 1,3 |
| 2,0 | 2,1 | 2,2 | 2,3 |

On selectionne déjà la colonne qu'on va utiliser avec la formule qu'on a vu précdemment et on fait de même avec le 2eme index

```
array_addr + elem_Size1 * (i - first_Index) + elem_Size2 * (y - first_Index);
```

Dans ce cas, on assume que tous les éléments sont après les autres, ça s'appelle le Row-Major order ou Row-major index.

D'autres compiler regroupent tous les index 1 puis tous les index 2, ce qui donnerait:
- 0,0
- 1,0
- 2,0
- 0,1
- 1,1
- 2,1
- 0,2
- 1,2
- 2,2

Cela s'appelle Column-major order

### Times for common Operation
Les opérations de base comme lire ou modier sont de O(1), mais pour ajouter ou enlever, c'est différent.

Pour ajouter un element à la fin, on ajoute le nombre d'éléments donc 0(1) et pareil pour enlever le dernier.

Pour enlever le premier ou ajouter le premier, cela nécessite de tout restructurer, c'est donc 0(n) afin d'éviter les trous

|           | Add    | Remove |
|-----------|--------|--------|
| Beginning | O(n)   | O(n)   |
| Middle    | O(n) ? | O(n) ? |
| End       | O(1)   | O(1)   |


## Struct
Quand on a besoin de stocker plusieurs types de variables, on peut utiliser des trucs

## LinkedList
Une linkedList est constitué de Node qui est une struct ayant uen variable et un Pointer qui dirige vers la node suivant, cela permet d'avoir une liste dynamique.

Elles peuvent être circulaires, lorsque la derniere pointe sur la première ou elle peut être terminer en mettant le pointer à 0. Elles sont beaucoup plus simples à modifier, re-organiser. Elles consoment plus de mémoire en échange).

Beaucoup de data structures sont construites sur les LinkedList comme les queues et les stacks.

### Queues
First In, First Out. (queue in,dequeueing)

### Stacks
Last In, First Out. (Pushed in, poped out)

### trees
Cela fonctionne comme une LinkedList mais avec 3 pointers pour avoir 2 variables pour créer un arbre (Binary Tree). Il est possible d'avoir plus que 2 variables par nodes en modifiant le nombre de pointer (changeant la struct)

### Graph Data
Ce sont des nodes qui peuvent se connecter entre eux, il n'y a pas de lien de parenté.
