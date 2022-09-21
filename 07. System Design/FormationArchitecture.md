# Architecture Logicielle

## Objectifs :
* High level Design
* Style d'architecture plus utilisée avec pros & cons et personalisation
* Savoir choisir une architecture

## Définitions 

L'architecture logicielle est l'assemblement de différents composants/fonctionnalités d'un système pour répondre à différents critères (résilliance, Scaling, etc). L'architecture doit référencer beaucoup d'éléments, elle n'est pas bas niveau. Par exemple, elle doit connaître les différentes éléments hardware mais pas besoin de connaître l'implémentation comme la configuration, ça c'est le low-level design.

Il y a plusieurs niveux d'architecture :

* Coding: Low-Level
* Design : Low-Level ?
* Architecture : High-level

Chaque niveau se regroupe dans plusieurs vues qui sont les suivantes: 

* Vue de réalisation => Diagram des composants et leurs relations (tech)
* Vue Logique => Interaction des différents objets métiers (métier)
* Vue des cas utilisations => Diagram des cas d'utlisations (métiers)
* Vue des processus => Processus & thread, etat(transitions (technique)
* Vue de déploiement => Diagram du déploiement hardware (tech)


L'architecture peut avoir des contraintes lié au code, à l'hardware mais c'est une couche d'abstraction au-dessus et ce n'est pas l'oeuvre d'une personne, il faut prendre les avis des gens, construire ensemble pour voir  les différnets pitfalls en avance, chacun ses maitrises, et tout n'est pas sur un seul schéma. Il n'y a pas de normes et d'éléments absolus.



## Documentation
On utilise différents languages pour modéliser des systèmes comme :*
* UML (Standard même dans les cas particuliers)
* SysML (systeme Machine)
* AADL (Beaucoup orienté calcul)

Une architecture doit dont être documenté (DAT => dossier d'architecture technique). Il peut aussi avoir un Guide de Design des composants pour ajouter des objectifs, des particularités sur chaque composants ce qui permet d'avoir des guidelines pour l'implementation low-level

### DAT
Le DAT doit avoir :

#### Vision du produit
Una page max. C'est un résumé du projet rapide pour pouvoir comprendre de quoi parle le sujet, quels sont les cibles, les objectifs, les métrics, les couts, etc. Il est là pour donner une rapide overview

#### Facteurs déterminants
Ce sont les facteurs qui vont décider et limiter le design car ils sont fondamentaux comme le fait que ça soit un système embarqué, un système militaire, les besoins en sécurité, le nombre d'utilisateurs

#### Liste Macroscopique de fonctionnalité

C'est le fait de décrire les différentes fonctionnalités du système (Ex : Cuisine, Service, Livraison, Approvisionnement, Payement, resevation, etc)

#### Metriques de qualités

Ce sont les métriques qu'on utilise pour déterminer les métriques pour mesurer la qualité d'un système, quelles variables on utilise pour mesurer nos objectifs. Il y a un exemple de thème avec les normes ISO 25010
![image](https://user-images.githubusercontent.com/58773222/191449262-7891f6fe-e614-4a31-86d3-5015a92b551c.png)



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
