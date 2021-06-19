# Les basiques d'un ordinateur
> Source : https://www.youtube.com/playlist?list=PLH2l6uzC4UEW0s7-KewFLBC1D0l6XRfye

## Random Lexique
1 bits = 0 ou 1
1 byte = 8 bits
hexadecimal = binary sur une base 15 (1 à F)
Binary, les 0 à gauche valent 0

## Basique
Le binaire qui veut dire 2 états, soit 0 ou 1, qui correspond au flow d'electricité (le courant passe ou pas). Cela peut aussi être "On" state quand le courant circule (Vrai) et "Off" State quand le courant ne passe plus (false).

Les transistors permettent de faire un peu plus que 2 états, il y avait certains ordinateurs qui était en ternary (3 states) ou Quinary (5 states). Le probleme est que plus il y a d'état, plus c'est dur de les garder séparé, ce qui est prône à l'erreur et à plusieurs millions d'opérations à la seconde, c'est préférable de limiter les erreurs.

De plus, une branche de math existe déjà basé sur le concept de True/False, c'est l'algebre booleene.

## Algebre Booelene en electronique
Il y a plusieurs opérations possibles :
- AND (L'un et l'autre)
- OR (L'un ou l'autre)
- Not (Inverse la valeur booleene, il prend qu'unn seul bool)

C'est un comportement facile à reproduire avec des transistors.

### And Gate
Cela se crée avec 2 transistors collés à l'autre pour avoir 2 inputs et 1 output.
![AndGate](img/AndGate.png)

### OR Gate
Cela nécessite un peu plus de cable que la AND Gate, car il faut mettre les transistors à l'opposé pour que le courant puisse passer d'un coté ou de l'autre. L'arc signifie que les cables se chevauchent mais ne sont pas connectés

![OrGate](img/OrGate.png)

### Not Gate
C'est un peu plus compliqué, mais il n'y a besoin que d'un transistor. Il faut déplacer l'output avant le transistor, de cette façon :

![NotGate](img/NotGate.png)

Si l'input est On, le courant passe le transistor et part dans la terre, donc l'output ne recupere pas le courant. A l'inverse, si l'input est off, le courant ne peut pas aller en terre et donc passe par l'output.

### XOR
Enfin, la derniere opération qui n'a pas été mentionné, c'est le XOR car c'est une combinaison de 3 autres.

![XorGate](img/XorGate.png)

## Traduire True/False en valeur (Nombres & lettres)
Cela fonctionne comme pour les nombres et les chiffres. C'est à dire qu'on a des chiffres de 0 à 9 et on ajoute plus de chiffre pour constituer des nombres. C'est juste en base deux au lieu d'être en base 10.

Ce qui donne au lieu d'avoir :
| 1000 | 100 | 10 | 1 |
|------|-----|----|---|

On obtient :
| 8 | 4 | 2 | 1 |
|---|---|---|---|

Cela veut dire que si on a 1011, on a 1(8), 0(4), 1(2) et 1(1), cela nous donne 11. Les additions marchent de la même façon avec les retenu
 10110111 (183)
+00010011 (19)
 11001010 (202)

 Chacun de ces 0/1 sont des bits. C'est à dire que la somme au dessus est en 8-bits soit 256 valeurs de 0 à 255. 8-bits cela s'appelle un byte, donc 1kb = 1000 kilobytes (soit 8000bits).

 Les ordinateurs doivennt aussi représenter des nombres à décimal (float). Pour cela, ils ont le standard IEEE 754. En gros, cela utilise un systeme scientifique avec un significant qui possède les chiffres (décimales et entier) avec un exposant qui permet de placer la virgule.

 Cela permet d'avoir ce genre de variable pour un float en 32-bits :
 ![float](img/float.png)

 Pour les lettres, on utilise le même systeme où elles sont numérotées et on utilise 5bits pour avoir l'ensemble des possibilités. Actuellement, on utilise le format ASCII qui utilise un 7-bits code pour avoir des symboles, ponctuation et majuscules/minuscules, avec même des LineBreak pour pouvoir passer a la ligne.

 En tant que standard, c'est devenu un moyen universel d'échanger des données, cela s'appelle de l'interoperability (interop en code). ASCII est passé à 8bits pour permettre d'inclure des caracteres nationaux comme les accents en français ou les elements cyrillic en russe. Cela avait certaines limitations notamment quand on passait d'un pays à un autre.

 Pour cela, les pays ont crée des encodages multi-bytes qui était incompatible les unsn avec les autres. C'est pour cela que l'Unicode est né. Crée en 1992, UniCode utilise 16-bits pour véhiculer plus d'un millions de code pour chaque character de tous les pays, des symboles mathematiques et même de la place pour des emoji.

 De la même manière que les lettres, les formats comme MP3s, ou GIF utilisent des chiffres binaires pour encoder des sons, des couleurs de pixels de photo.

 Tout a le même format, une longue sequence de bits qui sont traités de façon différentes.

# Le fonctionnement d'un ordinateur

Les ordinateurs actuels peuvent être en 32bits ou 64bits. Cela signifie qu'ils opérent par chunk de 32 ou 64bits. 32bits correspond à un peu moins de 4.3 milliards de possibilités. Le premier bit est souvent utilisé pour le signe (négatif ou positif), cela veut dire qu'on a plus ou moins une gamme de + ou - 2 milliards.

Cela peut paraître beaucoup mais les chiffres dans notre société prennent une démesure (7 milliards d'habitants par exemple). C'est pour cela qu'on passe à 64bits qui peuvent aller jusqu'à 9.2 quintillon.

La nécessite venait surtout du fait qu'un ordinateur moderne a des trillions de bytes et qu'il fallait pouvoir stocker les adresses pour les identifier.

## CPU

### Organisation d'un CPU

Un processeur a plusieurs registres pour stocker des variables temporaires (A,B,C,D), de la mémoire et une table d'instruction comme LOADA, LoadB, StoraeB, Add.

Le 4 premiers bits sont le type d'opération et les 4 autres sont pour l'emplacement de la donnée, ce qui nous donne une instruction de 8bits.
Il faut savoir à quel instructions le CPU est donc il faut aussi ajouter un instruction Adress Register pour avoir l'adresse de l'instruction actuelle (et on peut incrémenter à partir de la) et un registre pour savoir quelle instruction est entrain d'être executé L'instruction Register

 ![CPUSetUp](img/CPUSetUp.png)

 Organisation lors de l'execution d'une instruction. Le CPU recupere l'instruction à l'adresse de l'instruction Adress Register. L'instruction est 0010 1100 (je la sépare pour avoir les 4bits séparés), c'est celle à l'emplacement 0 de la RAM car on commence le programme.

 ![CPUInstrucSchema](img/CPUInstrucSchema.png)

 Dans cet exemple, l'instruction est de lire la mémoire à l'emplacement des 4 derniers bits (1100 ou 14) et de le load dans le registre A (instruction 0010). Une fois que c'est bon, on incremente l'adresse register par 1 et on recommence le cycle Fetch-Decode-Execute (détaillé ci-dessous)

 A noter que certaines instructions, comme ADD ont une organisation différente car elles ajoutent 2 registres entre eux, et avec 4 registres, on a besoin que de 2 bits pour symboliser l'information, les 2 premiers bits sont pour le premier registre et les 2 suivants pour le second registre (ex : 0100 correspond au registre B et A).

 A ce moment la, les 2 valeurs sont recuperés et envoyer à l'ALU avec l'operation Code (dans ce cas la, l'addition) qui s'occupe de faire le calcul et renvoie l'output au Control Unit.
 A ce moment la, le Control Unit stock le résultat dans un registre temporaire, desactive l'ALU et peut enfin stocker le résultat dans le registre voulu (2nd, dans ce cas la, registre A)).

 Evidememnt, il est possible d'enregistrer une variable à une adresse spécifique de la RAM, cela fonctionne de la même manière que pour un registre. Le CPU active le write enable pour la RAM au lieu du registre.

 Le passage d'une instruction à une autre est fait avec une horloge (métronome) qui va s'occuper de la fréquence. Il faut qu'elle respecte le temps de l'electricité pour que l'instructions est le temps de finir (c'est la fréquence des CPU, Clock Speed). c'est mesuré en Hertz. Un hertz = 1 cycle par secondes.

  ![FirstCPUarchi](img/FirstCPUarchi.png)
  C'est le premier CPU intel 4004. Il avait une clock speed de 740khz, soit 740 000 instructions à la secondes.  1mhz (mega heart) correspond à 1 millions de cycles à a secondes et 1ghz correspond à 1 milliards de cycle à la seconde.

  Il est possible d'overclock (pousser un peu le CPU) ou même d'underclock pour économiser de l'electricité. Le fait de manipuler la fréquence basé sur l'a demande s'appelle la Dynamic Frequency Scaling.

### Comment le CPU execute un programe (Fetch-Decode-Execute Cycle)
En partant d'une ligne :
INC A (assembly) signifie incrémenter le registre A (c'est à dire ajouter 1 à A, peu importe ce qui est dedans). Cela prend la forme de :
00111100 en machine code (binaire).
Le binaire est souvent traduit en hexadecimal pour que ça soit plus simple à retenir, cela correspond donc à 3C

INC A = 00111100 = 3C

L'hexadecimal va de 0 à 15 (1-9 + A-F), ce qui signifie qu'il peut représenter une plage de 4bits (3 = 0011 & C = 1100), donc 3C = 1 byte

Voici, un schéma simplifié du systeme d'un microprocesseur :
![CPU-Schema](img/schema-cpu.png)

Le code sera placé dans la premiere ligne (à droite) AE00, cette adresse sera mis dans le PC (Program Counter), en partant du principe que le registre A contient 00 (H signifie qu'on est en hexadecimal), on obtient ce statut ;

![CPU-step1](img/CPU-step1.png)

Le binary patern dans le Program Counter (AE00) est transferé dans le MAR (Memory Adress Register), ce qui fait que le PC (Program Counter) augemnte de 1, on passe donc à l'instrction AE01.

Le contenu du MAR (Memory Adress Register) est tranferé dans l'adress bus, et le CU (Control Unit) envoie 2 low pulses dans les 2 control lines (CS line & Read/Write line => R/W Line).

Un low pulse dans la CS Line est responsable d'activer la puce, et celui dans la R/W Line assure que la location selectionnée est lue.

![CPU-step2](img/CPU-step2.png)

Le "3C" parlt donc dans le BR (Buffer Register) via le Data Bus et une copie est envoyé dans le IR (Instruction Register).

A ce moment la, on est à la fin du "fetch" dans le fetch-decode execute cycle.

![CPU-step3](img/CPU-step3.png)

On commence donc le décodage de l'instruction. Le decoder détermine donc ce que 3C signifie et envoie l'information au CU (Control Unit). La valeur du registre A est envoyé dans l'ALU (Arithmetic and Logic Unit) et demande à l'ALU d'y ajouter 1

![CPU-step4](img/CPU-step4.png)

La nouvelle valeur est envoyé dans le registre A via l'internal Data Bus, ce qui conclut l'execute dans le fetch-decode-execute cycle.

L'ensemble de ce systeme est geré par le CU (Control Unit) qui s'occupe d'organiser tous les éléments d'un CPU.


### Advanced CPU
A l'heure actuelle, les ALU sont beaucoup plus sophistiqués et beaucoup plus complexe. Ils peuvent faire des multiplications, et des divisions ce qui les rend plus gros aussi. C'est un échange pour gagner de la vitesse. C'est pour cela que les PC ont maintenant des circuits dédiés aux opérations graphiques, décodé des vidéo et encrypter des fichiers.

Cela permet d'économiser beaucoup d'opérations au CPU avec les instructions standards grâce à des circuits spécialisés. Pour garder la compatibilité, les instructions ont été ajoutées et ajoutées mais jamais enlever.

Augmenter la clock speed et toutes les instructions a mené à un autre probleme : Entrer et sortir les données du CPU suffisament vite, ce qui est la RAM qui est un module de mémoire en dehors du CPU. Les 2 sont connectés par un set de cable de données (BUS). Ces BUS sont petits et l'electricité va très vite mais quand il y a 1 milliards d'opérations à la seconde, le moindre délai est un problème. Sans compter le fait que la RAM doit trouver l'adresse, recupérer la donnée et se configurer pour l'output. Un LOAD from Ram prend pluiseurs, voir dizaines de clock speed. Le processeur est iddle à ce moment la.

Pour régler ce problème, le CPU a une petite RAM appelé le cache (en général, kb ou mb au lieu de gb, donc beaucoup plus petit). Cela accelere le processus car la RAM utilise l'entierté du BUS et envoie un ensemble de donnée plutôt qu'une seul valeur, cela ne prend que peu de temps en plus par rapport à une seule valeur. Cet ensemble est mis en cache et est executé par le processeur en attendant que la nouvel ensemble de donnée arrive.

Le cache est situé sur le processur, donc cela permet de limiter le trajet au minimum et donc match la fréquence du CPU. Si le CPU demande une valeur et qu'il a dans le cache, ça s'appelle un cache Hit et si elle n'est pas dans le cache, c'est un cache miss.

Le cache peut aussi être utilisé pour stocker des valeurs temporaires quand elles sont utilisées longtemps ou lors de long calcul. Les données qui sont modifiées dans le cache sont flagged comme "Dirty Bit" et lorsque le processeur demande d'autres données, les valeurs sont renvoyés à la RAM pour ré-écrire les données et resynchorniser l'ensemble.

Pour optimiser encore plus le CPU, le Fetch-Decode-Cycle est enchainé, car chaque cycle utilise des parties différentes du CPU. Quand une instruction est executé, une nouvelle est entrain d'être décodé, donc le CPU execute 3 instructions à la fois. Ils peuvent gérer les data dependencies et ralentissent certaines instructions pour pouvoir manipuler la nouvelle donnée et pas l'ancienne. Par exemple, instruction 1 recupere une donnée 2, instruction 2 l'incremente et instruction 3 la store. Si on ne ralentit pas l'instruction 3, il va mettre en mémoire la valeur de la donnée avant que l'instruction 2 soit executé (donc la mauvaise valeur) et va stocker l'ancienne valeur.

Les CPU modernes peuvent ré-organiser les instructions dynamiquement avec les dependences pour éviter les ralentissement et garder le pipine actif (out of order execution).

Cela pose aussi un probleme pour tous les instructions à base de condition comme les Jump car le CPU doit executer cette instruction pour savoir s'il doit jump ou non. Les CPU modernes estiment qu'elle est l'outcome la plus probable et commence à mettre en pipelines les instructions : Speculative execution. Si le CPU a raison, il n'y a aucun délai. Si le CPU a tort, il vide le pipeline (pipeline flush) et recommence. A l'heure actuelle, les CPU ont plus de 90% de précision pour les guess.

L'optimisation de CPU se fait aussi en multipliant les parts du CPU. Par exemple, un CPU qui a plusieurs ALU peut faire plusieurs instructions d'ALU en même temps au lieu d'une seule, cela permet de tirer le plus de chaque cycle.

Enfin, il y a les cores de CPU qui permet de procéder encore plus d'instructions et grâce au cache qui est commun, cela permet de faire d'aller beaucoup plus vite dans les instructions d'une seule tache.

## Comment un ordinateur Calcule? (ALU)

### Arithmetic Unit
Un ordinateur calcule grâce à l'ALU (Arithmetic and Logic Unit), c'est le cerveau mathématique de l'ordinateur. Elle a 2 units : celle arithmetic et celle logic.

L'arithmetic permet de faire des additions, soustractions, incrementer, decrementer. Pour simplifier le système, on utilise de l'abstraction et créer les composants basés sur de la logique (AND, OR, NOT, XOR). (XOR est un OU exclusif, c'est à dire l'un ou l'autre)

Voici les 4 d'opérations possibles :

![operations](img/operations.png)
Dans le cas, du 1+1, c'est égal à 0 et le 1 est avancé sur la colonne suivannte. Ces opérations collent parfaitement avec  un tableau de logic, en partant du principe que 0 = false et 1 = true

![logic](img/logic.png)

Le circuit ci-dessus est appelé un Half Adder. Il permet d'avoir 2 output : Sum et Carry basé si A & B sont vrai. Si les 2 sont vrai, la somme est fausse avec le XOR mais le carry est vrai avec le AND

Cela nous donne cette encapsulation :

![halfadder](img/halfadder.png)

Le probleme c'est que cette logique ne marche qu'avec 2 bits, en prenant en compte le carry, il faut pouvoir prendre en compte 3 bits : A, B, C

Ce qui amene à la Full Adder table :

![fullAdderTable](img/fullAdderTable.png)

et la logique du fulladder, qui est 2 half adder : une avec les 2 valeurs initiales A & B et une avec le carry qui permet de déterminer la sum final et le carry final

![fullAdder](img/fullAdder.png)

Si on veut augmenter le nombre de bit supportés, il suffit juste d'aggrandir la séquence où la premiere opération ne nécessite que d'un half adder car il n'y a pas encore de carry, puis elle est suivi de full adder.

![RippleAdder](img/RippleAdder.png)

Le problème du full adder est qu'il peut finir avec un carry s'il dépasse 8bits, ce qui provoque un overflow. C'est pour cela que les éléments de 8 bits ne peuvent pas dépasser 255.

Pour éviter l'overflow, on peut aggrandir le cycle avec plus de full adder pour arriver à 16/32/64 bits mais cela prend plus de gate et cela prend plus de temps pour le carry d'être passé de cycle en cycle.

C'est pour cela que les LUA actuels utilisent un "Carry-look-ahead adder", c'est plus rapide et a la même fonctionnalité. Ce qui donne ces fonctionnalités :

![fonctionnalité](img/fonctionnalité.png)

Il n'y a pas de multiplication, ni de division. Aucun circuit n'est prévu pour ces opérations, l'opération fait plusieurs fois le même circuit (addition) pour faire une multiplication.

Maintenant, les téléphones portables/ordinateurs portables ont des circuits dédiés pour les multiplications. Cela nécessite plus de logic gates, c'est donc reservés aux machines puissantes et pas les éléments simples comme des micro-ondes ou des thermometres.

### Logic Unit

Elle permet de faire plusieurs tests et utilisent le même type de circuit que l'arithmetic unit. Par exemple, pour tester si un chiffre est inférieur à 0 ou si le chiffre est égal à 0. Pour tester, si un chiffre est égal à 0, on a ce type de circuit :

![zero](img/zero.png)

et un Not est utilisé entre le dernier OR et l'output avant d'inverser l'output pour savoir si le chiffre est bien égal à 0 (car 0 = false)

### ALU schema

Premier ALu par Intel :
![firstALU](img/firstALU.png)

Les Alu suivent un schéma "V", voici un schéma pour un ALU à 8 bits :

![ALUschema](img/ALUschema.png)

Il y a donc 3 entrées : Input A, Input B qui vont être manipulés, l'opération code qui va être comment les variables vont être manipulés (00111100 ou 3C pour INC A dans l'exemple du fonctionnement du CPU)  et 2 sorties : le résultat qui est celui de l'opération et les flags qui ajoutent des informations sur l'output

## Register & RAM
Random Access Memory (RAM) stock les éléments tant qu'il y a du courant contrairement à la mémoire persistante. (A creuser sur le côté volatile, non volatile qui permet de stocker la mémoire)

### RAM
Les circuits vont naturellement dans un sens mais il est aussi possible de le faire aller dans les 2 sens

![CircuitLoop](img/CircuitLoop.png)

Le probleme c'est qu'on peut pas le reset (avec OR ou AND) puisque même en changeant A, on ne peut plus revenir à la situation initiale

Pour cela, il faut les combiner dans un circuit appelé : And-or Latch

![LatchCircuit](img/LatchCircuit.png)

Ou activer Reset (Reset = 1) repasse le circuit à 0, tandis que set (Set = 1) passe le circuit à 1. Si les 2 sont à 0, c'est la derniere valeur qui prime

Cela permet donc de stocker 1 bit, d'ou le nom car le circuit s'accroche à une valeur.

Le circuit a été simplifié (pour l'utilisation) en permettant à avoir un seul point d'entrée que l'on peut set à 1 ou à 0. Pour cela, on a ajouté des gates.

Il a aussi été securisé avec un Write Enable pour permettre de lock la mémoire lorsqu'on l'a lit (Read) et la débloquer quand on l'écrit (Write). C'est à dire si le Write Enable est à 0, l'output est à 0 car c'est verouillé. C'est uniquement quand on passe le Write Enable a 1 que l'on peut output 1. Si on repasse le Write Enable à 0, la data restera à 1 et sera verouillé.

Ce qui donne le gated-latch.

![gated-latch](img/gated-latch.png)

Un groupe de latch s'appelle un register. Il contient un seul chiffre, et le nombre de bits du register qui est sa longueur (width)


Ce qui nous donne un 8-bit register :

![register](img/register.png)

Il y a Write Enable pour l'ensemble du Register et une entrée/sortie pour chaque latch du register. Le problème de cette organisation est qu'elle scale tres mal sur la taille (même s'il n'y a qu'un seul Write Enable pour le register)

C'est pour cela que l'on utilise maintenant des matrix (16x16 matrix => 256bits). On utilise le principe des coordonées avec un And avec un cable par colonne et par ligne

![Latch-Matrix](img/Latch-Matrix.png)

On voit que seulement une cell va être activé par la colonne et la ligne qui s'active, toutes les autres sont desactivées. Cela permet d'avoir Write-Enable et Data-In/out commun à toutes les cellules car un seul latch sera activés
![Latch-cell](img/Latch-cell.png)

Cela signifie que pour avoir 256bits de mémoire, on a besoin de 35 cables - 1 data wire, 1 write enable wire, 1 read enable wire et 16 pour les colonnnnes et 16 pour les lignes au lieu des 500+ de l'autre situation.

Comme il y a 16 rows/colonnes, on store l'adresse dans un chiffre à 4 bits. Ce chiffre est envoyé à un component le MultiPlexer

![multiplexer](img/multiplexer.png)

Il permet d'activer une ligne spécifique, on en prend un pour les colonnes et un pour les lignes. C'est à dire que pour faire marcher un registre de 256 bits, on a besoin de :
- 8 bit pour l'adresse des Latch
- Data (1bit)
- Write Enable (1 bit)
- Read Enable (1 bit)

Le probleme est que 256 bits est tres léger, donc il faut scale enccore plus (en les mettant en ligne comme pour le premier register). On les met 8 par 8 pour pouvoir stocker des données de 8 bits (au lieu de 1). On a besoin des Write Enable, Read Enable et de leur adresse pour chacun à nouveau.

On utilise la même adresse pour registre (organisation, simplicité)

![RAM](img/RAM.png)

Ce qui nous donne, non pas une série de circuits, mais une banque de mémoire uniformisé de 256 adresses ou l'on peut lireou écrite une valeur de 8 bits.

![simplified-Ram](img/simplified-Ram.png)

Le nom de RAM vient du fait qu'on peut acceder à n'importe quelle adresse, à n'importe quel moment dans un ordre aléatoire (d'ou Random-Acces Memory)

Plus d'informations dans la partie hardware pour l'illustration sur une vrai RAM


### SRAM (Static random-Access Memory)
Ce type de mémoire utilise des latch aussi


## Programmes

### Execution

Un programme a plusieurs instructions (opcode):
- Load A / Load B (Load une valeur de ram dans A ou B)
- Store A (Store value in A dans un registre)
- Add / sub (2 registres et store dans le second registre)
- Jump (saute à la prochaine instructions)
- Neg Jump (saute à la prochaine instruction si le result de l'ALu trigger le Negative flag)
- Halt dit au programme de s'arrêter

Si le programme reçoit en instructions un code qui ne correspond à aucune des instructions qu'il connait il crash, c'est pour cela qu'il est important de mettre un halt au programme et cela permet aussi des séparer les instructions, de la mémoire.

Les ordinateurs modernes ont plus d'instructions comme Jump if equal/ jump if greater. 4bits d'opération permettent d'avoir uniquement 16 opérations, c'est pour ça que les CPU modernes ont des approches différentes.

Ils utilisent déjà plus de bits (32/64) donc une plus grande instruction length. En plus, ils utilisent des instructions à taille variables. Par exemple, si les opcodes sont de 8bits, quand le CPU voit une instruction qui n'a pas besoin de valeur supplémentaire comme Halt, il l'execute automatiquement. A l'inverse, s'il voit une instruction qui a besoin de plus de donnée, il va aller chercher la suite des informations (qui sont sauvergardés directement apres l'instruction dans la mémoire), c'est l'immediate value. Cela permet d'avoir des instructions de bits variables.

Le premier processeur (INTEL 4004) avait 46 opérations, ceux actuels ont des milliers d'opérations possibles

### Charger un programme

Avant, pour charger un programme, il fallait agencer les cables dans le plugboard pour faire l'execution, un programme par set up. En 1920, on a permis de swap  ces plugboards pour pouvoir run plusieurs programmes dans une machines. Réaliser ces plugboards mettait beaucoup de temps à concevoir et beaucoup de temps à créer, un nouveau modele a été crée plus flexible, plus rapide : Memory Electronic.

Les programmes ont été entré dans des mémoires et chaque mémoire avait un programme et potentiellement toutes les donnnées nécessaires. Uniformiser les données du programmes dans une simple memoire partagé s'appelle la Neumann architecture.
La mémoire était interchangeable et le programme s'executait comme l'intel 4004 (avec la RAM qui était une mémoire avec un programme dedans).
L'architecture Neumann est à la base des ordinateurs modernes (toujours actuel).

Pour écrire les données dans la mémoire, les ordinateurs avaient un reader de punch cards (8 bits), chaque ligne était une instruction qui se chargeait dans la mémoire. Le reader de punchcard pouvait aussi lire plusieurs punchards et les stocker dans la mémoire une par une en un seul block.

Un ensemble de Punch-card créait un programme. Le plus gros programme avait 62 500 punch cards, ce qui corresponnd à 5 mega bytes de donnée. Un ordinateur avait aussi un punching card pour pouvoir output les données dans un format de punch cards, ce qui permet d'analyser les données ou de s'en servir pour un autre programme.

Enfin l'autre façon de programmer et contrôler un ordinateur est le "panel programming" qui au lieu d'avoir un mur de cable à brancher ou à débrancher pour activer des fonctions, cela pouvait aussi être fait avec des boutons et des lumieres pour symboliser ce qui était allumé.

![loadProgram](img/loadProgram.png)

Il était donc possible d'entrer un programe juste avec les interupteurs/boutons (comme une punchcard). Ils étaient surtout utiliss en loisir car les périphériques punch card readers étaient cher

Le premier ordinateur personnel avait 2 modes : entrée de programme et execution. Il fallait entrer les instructions avec les interrupteurs par instructions et une fois qu'on avait fini, on activait le bouton "Switch Back" pour revenir à l'instructions 0 et tout s'executait, et lse lumieres s'écrivait

![HobbyComputer](img/HobbyComputer.png)

C'était très dur d'entrée car il fallait connaître les OpCodes et les registers wits

### Software

Façon de programmer plus simple (softer) que le hardware et les boutons qui étaient plus durs. L'idée est de créer en pseudo-code la logique, puis traduire la logique en instructions binaires à la main. Le programme pouvait être envoyer à l'ordinateur à ce moment la.

L'idée était donc de transformer le binaire en instruction comme LOAD_A value pour load une value dans le registre A. Pour cela, les programmers ont crée des helpers programs qui était reutilisables en binaire. Ces programmes lisaient les instructions et les assembler en instructions binaires, d'ou le nom : assembleur (assembler).

Les premiers QOL sont apparus avec les meta data de loop pour préciser à quel endroit devait revenir un JUMP plutôt que de donner l'adresse de l'instructions exacts. C'est juste une couche de vernis. En gros, une terme est associé à un code.

Les langages plus haut niveau peuvent nécessiter plusieurs instructions. C'est pour cela que les compilers ont été crée. Cela a permis de supprimer la gestion des registres, des adresses.

De cette façon, on a diminué le temps de programmation en contrepartie de légerement augmenter le temps de computing. C'est le début de l'uniformisation des ordinateurs avec chaque ordinateur possédant son propre compiler mais tous peuvent run du COBOL.
