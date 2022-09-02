# C# features

## Yield keyword
Tous les IEnumerable peuvent être utiliser dans une foreach loop. En gros, cela permet d'examiner plusieurs valeurs dans un container/collection, une à la fois.

Application du yield keyword

```
class IteratorExemple : IEnumerable<int> {
  public IEnumerator<int> GetEnumerator() {
    for(int index = 0; index <10; idnex++)
      {
        yield return index;
      }
  }

  IEnumerator IEnumerable.GetEnumerator() {
    return GetEnumerator;
  }
}
```

Le yield keyword permet d'utiliser les foreach avec les IEnumerable. c'est à dire que la valeur est envoyé et la fonction est mis en "pause" contrairement à un return classique. La prochaine itération continuera au dernier index afin de parcourir toutes les valeurs du IEnumerable

Yield ne peut être utiliser que dans les méthodes qui return un IEnumerator<T> ou IEnumerable<T> et leur version non-generic

### Named iterators
Il est aussi possible de créer une method qui return un IEnumerable<T> et avoir plusieurs versions avec des comportements differents :

```
public Class Counter
{
  public IEnumerable<int> CountUp(int start, int end)
  {
    int current = start;
    while (current < end)
    {
      yield return current;
      current++;
    }
  }

  public IEnumerable<int> Countdown(int start, int end)
  {
    int current = start;
    while(current > end)
    {
      yield return current;
      current--;
    }
  }
}

Counter counter = new Counter();
foreach(int number in counter.CountUp(5,50))
{
  Console.WriteLine(number)
}

foreach(int number in counter.Countdown(50,10))
{
  Console.WriteLine(number)
}
```

## Constants
Une façon d'avoir une variable qui ne change jamais de valeur est d'utiliesr les keywords :
- Const
- readonly

C'est une sécurité pour être sur que personne ne change la valeur, c'est utile pour le GUID de la verison d'un logiciel (comme Visual Studio) par exemple. On peut donc déclarer ses variables en tant que const car une fois déclaré, ils ne changeront jamais. Une variable const est par défaut static.

La différence entre const et readonly est que readonly peut être assigné par la suite. Ce sont des runtime constants. C'est utile lors de constructors par exemple, si on veut donner un GUID à chaque nouvelle voiture.

## Attributes
Cela permet d'ajoute  de la metaData au code. Ils peuvent être ajoutés au types, paramètres de méthodes et return types. Les attributs peuvent être detectés par le compiler, external code tools, ou même le code en reflection.

Cela prend cette forme

```
[Obsolete]
private void DisplayFlashPlayer()
{  
}

[Obsolete("Utiliser la fonction DisplayNativePlayer", true)]
private void DisplayFlashPlayer(int width, int height)
{
}
```

Le True permet de signifier si le compiler doit considérer le message comme une erreur plutôt qu'un warning. Les attributs peuvent se cumuler
```
[Attribute 1]
[Attribute 2]
[Attribute 3]
public class SomeClass {

}
```

## NameOf operator
Cela permet d'avoir le nom de la proprieté utilisé. C'est en général une bonne pratique d'utiliser nameOf plutôt que d'écrire le nom de la proprieté car cela permet de changer le nom si nécessaire plus simplement.

Par exemple, dans une class "Book", on veut override le toString pour avoir une meilleure division

```
Class Book {
  public string title {get;set;}
  public string Author {get;set;}
  public int Pages {get;set;}

  public override string ToString() {
    // Façon 1 :
    return $"Book Title = {Title}, Author = {Author}, Pages = {Pages}"
    // Façon 2 :
    return $" nameof(Book) nameof(title) = {Title}, nameof(AuthorAuthor) = {Author}, nameof(Pages) = {Pages}"
  }
}
```

## sizeof Operator
Cela permet de récupérer la taille en bytes (8 bits) d'un type. Par exemple, sizeof(int) retourne 4 car c'est la taille d'un int. C'est pratique pour manipuler des bytes, on peut créer des byteArray

```
byte[] byteArray = new byte[sizeof(int) *4];
```
Une bonne pratique est de mettre sizeof(int) plutôt que 4 car cela explique le choix du chiffre 4

## Bit Fields
Il est facile d'oublier que les variables sont avant tout une allocation de mémoire à une valeur en bits. Il est intéressant donc d'utiliser les bits directement pour traduire des données. C'est tres utile dans les data fields.

