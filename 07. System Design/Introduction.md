# System Design
Un Systeme Design est le façon de créer un système qui permet de satisfaire plusieurs contraintes.

Prenons un cas simple, on a crée un Algorithme qui intéresse plusieurs personnes. On va mettre à disposition l'accès à ce code mais pas le code directement. On expose donc le code par Internet avec une API (Application Programming Interface) pour permettre à des personnes externes d'executer le code et de récupérer l'ouput. Les clients font faire des request et le système va renvoyer une réponse adaptée à la requête.

Ce système peut avoir plusieurs requirements comme une base de donnée, de configurer les endpoints, ce qui se passe quand la machine est HS (courant, Erreur, etc) car des gens ont payé pour l'accès. 

Pour éviter les problèmes de machine et d'uptime, c'est mieux de passer par le cloud comme A(mazon) W(eb) S(ervices) pour que les problèmes leur incombent plutôt que de gérer plusieurs serveurs qui prennent le rélais. Le cloud est en gros un ensemble d'ordinateurs à utiliser, ce qui permet d'éviter de se focaliser sur les problèmes matériels et plutôt sur tout le reste.

## Business Requirements

Il peut avoir plus requirements pour un Système Design, le premier est la charge qu'il doit pouvoir assurer. A force d'augmenter le nombre
