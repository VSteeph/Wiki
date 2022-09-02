# Pro C# 8 with .NET Core 3

## Chapter 1 : .NET Core introcution

 C# 8 est principalement pour .NET Core car il y a plein de fonctionnalité qui sont incompatibles avec .NET Framework et c'est la raison pour laquelle, il y a peu de chance que .NET Framework support le C# 8

 > Certaines features peuvent être utilisées en passant par des packages Nuget

### Avantages de .NET Core
- Interoperabilité avec un code xistant
- Support pour de nombreux langages
- Un common Runtime Engine partagé par tous les langages .NET CORE
- Langage Integration (inheritance, exception, debugging)
- Une base class Library vaste
- Un deployement simplifié (plusieurs versions de .NET Core possibles sur un ordi)
- Un support en command Line (CLI Command Line Interface)

### Support LifeCycle
Le cycle de développement de .NET Core est tres rapide, il y a donc un systeme de LTS (3 ans de support apres leur release ou 1 an apres une autre version LTS).

La version 3.1 est la LTS à ce jour.

### Building Block

Les 4 points clés de .NET Core :
- Core Runtime (CoreCLR & CoreFX)
- CTS (Common Type System)
- CLS (Common langage SPecification)

Le runtime est composé de :
- .NET Core COmmon Language Runtime (or CoreCLR)
- .NET Core Librairies or CoreFX

Le CoreCLR est un ensemble d'implementations liés à une plateforme spécifiquement (Windows, IOS, Linux) et une architecture (x86, x64, ARM).

Seulement les types qui sont liés aux déployement sur la cible sont inclus dans le CoreCLR mais ils sont considerés comme privé, tandis que le CoreFX est principalement platforme agnostic et inclue tous les types basiques pour .NET Core. C'est lui qui a les implémentations publics.

Le CTS décrit tous les types de donnnées et les programming constructs supportés par le runtime et spécifie comment ces entités interagissent entre elles.

Le CLS permet de s'assurer que les types sont supportés par l'ensemble des programming langage de .NET Core.


### .NET Standard

Le nombre de librairies (base Class librairies) dans le .NET Framwork est bien plus important que celui de .NET Core.

https://docs.microsoft.com/en-us/dotnet/standard/net-standard (compatbilité entre .NET & .NET Core)

### .NET Assemblies
L'ensemble binaire qui contient le "managed code" est appelé une assembly contrairement au code qui peut aps être host directement sur le .NET Core runtime "unmanaged code". il est important de noter que le "unmanaged code" lock le programe sur une cible de déployement spécifique.

Les binaries de .NET Core sont ausi des *.dll (comme ceux unmanaged de windows) mais il n'y a aucune similarité entre les 2. Les .NET Core binaries n'ont pas d'instructions spécifique aux plateformes, ils ont un IL (Intermediate Language) platforme agnostic.

Une assemblie .NET Framework peut être : *.dll ou *.exe, ce qui n'est pas le cas de .NET Core (toujours *.dll). L'exe est juste un raccourci pour executer l'assembly (commande : dotnet <assemblyName>.dll)

En .NET Core, l'assembly a aussi du code CIL et des metadata pour décrire en détails les caracteristiques de tous les types.

Les metadata permettent enormement de choses comme les docs (docfx), intelisense, debugging tools, etc.

Enfin, il y a aussi les metadata des assemblies (appellé manifest). Cela permet de connaître les dependecies, la version de l'assembly, copyright, ...

Toutes les metadata sont generés par le compiler

### Precompiling CIL to platform specifiques instructions

Il existe un pre-JIT pour le .NET Framework appelé ngen.exe. L'équivalent en .NET Core est crossgen.exe. Cette capacité de produire du code "Prêt à être executer" est integré au framework.

### CTS (Common Type System)

Cela décrit comment les types sont définis. Il y a 5 types majeurs.

#### CTS Class Types
La base de l'OOP, une cclasse peut être composé d'un nombre indeterminé de membres (constructs, properties, methods, events) et de Data Points (champs). Les classe sont déclarés avec le keyword "class"

Une classe a plusieurs caracteristiques :
- Sealed
- Interface implementé
- Abstract ou concrete
- visibilité

#### CTS interface Type
Un interface...

#### CTS Structure Types
Cela peut être vu comme une classe légère de type valeur. Cela peut être utile pour tout ce qui est donnée géometrique, math comme des vecteurs (car valeur).

#### CTS Enumeration Types
Cela permettre de group un nom et un valeur. Par défaut, chaque item correspond à 32bits. C'est possible de le modifier pour les appareil à faible mémoire comme les mobiles.

#### CTS delegate Types
Equivalent d'un type-safe function pointer. La différence est qu'en C#, cela provient d'une classe plutôt que l'adrese mémoire brute.
Ils ont essentiel à l'architecture d'event de  .NET Core

#### CTS Type members
Echelle plus générique

### CLS
Il y a plusieures implémentations des instructions, ce qui n'est pas important pour le CLR. Les langages ont leur propre spécificité. Le CLS est la pour décrire en détails tous les types, features qui doivent être supportés. Les elements doivent respecté le CLS pour être build en .NET Core sans probleme.

Le compiler peut indiquer la CLS compliance.

### NameSpaces important

- System (math, garbage collection, environment variable, random, etc)
- System.Collections & Collections.Generic (Collection & interface)
- System.Data / Data.Common / System.Data.SqlClient (DataBase)
- System.IO / IO.Compression / IO.Ports (File, compression, data manipulation)
- System.Reflection / Reflection.Emit (reflection & dynamic)
- System.Runtime.INteropServices (interact with unmanaged code)
- System.Drawing / System.Windows.Forms (Desktop App)
- System.Windows / Windows.controls / Windows.Shapes (Root pour WPF)
- System.Windows.FormsSystem.Drawing (root pour WindowsForm)
- System.Linq / Linq.Expression (LINQ API)
- System.AspNetCore (ASP Net.core & ReSTful services)
- System.Threading / Threading.Task (multithread)
- System.Security (permission, crypto)
- System.Xml (xml data)

Les namespaces sont justes une organisations mais la classe Console dans systeme n'existe pas vraiment, il y a juste une classe qui s'appelle Systeme.Console.

.NET Core n'utilise plus le GAC (Global Assembly Cache) pour avoir une installation commune des librairies du framework.

A la place, chaque version de .NET Core a son propre dossier d'installations.

## Chapter 2 : Building C# App

### IDE
- Visual Studio (Community similar à professional, différence dans la licence)
- visual Studio Code qui est plus léger et qui est surtout la pour faire du ASP.NET Core car il ne peut pas build de Windows application (WinForms ou WPF) mais il peut run sur linux et macOS.

# CORE C# programming

## Chapter 3 : Core C# Programming Constructs

# Programming with .NET Core assemblies
