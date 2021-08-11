# Project FileStream

## version control

### Inclus
- .sln
- .csproj
- AssemblyInfo.cs (Properties Folder)
- Code Source


### Non-Inclus (.gitignore)
- .suo
- .csproj.user
- Bin folder
- Obj Folder

## Solution
C'est la racine du projet qui contient les projets (1 dossier par projet), cela peut être composé de plusieurs projets ou un seul. C'est pour cela dans les cas où il y a la solution et un projet du même nom. Il y a un dossier "Nom" qui contient un dossier "Nom".

Il y a le .sln qui est la solution et un .suo.

### .sln
Le .sln contient les informations sur les projets dans la soluton, la configuration des builds et les informations communes à l'ensemble des proejts

### .suo
Solution User Options files. Il y a plein de parametres pour Visual Studio comme les derniers fichiers ouverts (personnels)

## Project Directories
Il contient au minimum :
- .csproj
- .csproj.user
- properties Folder
- bin & obj folder
- Code source

### .csproj
C'est l"équivalent du .sln pour la solution. Il contient tous les fichiers, la config.

### .csproj.user
Il correspond au .suo à l'échelle du projet

### Bin & Obj Folder
Le dossier bin est l'endroit où les versions executables sont stockés. Le dossier Obj correspond à la phase intermediaire, quand il faut préparer des fichiers spécifiques ou incomplet pour préparer la fin de la compilation.

ces fichiers comportent un dossier pour chacune des configurations possibles. Par défaut, il y a le debug et le Release.

## Properties folders
C'est le dossier qui comporte les proprietés et les ressources qui sont ajoutés au projet.

Il contient le AssemblyInfo.cs qui correspond les informations sur le projet et les informations de versioning.
