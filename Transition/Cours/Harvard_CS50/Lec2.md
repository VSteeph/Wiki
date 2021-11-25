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

et évidemment, on peut avoir des arays dans des arrays avec int[][][]

## Const

Si on va utiliser une variable plusieurs fois sans avoir à la copier ou à l'envoyer et qu'on ne changera pas. On peut la déclarer comme une constance :

const int total = 5 (par exemple) Cela permet de protéger le code pour éviter de changer une variable.

Par convention, elles sont écrites en Majuscules =>

const int TOTAL = 5;.

## Character

Les caractères ont des valeurs numériques (Ascii par exemple), donc en C, un character est aussi un chiffre. Par exemple

printf("%i \n", c) va donner sa valeur numérique
printf("%c \n,c) va donner le "visuel

Charactere = Single quote ''  et les strings = double quote ""

## String

Les strings sont dans <string.h>

Il n'y a pas de string en C mais tous les langages ont une façon de représenter des strings. Un string n'est rien d'autre qu'un array de character. Une string est un peu plus développée qu'un array mais c'est le concept.

Les strings ajoutent un autre caractère à la fin d'un string qui est \0 pour dire que c'est la fin d'un string (EOF) et qui a la valeur numérique 0 => 00000000 (byte) donc chaque string prend un byte de plus.

Le 0 est la pour arrêter le string et éviter de modifier ou de récupére d'autres éléments dans la RAM qui peut être dangereux, il faut faire attention en C.

## Caractere & String

Le fait que les characteres sont des chiffres permettent de facilement les manipuler. Par exemple, on peut transformer des caracteres de minuscules en majuscules. Si on prend la table ASCII, on voit qu'il y a un décalage de 32 entre la minuscule et la majuscule, ce uqi permet de faire ça :

``` C
for(int i =0, n =strlen(s); i<n; ++i)
{
  if(s[i] >='a' && s[i] <= 'z')
  (
    printf("%c", s[i] - 32);
   )
}
```

Cette fonction existe déjà dans <ctype.h> comme : islower pour savoir si le caractere est une minuscule, ainsi que toUpper pour transformer en caractere en Majuscule.

## For

La condition est n'importe quel boolean, donc ça veut dire qu'on peut faire

for(i =0; i < 5; ++i) ou à la place du i mettre i ==5 ou i != 5 ou une autre variable genre s[i] == '\0'

sachant que la condition va être itéré à chaque itération donc ça sert à rien de mettre une fonction comme strlen qui va parcourir la string plein de fois et augmenter la compelxité.

On peut donc déclarer la variable strlen avant ou l'utiliser dans le for dans la partie "déclaration" qui est la premiere partie :

for (int i = 0, n = strlen(s); i < n;i++)

## Main

La fonction main peut aussi prendre des inputs qui corresponderont à des arguments dans l'executiion du programe comme

int main(int argc, string argv[]) ou argc est argumentCount donc le nombre d'argument qui vont être renseigné et argv pour la liste des arguments. et argv est argument vector

argc est renseigné automatiquement par le programe et c'est le nombre de mot dans la commande (Y COMPRIS LE nom du programme) donc

./hello john => cela va donner 2 arguments => argv[0]qui est le nom du programme et argv[1] qui est john

Main retourne aussi un type int qui permet de donner un exit status pour dire comment le programme s'est arrêté ex return 1

## Cyrptographie

Cela permet de transformer des informations avec une clé en d'autres informations qui sont codés mais plus dur à comprendre

## Variable

La plupart des variables en C sont en valeur quand elles sont en locales, donc le callee (celui qui reçoit la fonction) ne modifie pas la valeur de la varaible dans le caller
