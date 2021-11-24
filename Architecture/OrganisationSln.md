Voici des exemples de comment organiser un projet dev (Exemple en .NET sln). Cela depend forcement des situations mais par défaut, la séparation physique aide mais trop séparé peut être contraignant.

Exemple :

* SRC
    * Domain: Core du projet (Entreprise Wide consent comme les Types/Entities/Exceptions, et qui sont pas limités à l'application. Ex un client) mais AUCUNE logique.
    * Application: Cela concerne sur ce que l'application est censé faire. On y met la structure comme les interfaces et l'abstraction (Pas l'implémentation, cela dépend que du domain). On a la logique mais pas l'implémentation
    * Infrastructure: L'implémentation est fait dans l'infrastructure
    * Presentation (WebUI) ===> Presentation Layer, it is the interface application (MVC, Blazor, ...). Top layer for customer. Il depend de l'application et de l'infrastructure layer. Il depend de l'infrastructure pour faire les services registrations sinon on se refere qu'aux interfaces pour l'abstraction !

* Test




On peut aussi ajouter un projet pour répondre à certains besoins selon le projet comme qui peuvent être facilement extrait en package :
* Technical Utilities
* Logging


Cela peut être utile si les choses vont évoluer et qu'il y aura plusieurs sln, mais ces projets auront à terme la même "structure".
