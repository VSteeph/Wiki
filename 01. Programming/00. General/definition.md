> A trier, importer depuis mon wiki slite
# Définition générique

## Operand
l'élément sur lequel on effectue des opérations (exemple 3 +6 = 9, l'operand est 3)

## Stack
Principe de LIFO (Last in First Out). C'est un tas où l'interaction est seulement possible en haut de la pile. C'est une data structure linéaire ou une collection séquentielle. Si le stack est plein et qu'on veut push un élément, il y a un overflow. C'est comme ça que les processeurs fonctionnent, un stack d'instructions. Chaque élément est une frame où toutes les informations nécessaires sont indiquées (variable, instructions,  etc).

Dans une application, le stack est souvent associé à un heap (général plutôt que spécifique à l'application) qui permet de stocker les variables de références (en C# par exemple)

## Processor Register


## Types of computer architecture :
### Accumulator Machines (AC)
C'est considéré comme abandonnée mais a des instructions régulières qui permettent de décodé plus rapidement, en échange la machine a besoin de plus d'instructions.

L'accumulator est un registre qui permet de stocker les résultats et logiques intermédiaires pour éviter d'écrire le résultat de tous les calculs dans la mémoire. cela permet donc d'avoir des variables plus rapide à accéder.

Les nouveaux ordinateurs utilisent des registres qui servent d'accumulators, c'est donc moins d'actualité.


### Stack Machines :
La plupart de ses instructions se basent sur un stack de chiffres (pile comme pour l’exécution du code) au lieu d'avoir les chiffres dans des prrocesor registers. Comme les instructions sont toujours au même endroit (le haut de la pile, première frame), il n'y a pas besoin d'avoir des adresses de mémoire ou des registres de chiffres pour fournir les operands.

Cela donne un ISA (Instruction Set Architecture) appelé zero adress format.

### Loadstore Machines
C'est une architecture d'instructions qui se divisent en 2 catégories : Memory access (charge et stock entre la mémoire et les registres) et les ALU (Arithmeric Logic Unit) qui ont lieu uniquement entre les registres.

### Micro architecture
https://en.wikipedia.org/wiki/Microarchitecture

## Instruction set architecture

## Stack-oriented
https://en.wikipedia.org/wiki/Stack-oriented_programming

# Code

## Interoperabilité
C'est la capacité d'un produit ou un systeme à fonctionner avec d'autres produits ou systeme dans le présent ou dans le future. Cela peut aussi être 2 langages qui interagissent ensemble dans un même systeme.

## PDB File
Un fichier PDB contient des informations pour le debugger. Cela signifie Program Data Base. C'est un repository persistant qui garde les informations nécessaires pour que le programme fonctionne en debug mode comme les breakpoint

## CRUD
Create Delete Update Delete fonctionnality
