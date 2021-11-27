# Lecture 4 : Algo


## Running Time

Le temps qu'un programme met, le nombre d'itération, le temps. En général, on utilise le Big O Notation avec O(n) pour décrire le runing time d'un algorithme. (Log correspond à diviser par 2 encore et encore).

L'idée est de décrire la magnitude de la complexité du runing time mais pas de faire des formules compelexes, il faut qu'on comprenne rapidement la compelxité ex :
O(n) ou O(log(n)?

On se concentre surtout sur le dominant facteur. Par exemple O(n) ou O(n/2), c'est surtout O(n) qui nous intéresse comme log base 2 ou log base 7, on dira juste log(n)

Enfin, on a un dernier terme quand on a un algo qui a le même upper bound et lower bound qui ont la même compelxité, on peut dire theta(n) (ϴ)

Exemple de big Notation:

* O(n²) => Worst case
* O(n log n)
* O(n)
* O(log n)
* O(1) => Best case

Big O correspond aux temps le plus élévé possible, c'est à dire si c'est le dernier élément qu'on trouve, quelle sera la compelxité; ce qui s'oppose à Omega qui est le plus rapide possible.

On peut aussi analyser par "hertz", les CPU sont en Ghz donc 1 milliards d'opération. (Surtout rappeler que 1ghz c'est 1 milliard)

## Searching

### Linear Search

Cela correspond à une recherche élément par élément (linéaire) => O(n)

### Binary Search

C'est possible quand les recherches sont triés par ordre chronologique. Un binary search est le fait de prendre la moitié des informations et prendre la moitié inférieur et supérieur en fonction du chiffre.

Si on cherche 4 dans 1 à 10 :

* Milieu = 5, donc on prend de 1 à 4
* Milieu = 2, donc on prend 3 à 4
* Check 3, pas bon, c'est 4

Précision, en C on peut pas comparer des string avec == mais on peut faire strcomp dans string.h qui permet de comparer 2 strings (comparaison un par un des chac je suppose)

## Sorting

Le sorting est intéressant quand on commence à arriver des données qui ont une certaine quantité parce que faire du code complexe pour ordonner puis faire une recherche pour faire le meilleur algorithme alors que la différence sera minimale à l'échelle d'un ordinateur.

Le temps humain est plus important TANT que le temps machine n'est pas un blocage. L'optimisation se fait par la suite. Après, si on sait qu'on va process des milliers, des millions des lignes, on sait qu'on aura à l'optimiser des le début.

Le tout est un équilibre entre le temps humain, le temps machine et la mémoire utilisée.

### Selection Sort

On compare l'élement le plus bas puis en le comparant à tous les elements, puis le second le plus bas qu'on compare à n-1, ce qui nous donne uen complexité de 
O(n(n+1)/2) 

n + n-1 + n-2 +...+1  = n(n+1)/2 = (n²+n)/2 = n²/2 =n/2

donc pour résumer, on peut dire O(n²) si on veut rester dans la grande ordre de choses (et donc pas bien).

Le probleme de Selection Sort c'est qu'en terme de lower bound pour le running time, c'est la même durée que l'upper bouard (omega = Big O)

### Buble Sort

On compare le chiffre avec le suivant (s'il existe) et on inverse leur position, s'il sont dans le mauvais ordre. Le plus haut chiffre va toujours arriver à la bonne position, donc on peut diminuer de 1 ausi le nombre de chifre à comparer apres chaque itération.

C'est à dire qu'on fait n => n -1 => n-2 (etc, comme pour le selection sorting) sauf que le buble sorting marche beaucoup mieux avec le lower bound qui est à Omega(n), ce qui le rend plus efficace.

Pour le upper bound, on al a complexité suivante :
(n-1) x (n-1)
(n² - 1n - 1n +1
ce qu'on peut donc traduire par O(n²) en gros

cela veut dire que dans l'upper bound, Le Selection & Bubble sort sont asymptotiquement (asymptoically) simialrie

### Merge Sort (Recursion)

La capacité pour une fonction de s'appeler elle même. 

Le merge Sort c'est le fait de sort la première moitié et l'autre moitié des données puis de fusionner les 2.

Une fois qu'on arrive à 2 arrays triés, on compare les éléments le plus bas de chaque tableau et on recupère le plus petit, puis on continue jusqu'à avoir un tableau trier.

Comme pour le Binary Search, on divise le nombre d'éléments par 2 jusqu'à avoir un seul élément, à partir de la cet élément est trié puis on refusionne petit à petit en comparant élément par élément comme vu ci-dessus.

6 3 8 5 ==> 6 3 // 8 5 ==> 6 / 3 / 8 /5 ==> 3 6 / 5 8 ==> 3 5 6 8
                           
Pour la derniere étape, on compare le 3 avec le 5, c'est le 3 qui est plus petit, puis les 2 éléments les plus petits sont 6 et 5, c'est le 5 qui est le plus petit, puis les 2 éléments les plus petits sont 6 & 8, c'est le 6 le plus petit.

ce qui nous donne un upperbound et un lower bound de la même compléxité qui est O(nlog(n)) mais EN echange, cela a un prix, c'est que cela prend plus de mémoire.

## Struct

En C, on peut déterminer une struccture (data structure) qui est une composition de plusieurs values ex :

```C
typedef struct // type de la structure
{
  string name; // valeur
  string number;
}
person; //Nom de la structure

// cela s'utilies comme ça apres

int main(void)
{
  person people[2];
  people[0].name = "john";
  people[0].number = "123";
}
```

Value type?
