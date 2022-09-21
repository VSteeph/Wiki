# Architecture Logicielle

## Objectifs :
* High level Design
* Style d'architecture plus utilisée avec pros & cons et personalisation
* Savoir choisir une architecture

## Séparations des définitions 

* Coding: Low-Level (implementation)
* Design : Low-Level ?
* Architecture : High-level

Plusieurs vues :

Architecture Général:
* Vue de réalisation (Composants et leur relations)
* Vue Logique => Fonctionnelle
* Vue des cas utilisations => fonctionnelle
* Vue des processus (tech)
* Vue de déploiement (hardware)

Tout cela rentre dans le dossier d'architecture technique


L'architecture logicielle est l'assemblement de différents composants/fonctionnalités d'un système pour répondre à différents critères (résilliance, Scaling, etc). L'architecture doit référencer beaucoup d'éléments, elle n'est pas bas niveau. Par exemple, elle doit connaître les différentes éléments hardware mais pas besoin de connaître l'implémentation comme la configuration, ça c'est le low-level design.

## exemple de composants
* Serveur Web
* Database
* Load Balancer
* Distributed Cache Service
* Composant embarqué lourd
* Composant web

Exemple d'utilités: 
* Web socket (Gateway)
* Mesage Broker
* ESB (Entreprise Service Bus)

## différents styles

### Appels & Retours
Cela concerne la plupart des architectures orientés services ou composants distribuées. On peut avoir de l'orienté objet ou de l'orienté composants (DDD => Domain Driven Design qui est le fait de séparer (decouple) les éléments)

###
