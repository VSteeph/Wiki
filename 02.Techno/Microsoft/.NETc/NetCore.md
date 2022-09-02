# .NET CORE general

## Presentation 3.0
Platform pour créer toutes sortes d'applications :
- desktop (Winforms, WPF, enntity framework 6)
- Webform / CLoud
- Mobile
- Gaming
- IOT
- AI (Library ML.net)

Il est possible de créer des singles .exe

### desktop improvements
Overall :
- Better performancne
- API & Core runtime improvements (30% improvement depuis .NET framework)
- Deployment flexibility (.NET core peut même être integré à l'exe pour faciliter le déployment)

UI Framework
- XAML islands - informs & WPF can host WPF
- Better support for high DPI (4k monitor)

Latest technologie :
- C# 8/0 (Ranges pour envoyer des subset de l'array, Nullable reference types, async streams,...)
- .NET standard 2.1  
- ASP.NET Core
  - gRPC (Better performance based RPC services, standard implmentation donc cross langage)
  - Worker services (starting point pour les long process comme Window Server ou linnux daemon)
  - Web API + identity (security & authentication)
  - Razor Componant
    - Créer des clients UI (remplace Angular, React, Vue) et garder la stabilité de .Net (Web assembly qui permet de convertir .NET en IL native browser)
    - Fonctionne sur tous les browsers
    - Web Assembly permet les native peformances, 0 plugins ou code transpilation


# ASP .NET CORE

## Présentation

Il y a plusieurs modeles d'applications en .NET :
- MVC application (Model View Controller)
- Razor Pages Application

### Evolution de Asp.Net
(1996) Active Server Pages (ASP), cela a permis d'avoir du scripting server side pour des pages dynamiques.

(2002) création des forms avec .NET webforms, mais cela avait le défaut d'avoir beaucoup de données trasnferés entre le server et le site.

(2009) ASP.NET MVC, ils ont essayé de régler la probleme de .Webform, il est opensource, mais il avait ses propres défauts car il était basé sur .Net webforms

(2016) ASP.NET CORE, elle a été crée sur .NET Core, qui est la premiere plateforme de .NET et donc n'est pas lié à windows.

Le développement d'ASP NET CORE a été tres active ASP.NET CORE 2 en 2017 et CORE 3 en 2019 (donc *Visual Studio 2019* mais pas obligé d'avoir SQL-server 2019 même si c'est mieux)

La version 3.0 inclut "meta package" comme une partie de NET core. Entity framework a été enlevé du meta package et a son propre nuget pacckage maintenant.

## Intro

### Création d'un projet
- Type de projet (classic) puis custom
- Stack à choisir (.NET Framework / .NET CORE)
- .NET CORE version
- Template à choisir (Empty, MVC, Razor, Angular, Web App)
- Authentication pour l'appli (Systeme de Login ou autre)
- Docker Support & HTTPS

### Razor Pages
Introduit en 2.0, elles sont devenus la façon par défaut
https://docs.microsoft.com/en-us/aspnet/core/razor-pages/?view=aspnetcore-3.1&tabs=visual-studio

Elles permettent de mieux organiser son code en ayant la logique implenté et le view modele proche.

Elles ont les mêmes fonctions que le MVC (Routing, Models, ActionResult, Tags, Helpers, ...)

Les Razor Pages ont 2 parties :
- Razor PAge (UI/View)
- Page Model (Contains Handlers)

Comme pour le XAML, une page est divisé en C# et en UI (HTML au lieu de XAMl pour les Razor pages), le @model doit avoir la même nomenclature que la classe C#.

### Specific files

#### .Csproj
il a un peu changé avec .NET core. La façon principal d'ajouter d'est références comme pour la librairie standard est le Nugget Package.

Il n'y a plus certains fichiers comme le project json.

#### LaunchSettings.json ou appSettings

Ce sont les informations nécessaires pour Run le projet, il est possible d'avoir plusieurs profils (c'est le cas par défaut).

Le premier profil est IIS Express (localHost) et met l'environnement variables à developpement.

Cela peut aussi être changer dans les proprietés du projet (debug avec le profil, les environment variables, etc)

Tous les profils sont aussi présent dans le Run (Config manager Aka debug, Release, etc).

Les profils peuvent aussi être importés d'Azure (facile à modifier json)

#### Dossier wwwroot

Nouvel element avec .NET CORe, c'est l'emplacement pour tous les fichiers statics (img, css, js, lib). Cela sera le dossier root du site. Il est là pour séparer le code et les fichiers statics.

#### Dossier Pages
Cela permet d'avoir toutes les pages que l'on veut pour le site. Il y a aussi un dossier Shared où les fichiers commencent par un underscore comme _layout.cshtml. Cela signifie que se sont des vues partials. C'est comme des user components, ça veut dire que l'on peut les ré-utiliser plusieurs fois à plusieurs endroits.

##### Shared :
_Layout est le default layout (Master Page en XAML) pour l'application avec un header et un footer. Il est aussi plus customisable avec la possibilité de mettre des profils Include=dev ou Exclude=dev par exemple

_ValidationScriptsPartials qui permet d'include les scripts de validations quand on veut intégrer le JS sur certaines pages.

##### Reste
_ViewImports qui permet de définir les tags helpers (custom ou non) à un niveau global  
```
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
```

_ViewStart.cshtml permet de de définir la MasterPage de l'application.

Enfin, on a l'index, Error & Privacy pages (.cshtml). Cela permet de donner le HTML/CSS de la page, elles integrent (en expandant) la page index.cshtml.cs (lec ode) qui sont reliés par le model Name.

### Routing In Razor
Comment match les URLs avec les ressources du serveur pour process les requêtes. La solution la plus directe est de map les URLs avec l'emplacement des fichiers (emplacement physiques sur le disque) (solution choisie par .NET core)

Il y a néanmoins plusieurs regles pour ça :
- Routing se fait par rapport à l'adresse physiqeu du fichiers
- Razor Pages a besoin d'un root folder (Cela peut être configurer si besoin dans la startup class). Par défaut, le root folder est Pages.
- L'URL ne doit pas inclure l'extension du fichier (index.cshtml => index)
- Index.cshtml est le document par defaut, c'est à dire que s'il manque un fichier, cela rediriger vers le index.cshtml du dossier

![indexRedirect](IndexRedirect.png)