Par exemple, pour gérer les droits sur un forum, plutôt que d'utiliser un bool qui prend un byte, il est intéressant d'utiliser des bits :

```
Not Used - 0
Account Suspended - 0
Can Create Threads - 1
Can Edit own Post - 1
Can delete other's post - 0
Can edit other's post - 1
Can vote on posts - 1
Can create posts - 1
```

Si on prend les permissions ci-dessus, cela nous donne 00110111 (un byte) avec toutes les permissions de chaque utilisateur. Cela peut aussi être traduit en code hexadecimal, en l'occurence 37. Dans cette situation, c'est le binaire qui nous intéresse car cela symbolise une série de bool representant les droits d'un utilisateurs.

Il est possible de stocker ces variables dans des ints avec des mots clés comme :
```
int binaryNumber = 0b00110111; // 0b
int hexaNumber = 0x37; // 0x
```

### bit shift operators
Il est possible de déplacer les bits d'un certain nombres vers la droite ou vers la gauche grâce aux operators << & >>
```
int result = 0b00110111 >> 2 // decale de 2 vers la droite, ce qui donne 0b00001101
int result = 0b00110111 << 2 // decale de 2 vers la gauche, ce qui donne 0b11011100
```

### Bitwise logical operators
Les operators en bits sont les versions mono de and et or, c'est à dire && => & et || devient |. Ces operators vont parcourir tous les bits un à la fois et vont dire 1 = true, 0 = false.

Par exemple,
```
01010101
11111111
```
avec le "&", cela va regarder chaque série de bits (haut et bas) et s'il y a un 0, cela donnera 0 car, on a pris and. Si, on avait pris or, il suffirait d'avoir 1 pour donner 1.

```
01010101 => Valeur A
11111111 => Valeur B
01010101 => AND
11111111 => OR

// Code
int a = 0b01010101;
int b= 0b11111111;

int combinedWithAnd = a & b // 01010101
int combinedWithOr = a | b // 11111111
```

Le dernier bit operator est XOR. Il retourne vrai si l'un est vrai MAIS pas l'autre, c'est exclusif. Exemple
```
01010101 => Valeur A
11111111 => Valeur B
10101010 => XOR

int combinedWithXor = a ^b;
```

Enfin, le dernier oéprator est ~ qui est le complement, c'est à dire que comme ! il donnne l'inverse, donc il prend les bits et donne leur inverse
```
int a = 0b01010101;
int complementA = ~a; // ce qui donnera 0b10101010
```

Enfin tous les operateurs ont equivalent comme +=, c'est à dire
```
int number = 0b00001101;
number <<=1; // number = number << 1
number >>=1  // number = number >> 1
number &= 16 // number = number & 16
number|= 20  // number = number | 20
number ^= 32 // number = number ^32
```

