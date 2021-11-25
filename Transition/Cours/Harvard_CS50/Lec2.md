# Lecture 1

## Make

Quand on compile un projet avec make dans cs50. On passe par le compiler "Clang". Pour utiliser directement clang, il faut ajouter des paramètres. Par défaut, si on fait juste :

clankg hello.c, on va avoir un a.out (pour assembly out) qui va être le programme compilé. On peut donc ajouter un argument(options, flags) comme :

-o pour output
clang -o hello hello.c // ce qui permet de compiler dans un fichier hello.c

-l pour linked des librairies
clang -o hello -lcs50 hello.c // ce qui inclue la librairie cs50

=> -lm pour mac librairie // -lc pour une librairie de crypto

Il y a plusieurs étapes dans la compilations

* Preprocessing : On prend le source code tous les indicateurs de preprocessing (souvent celles qui commencent par #). Exemple #include va prendre le contenu du fichier et le mettre à la place de l'include

* Compiling: On transforme le C code en Assembly qui est le langage des CPU (Chaque CPU a sa propre façon d'implémenter l'assembly, c'est pour ça qu'on passe par l'assembly)

* Assembling: On Transforme l'assembly en Binaire pour qu'il soit executé par le CPU selon les regles données par l'OS/CPU

* Linking : On ajoute les librairies à ce soruce code (qui sont déjà en dll donc en binaire) et regroupe tout pour avoir un programme. 


## Debug

Il y a l'outil sur cs50 qui est debug50. Il est basé sur GDB (GNU debugger) qui est un outil utilisé et qui permet de plus facilement débugger que juste printf. Cela permet d'avoir un debugger step by step, en gros un debugger (avec BreakPoint, etc)

debug50 ./mario

## Data

* bool 1 byte

* char 1 bite

* Double 8 byte

* Float 4 byte

* int 4 byte

* long 8 bytes

* string ?bytes (varie)

## Mémoire
Quand on ouvre un fichier, un programme. Il est mis dans la RAM, c'est pour ça qu'on perd les informations quand on coupe le programme. C'est parce que c'est dans la mémorie volatile (mais plsu rapide).

Cela signifie que si l'on dépasse la mémoire d'une variable par exemple, un tableau avec un element non indexé, on va accéder à une autre valeur en mémoire qui peut être lié au programme mais aussi à un autre programmme et faire crash l'ordinateur.

## Array

int scores[3]; comme dans les autres langages et avec l'index pour attribuer la valeur scores[0] = 72 et pour avoir un parametre en array c'est dans ce format :

float average (int length, int scores[]);

En C, les arrays n'ont pas de fonctionnalités. Ils n'ont pas les points comme Length ou autre comme en C# donc scores.length ne marchera pas, il faut passer la length dans les fonctions et garder la variable.

## Const

Si on va utiliser une variable plusieurs fois sans avoir à la copier ou à l'envoyer et qu'on ne changera pas. On peut la déclarer comme une constance :

const int total = 5 (par exemple) Cela permet de protéger le code pour éviter de changer une variable.

Par convention, elles sont écrites en Majuscules =>

const int TOTAL = 5;

## Character

Les caractères ont des valeurs numériques (Ascii par exemple), donc en C, un character est aussi un chiffre. Par exemple

printf("%i \n", c) va donner sa valeur numérique
printf("%c \n,c) va donner le "visuel

Charactere = Single quote ''  et les strings = double quote ""

## String

Il n'y a pas de string en C mais tous les langages ont une façon de représenter des strings. Un string n'est rien d'autre qu'un array de character. Une string est un peu plus développée qu'un array mais c'est le concept.

Les strings ajoutent un autre caractère à la fin d'un string qui est \0 pour dire que c'est la fin d'un string (EOF) et qui a la valeur numérique 0 => 00000000 (byte) donc chaque string prend un byte de plus.

Le 0 est la pour arrêter le string et éviter de modifier ou de récupére d'autres éléments dans la RAM qui peut être dangereux, il faut faire attention en C.

## For

La condition est n'importe quel boolean, donc ça veut dire qu'on peut faire

for(i =0; i < 5; ++i) ou à la place du i mettre i ==5 ou i != 5 ou une autre variable genre s[i] == '\0'
