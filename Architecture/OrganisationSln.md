Voici des exemples de comment organiser un projet dev (Exemple en .NET sln). Cela depend forcement des situations mais par défaut, la séparation physique aide mais trop séparé peut être contraignant.

Exemple :

* SRC
    * Domain: Core du projet (Entreprise Wide consent comme les Types/Entities/Exceptions, et qui sont pas limités à l'application. Ex un client) mais AUCUNE logique.
    * Application: Cela concerne sur ce que l'application est censé faire. On y met la structure comme les interfaces et l'abstraction (Pas l'implémentation, cela dépend que du domain)
    * Infrastructure: L'implémentation est fait dans l'infrastructure
    * WebUi ===> Presentation Layer, it is the interface application (MVC, Blazor, ...). Top layer for customer.

* Test

