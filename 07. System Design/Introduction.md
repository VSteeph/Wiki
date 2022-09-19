# System Design
Un Systeme Design est le façon de créer un système qui permet de satisfaire plusieurs contraintes.

Prenons un cas simple, on a crée un Algorithme qui intéresse plusieurs personnes. On va mettre à disposition l'accès à ce code mais pas le code directement. On expose donc le code par Internet avec une API (Application Programming Interface) pour permettre à des personnes externes d'executer le code et de récupérer l'ouput. Les clients font faire des request et le système va renvoyer une réponse adaptée à la requête.

Ce système peut avoir plusieurs requirements comme une base de donnée, de configurer les endpoints, ce qui se passe quand la machine est HS (courant, Erreur, etc) car des gens ont payé pour l'accès. 

Pour éviter les problèmes de machine et d'uptime, c'est mieux de passer par le cloud comme A(mazon) W(eb) S(ervices) pour que les problèmes leur incombent plutôt que de gérer plusieurs serveurs qui prennent le rélais. Le cloud est en gros un ensemble d'ordinateurs à utiliser, ce qui permet d'éviter de se focaliser sur les problèmes matériels et plutôt sur tout le reste.

## Business Requirements

Il peut avoir plus requirements pour un Système Design, le premier est la charge qu'il doit pouvoir assurer. A force d'augmenter le nombre d'utilisateurs, le serveur peut avoir des ralentissements ou voir être down. Il y a plusieurs façons de compenser ça :

* Acheter une plus grosse Machine => Ordinateur plus puissant => Vertical Scaling
* Acheter plus de machine => Division des tâches => Horizontal Scaling

Le fait de pouvoir gérer plus de request en adaptant son infrastructure s'appelle la "scalability", c'est en gros, on peut gérer plus de requête avec plus d'argent. Comme pour tout, chaque évolution a des avantages & inconvéniants


### Differences entre les Scaling

Un Horizontal Scaling a besoin d'un Load Balancing contrairement à un Vertical Scaling. Cela permet de rediriger le traffic.

Par contre, si une machine échoue en Horizontal scaling, le traffic peut être redirigé alors que dans le Vertical SCaling, on a un "Single Point of Failure", c'est le concept de "Resilience".

La communication entre les ordinateurs se fait par le réseau tandis que cela se fait par le système dans un ordinateur. La communication est donc plus rapide et plus fiable en Inter Process Communication (Vertical) vs Network Calls (Horizontal) RPC (Remote PRocedure Calls).

Enfin, le dernier point est la consistance de donnée (Data consistancy). Imagine qu'on a une transaction entre plusieur ordinateurs, c'est dur de maintenir les données en horizontal contrairement au vertical qui permet de s'assurer que tout est consistant.

Néanmoins, le vertical scaling a une limite qui est celle du hardware alors que l'horizontal peut être scale de manière quasiment infini (linéaire) à moins d'avoir un bottleneck important.

## Solutions

Dans le monde réel, on utilise les 2 en fonctions des besoins avant d'utiliser les qualités que l'on souhaite selon le cas. On utilise le Vertical Scaling pour la consistance des données et la communication fiable et rapide tandis qu'on utilise l'horizontal SCaling pour le scaling et la résiliance.

En gros, c'est pas si hybride. C'est juste un système horizontal avec les plus gros serveurs possibles en terme de budget
