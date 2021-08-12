> A completer (form slite)

Lorsqu'un projet (.csproj) compile, les fichiers .targets sont ajoutés et permettent de faire le résultat final avec le point d'entrée et le process global du build. Cela permet de customiser la façon de build un projet, de déterminer quels fichiers vont être integrés dans le projet.

Cela permet aussi d'ajouter plusieurs instructions à 3 moments différents :
BeforeBuild
DoBuild
AfterBuild (rarement utilisé)

Pour customiser unBuild, cela passe par 2 types de fichiers.

## Directory.Build.props
Cela permet d'ajouter des fonctionnalités/éléments à tous les projets. Par exemplr pour accèder, permettre que tous les projets utilisent la fonction deterministic de Roslyn donnerait :
```
<Project>
 <PropertyGroup>
   <Deterministic>true</Deterministic>
 </PropertyGroup>
</Project>
```

Cela permet decréer le défaut/un standard. Cela peut être override par d'autres éléments ou certains fichiers au cas par cas.

Ce fichier ne donne pas accès à toutes les proprietés, pour avoir accès à la majorité des proprietés, il est preferable d'utiliser

## Directory.Build.targets
Cela permet d'override tous les settings précedents et de donner un état "final" plutôt qu'un état initial comme le .props.

## Choix
En gros, les .props est importé au début dans l'ordre d'importation tandis que les .targets sont importés à la fin du build order.

SI, les proprietés vont être customisés dans les projets, il faut utiliser les .props files, si les proprietés sont nécessaires et crées des dependances, il faut les mettre dans les .targets.



## Ressources :
https://docs.microsoft.com/en-us/visualstudio/msbuild/customize-your-build?view=vs-2019
