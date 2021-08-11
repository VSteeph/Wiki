## Unsafe
Unsafe signifie principalement qu'il n'y a plus de management de la mémoire automatique. C'est utile pour travailler avec des langages qui n'ont pas cette fonctionnalité comme le C ou le C++

Pour cela, il suffit de créer un bloc unsafe, de créer une fonction ou une classe avec le keyword unsafe

```
public void RandomFunction() {
  unsafe {

  }
}

public unsafe void RandomFunctionBis() {

}

public unsafe class RandomClass() {

}
```

Il faut aussi autoriser le code unsafe auprès du compiler.
1. Solution Explorer => Properties
2. Build tab
3. Check box "Allow unsafe Code"

OU
/unsafe en command line

Le cadre unsafe permet d'utiliser les pointers comme type de variable. Ils sauvegardent la memory adress d'un objet. Cela s'approche des références mais ils contiennent une adresse brute et ne sont pas gerés par le garbage collector qui maintient les références.

Cela suit les opérateurs de C++

```
int* p; // int pointer * => indirection operator
int* pointerToX = &x; // & adress operator Créer un pointer de la varaible x
*pointerToX = 3 // change la valeur
pointerToX->GetTypes(); // -> Member access operator to access member through pointer
```

### Mettre en mémoire dans le stack
Dans le cas d'un Array (int[10]), il y a 4 bits qui sont alloués dans le stack lors de la création de la référence. lorsque, new int[10] est appelé pour créer l'array, 40bits sont alloués dans le heap car c'est une reférence. Une fois que la frame est terminée, la référence est clean, donc les 4 bits sont liberés immédiatement mais les 40bits du heap sont laissés un peu plus longtemps et s'il n'y a aucune référence à ce tableau, la mémoire sera liberée.

Dans des cas de limitations de mémoires, il est possible de stocker un tableau dans le stack et non dans le heap, ce qui permet de libérer la mémoire immédiatement. Cela est possible avec le mot clé stackalloc
```
public unsafe void DoStuff()
{
  int* numbers = stackalloc int[10]; // à la fin de la fonction, les 40 bits seront instantanement liberés
}
```

### Fixed
#### Block Fixed
Il est important de garder en considération que les éléments gerés par le garbage collector et ceux en code sont difficilement compatibles, car le GC déplacent des éléments en maintenant les références à jour, mais il n'actualisera pas les pointers. C'est pour cela que l'on peut utiliser le mot clé Fixed pendant la durée du bloc

```
Point p = new Point();

fixed(double* x = &p.X) {
  (*x)++;
}
```
- le pointer doit être declaré dans le fixed statement
- on peut déclarer plusieurs pointers en les séparant avec une virgule
- Fixed statement peut être nested
- Cela ne dure que le temps du block

#### Keyword Fixed
En tant que keywardo, Fixed permet de bloquer la taille d'un tableau, car il est facile de recréer un tableau en C#, ce qui est impossible en C/C++

```
int[] numbers = new int[10];
numbers = new int[15];

fixed int numbers2[12]; // il ne pourra jamais changer de taille
```

### Utilise du code Native
Pour cela, il y a plusieurs mots clés lorsqu'on importe une dll en C#
```
public static class DllWrapper
{
  [DllImport("MyDll.dll", EntryPoint="add")]
  static extern int Add(int a, int b);
}
```
Extern permet de ne pas mettre de body car la méthode est définie ailleurs (library). Toutes les méthodes externs doivent être static. Enfin, l'entryPoint doit avoir le même nom que la fonction referencé.
