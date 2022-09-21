# Architecture Logicielle

## Objectifs :
* High level Design
* Style d'architecture plus utilisée avec pros & cons et personalisation
* Savoir choisir une architecture

## Définitions 

Il y a plusieurs niveux d'architecture :
* Coding: Low-Level (implementation)
* Design : Low-Level ?
* Architecture : High-level (Focus ici)

Architecture Général:
* Vue de réalisation => Diagram des composants et leurs relations (tech)
* Vue Logique => Interaction des différents objets métiers (métier)
* Vue des cas utilisations => Diagram des cas d'utlisations (métiers)
* Vue des processus => Processus & thread, etat(transitions (technique)
* Vue de déploiement => Diagram du déploiement hardware (tech)

L'architecture logicielle est l'assemblement de différents composants/fonctionnalités d'un système pour répondre à différents critères (résilliance, Scaling, etc). L'architecture doit référencer beaucoup d'éléments, elle n'est pas bas niveau. Par exemple, elle doit connaître les différentes éléments hardware mais pas besoin de connaître l'implémentation comme la configuration, ça c'est le low-level design.

## Documentation
On utilise différents languages pour modéliser des systèmes comme :*
* UML (Standard même dans les cas particuliers)
* SysML (systeme Machine)
* AADL (Beaucoup orienté calcul)

Une architecture doit dont être documenté (DAT => dossier d'architecture technique). Il peut aussi avoir un Guide de Design des composants pour ajouter des objectifs, des particularités sur chaque composants ce qui permet d'avoir des guidelines pour l'implementation low-level

### DAT
Le DAT doit avoir :

* 1 page: Vision du Produit (Résumé du projet rapide pour pouvoir comprendre de quoi parle le sujet, quels sont les cibles, les objectifs, les métrics, les couts, etc)
* Facteurs déterminants / Contraintes d'architecture (Exemple: embarqué, militaire, distribué, pérénité, sécurité, Nombre d'utilisateurs, etc)
* Liste Macroscopique de fonctionnalités (Ex : Cuisine, Service, Livraison, Approvisoinement)

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

### Architecture en couche
C'est les architectures qui sont divisées en plusieurs tiers.

### Architecture centrée sur les données
C'est une architecture qui est moins utilisé à l'heure actuelle avec une base de donnée centrée sur les données avec plein d'éléments autour.

### Flot de donnée
C'est beaucoup utilisé dans des batch processing, c'est quand on a des données qui va traverser une série de composants pour arriver à l'output final
