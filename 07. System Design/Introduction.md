# System Design
Un Systeme Design est le façon de créer un système qui permet de satisfaire plusieurs requirements.

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

## Methodology générique

Le principal problème dans le Systeme Design est comment scale un système pour qu'il puisse faire face à la demande. Pour cela, il y a plusieurs étapes qui ajoutent en complexité au fur et à mesure qu'on avance, cela permet d'assumer plus de traffic, d'avoir un système plus scalable et plus résilient en échange de complexité :

* Optimisation des process existants et améliorer l'output avec les même ressources => Vertical Scaling
* Préparer les charges de travail en dehors des peak hours => Preprocessing & CronJob
* Garder des backup et éliminer les Single Point of Failure => Master/Slave Architecture
* Mettre à disposition plus de ressources qui existe déjà (serveurs) => Horizontal Scaling
* Spécialisé les ressources dans un domaine (Exemple: serveur pour les Commande CLick'n'Collect et un pour les commandes MarketPlace) => Microservices architecture, ce qui permet de scale individuellement les domaines les plus demandant
* Gros Backup qui copie le système actuel pour en faire un Système de backup, cela ajoute beaucoup de complexité surtout dans la communication => Distributed System (Positioning donc plus proche pour plus rapide response time, élimine single point of failure et backup plan)
* Place central pour permettre de distribuer les requêtes de façon intelligentes basé sur un critère response time (Load + Distance) => Load Balancing


A partir de cette étape, le système est déjà assez conséquent. Un Système est noté sur plusieurs paramètres comme sa résilience, Scalability, Extensibility et Fault Tolerancy. On commence à séparer les responsabilités. Le load balancing est pas lié aux types d'objets qui est produits dans les systemes (Voiture, Bouffe, etc) et les systèmes ne sont pas liés au load balancing, l'origine de l'appel est pas important

* Decoupling : On sépare les concerns pour qu'on puisse gérer des systèmes séparés et pus efficacement
* Loggings and Metrics: Cela permet de bien comprendre les évenements de tout logs et noter
* Garder le système Extendable pour pas avoir à ré-écrire tout le code. Si le code doit être ré-écrit parce qu'on change de spécificités c'est qu'il y a un prbolème.

## Mindset

Il y a le High-level design qui est de determiné le type de problème que l'on rencontre et comment on les résoud. C'est à déployement de serveurs, comment les systèmes interagissent.

L'opposé est le Low-level Design qui est plutôt comment on va coder ces éléments, les classes, les fonctions. C'est l'implémentation et comment faire une implémentation efficace et clean. C'est convertir des requirements en code. On va souvent utiliser des diagrams (UML, Activity, sequences, class Diagrams). Le point important est que c'est très détaillé et très technique

