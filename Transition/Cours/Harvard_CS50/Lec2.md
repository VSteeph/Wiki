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

bool 1 byte
char 1 bite
Double 8 byte
Float 4 byte
int 4 byte
long 8 bytes
string ?bytes (varie)

## Mémoire
Quand on ouvre un fichier, un programme. Il est mis dans la RAM, c'est pour ça qu'on perd les informations quand on coupe le programme. C'est parce que c'est dans la mémorie volatile (mais plsu rapide).