### Enumeration Flags
> tres bon exemple sur la doc Microsoft

 [Microsoft Doc](https://docs.microsoft.com/en-us/dotnet/api/system.flagsattribute?view=netcore-3.1)

 Cela permet d'utiliser les bits comme Enumerations :
 ```
[flags]
public enum ForumPrivileges
{
  CreatePosts = 1 << 0,    // 1   00000001
  EditOwnPosts = 1 << 1,   // 2   00000010
  VoteOnPosts = 1 << 2,    // 4   00000100
  EditAnyPosts = 1 << 3,   // 8   00001000
  deletePosts = 1 << 4,    // 16  00010000
  CreateThreads = 1 << 5,  // 32  00100000
  Suspended = 1 << 6,      // 64  01000000

  // comme dans la doc microsoft, on peut aller plus vite en faisant, le << sont la pour la démonstration
  None = 0
  BasicUser = CreatePosts | EditOwnPosts | VoteOnPosts,
  // cela permet de créer un basic user avec les valeurs suivantes
  00000001 - CreatePosts
  00000010 - EditOwnPosts
  00000100 - VoteOnPosts
  00000111 - Combinaison des 3 valeurs avec Or

  Administrator = BasicUser | EditAnyPosts | deletePosts | CreateThreads // ce qui donne 00111111
}
 ```
 C'est à dire qu'avec le shift, on peut avoir un seul bits à comparer et facilement savoir si la personne a les droits et on peut aussi attribuer des droits avec le | ou en enlever avec le XOR (XOR permet de toggle plus que d'enlever) :

```
ForumPrivileges privileges = ForumPrivileges.BasicUser;
privileges |= ForumPrivileges.Suspended;

00000111 - basic users
01000000 - suspended
01000111 - nouveau privileges avec OR

// inversement
privileges ^= ForumPrivileges.EditOwnPosts;
01000111 - etat des privileges del 'user'
00000010 - Edit Own post
01000101 - Nouveau privileges avec XOR
```

Enfin, & permet de savoir si un element est activé

```
bool isSuspended = (privileges & ForumPrivileges.Suspended) == forum.Suspended
01000111 - privileges
01000000 - Suspended
01000000 - resultat AND
```

## Reflection

C'est le fait d'inspecter des elements executables du code. Il est possible de savoir les types, méthodes, properties, variables d'une assembly même quand lep rogramme est cours. La reflection est le fait d'analyser la structure d'un code.

(Outil : Mono.Cecil pour manipuler des assembly, ILSpy pour les regarder)

## IDisposable interface
Par défaut, le GC s'occupe de libérer la mémoire. Parfois, les taches nécessite d'utiliser des ressources non-gerées par le GC. Par exemple, quand on ouvre un fichier, ce qui nécessite de close le stream (writer)

Les types qui utilisent de la mémoire "independante" vont implémenter une interface IDisposable qui a une method Dispose qui permet de nettoyer toute la mémoire que l'object utilise. La method close l'utilise (mais en cas d'exception, il est possible que le Dispose ne s'execute pas).

C# a mis en place une façon plus simple de faire ça, c'est le using statement

```
using (FileStream fileStream = file.OpenWrite("fileName"))
{
  //Do stuff
}
```

A la fin du block, la method dispose sera appelé même s'il y a une exception lors de l'execution du block, ce qui rend le processus plus safe.

## Preprocessor Directives
Ce sont des instructions pour le compiler dans le code, cela commence par #.

- #warning & #error permet de throw un warning ou une erreur lors de la compilation.
- #region & #endregion sont la pour regrouper les méthodes par thématiques (block dans VIsual Studio)
- #if, #else #elif, #endif sont des if statements qui sont basés sur les symbols (défini dans le CsProj), cela va permettre d'executer un code ou un autre selon la situation. (&& et || fonctionnent dans la condition)
- #define et #undef permettent de set ou unset des symboles

```
#define Debug
Console.WriteLine("Debug Has been set");

#if Debug
  Console.WriteLine("Running in Debug Mode");
#else
  Console.WriteLine("Running in release");
#release
```

## Nullable Types
Les variables de type value (à l'opposée des ref) ne peuvent pas être null. Cela peut être utile dans certain cas (comme un bool : Vrai, Faux, Uncertain)

Cela peut s'écrire de 2 façons
```
Nulaable<bool> isComingToTheWedding = true;
isComingToTheWedding = null;

// version simplifié
bool? isComingToTheWedding = true;

// Checking
if(isComingToTheWedding.HasValue)
  {
    bool actualValue = isComingToTheWedding.Value;
  }
```

Il y a aussi un moyen plus simple avec le null-coalescing operator "??"
```
bool actualValue = isComingToTheWedding ?? false;
```

A noter qu'un Nullable<T> ne peut pas être null. L'écriture "Null" se fait grâce au compiler.

## Null Propagation Operator
C# 6.0 a introduit les null propagation, succint null checking or the null propagator operator qui permet de gérer le null checking. Beaucoup d'éléments peuvent être null et devoir check pour chaque element est assez repétitif.

Imaginons ce genre de scene :
```
private string GetTopPlayerName() {
  if(highscoreManager == null) return null;
  if(highscoreManager.Scores == null) return null;
  if(highscoreManager.Scores[0] == null) return null;
  if(highscoreManager.Scores[0].Player == null) return null;

  return highscoreManager.Scores[0].Player;
  }
}
```

De la même manière que le nullable type, on peut utiliser ? pour ce qui peut être null :
- Conditional Member access Operator ?.
- Conditional Indexer access Operator ?[]

Cela se traduit par
```
return highscoreManager?.Scores?[0]?.Player?.Name;
```

Si le moindre élément est null, cela va return null et arrêter l'expression. C'est pour cela qu'il est important de faire gaffe au type de variable qui prend la valeur, car si c'est un value type, il ne peut pas être null à moins de l'avoir transformer en Nullable ou utiliser le Null Coalescing operator ??

```
int? score = highscoreManager?.Scores?[0]?.Score;
int score = highscoreManager?.Scores?[0].Score ?? 0;
```

Cela marche aussi avec les délégates avec le ?.Invoke qui permet d'avoir le même comportement mais pour les methodes.

## Transformer un programme en commande
Cela peut se produire grâce au string[] args dans Main, Exemple

```
static void Main(string[] args) {
  int a = Convert.ToInt32(args[0]);
  int b = Convert.ToInt32(args[1]);
  Console.WriteLine(a + b);
}
```

## Value Conversion
Il est possible de cast des variables sur un autre type (implicit int vers double) ou explicite. Il est aussi possible d'instaurer des conversions entre des types custom.

```
public class MagicNumber
{
  public int Number { get; set;}
  public bool IsMagic {get;set;}

  // Override de MagicNumber à Int
  public int ToInt()
  {
    return Number
  }

  // override de Int à Magic Number (static)
  public static MagicNumber FromInt(int number)
  {
    return new MagicNumber{Number = number, IsMagic = false};
  }

  // Implicit conversion (static  & public forcé)
  public static implicit operator MagicNumber(int value)
  {
    return new MagicNumber() {Number = vbalue, IsMagic = false};
  }
}
```

On peut déterminer implicit ou explicit (les 2 mots clés existent), on a choisi implicit ce qui permet de faire ça
```
int aNumber = 3;
MagicNumber magicNumber = aNumber;
```

La version explicite ressemblerait à ça
```
static public explicit operator int(MagicNumber magicNumber)
{
  return magicNumber.Number;
}

MagicNumber magicNumber = new MagicNumber() { Number = 3, IsMagic = true};
int aNumber = (int) magicNumber;
```

## Goto keyword
Une des rares utilisations de goto est pour sortir de nested loops et cela prendrait ce genre de forme car cela permet de couper court à une série de loops
```
while(x < 100)
{
  while(y < 100)
  {
    while(z <100)
    {
      if(thing==otherThing)
      {
        getOtherThing;
        goto Found;
      }
    }
  }
}
goto End;
Found:
  Console.WriteLine("Thing is OtherThing");

End:
  Console.WriteLine("thing is not OtherThing");
```

De preference, c'est mieux de pas les utiliser ou de se limiter à ce rare cas et ne pas les multiplier.

## Generic Covariance and Contravariance

Lors de l'héritage, on peut mettre la classe dérivé en tant que classe parent. Cela s'explique car le dervié est aussi la version de base. Un carré est un rectangle.
```
public class GameObject
{
}

public class Ship : GameObject
{
}

GameObject newObject = new Ship();
```

Il est important de noter que cela a des limites, par exemple dans les list. Exemple :
```
List<GameObject> objects = new List<Ship>();
objects.Add(new Asteroid());
```

Cela poserait des problemes car on aurait une liste de Ship avec des asteroides.

En C#, on contrôle le transfert de hierarchie vers un type generic qui l'utilise. Cette regle qui contrôle si et comment la relation est appliqué s'appelle la variance

Pour définir un generic type, on peut mettre plusieurs parametres
```
public interface IGeneric<T1,T2>
```

Le premier parametre est l'invariance, et c'est par défaut. Cela signifie que l'héritage est completement ignoré.

Le second est la covariance, cela signifie que l'héritage est conservé.
```
Covariant<GameObject> thing = new Covariant<Ship>();
```
Cele sert uniquement à servir de return values pour des méthodes. Cela ne peut pas servir d'input car c'est prône à l'erreur. C'est pour cela que le .Add d'une liste ne fonctionne pas, car cela prend un input.

Par contre, IEnumerable<T> est covariant qui permet d'iterer sur une collection.

La derniere option est la Contravariance, elle invere l'héritage.
```
Contravariant<Ship> thing = new Contravariant<GameObject>();
```

Plus d'information sur C# Player guide p290

## Advanced NameSpaces
Il est possible d'avoir des situations amibuges, souvent liés à une mauvaise appelation. Par exemple, avoir un NameSpace System.Console et une classe Systeme qui a une methode console.

Lorsque c'est pas possible à éviter (Librairies externes ou autres), il est possible de créer des global keywoard avec l'operator (::) comme :
```
global::System.Console.WriteLine("thingy");
```

le global:: signifie que le compiler doit chercher des namespaces ou types names en haut du systeme.

Il est aussi possible de créer des alias sur des DLL. Quand il est nécessaire d'avoir 2 versions différentes d'une DLL (à éviter aussi)

1. Solution Explorer > Project > References Elements > Assembly à donner alias
2. Clique droit > Proprietés
3. Changez le champ Aliases de Global à autre chose.

Pour utiliser cet alias, il faut le préciser en haut du fichier (avant les directives et les namespaces)
```
extern alias MyAlias;
```

Suite à cela, on peut acceder aux éléments comme Cela
```
MyAlias::NameSpace.class
```

## Checked & Unchecked Context

```
int x = int.MaxValue;
x++;
Console.WriteLine(x);
```

Par défaut, cela est supposé créer une erreur overflow. La plupart des scénarios ne créeront pas d'overflow et vont simplement transformer la variable dans un type de data plus grand (long au lieu de int par exemple). Dans certain cas, ils vont juste être wrap around (donc passer de max au min), ce qui peut poser de gros problemes dans certain scas.

Cela se produit car C# execute son code dans un contexte unchecked. Cela signifie que le runtime ne se soucie pas des overflow, il ne les vérifie pas. Il permet aux bits d'être reinterpretés et de trunc la valeur.

Il est possible de forcer un contexte check avec le block checked
```
int x = int.MaxValue
checked {
  x++;
}
Console.WriteLine(x);
```

Cela va générer une exception d'overflow, mais il est aussi possible de faire l'inverse avec le block unchecked. Ce block existe car même si c'est le mode par défaut, il est possible de parametrer tout une application en checked ou unchecked dans les parametres du compiler avec la commande /checked- ou /checked+ ou alors

1. Clique droit sur un project
2. Properties
3. Build tab
4. advanced button
5. Check for arithmetic overflow/underflow

## Volatile fields

Il faut déjà décrire 2 concepts de programmation qui sont :
- Program order of instruction
- out of order execution

Par defaut, on assume que le programme va executer le programe ligne par ligne. Le CPU optimise les instructions pour pouvoir remplir son pipeline en permanance et peut donc les re-arranger ou les executer en paralleles. Le faut de re-arranger les instructions s'appelles le "out of order execution", c'est la façon dont le CPU execute le code plus rapidement.

Le CPU sait gérer pour qu'il n'y ait aucun probleme et que la logique du programe soit respecté. Un des problèmes qui peut survenir avec ce comportement est que le CPU assume qu'il n'y a qu'un seul thread. Lorsque plusieurs threads sont utilsiés, il peut avoir des problemes d'executions.

```
//Thread 1
value = 42;
complete = true;
//thread 2
while(!complete)
  Console.WriteLine(value);
```
Dans ce contexte,  on peut avoir une différente valeur que 42 affiché car, 42 n'a pas encore été assignéé. L'idée est le resultat d'une memory operation (Read ou Write) visible aux autres threads, on parle d'opération visible. Dans notre contexte, cela signifie que le complete = true peut être visible avant le value = 42.

### Memory Barriers
Une des solutions est la memory barrier. C'est une instruction qui indique que les taches en cours reads/writes doivent être compléter avant de passer cette barriere.

1. Acquire semantics - si une opération acquieres de la sméantique, elle sera visible avant la derniere la prochaine instruction
2. Release semantics - si une opération release de la semantics, l'instruction précedente sera visible avant

En C#, on peut marquer des champs avec le mot clé volatile. Lire un champ volatile, un volatile read signifie que le champ a acquis de la semantics. Cela signifie qu'il sera effectué avant n'importe quelle de ces references

Lorsqu'on écrit un champ "volatile write", cela signifie qu'on "release semantics". Cela veut dire que cela va s'effectuer apres les references à cette mémoire.

dans notre exemple
```
private volatile bool complete; // executer avant la prochaine instructions
value = 42;
complete = true // comme volatile, on s'assure que l'instruction précédente a été executé avant de le rendre visible
