# Document Architecture technique

Le DAT doit avoir :

## Vision du produit
Una page max. C'est un résumé du projet rapide pour pouvoir comprendre de quoi parle le sujet, quels sont les cibles, les objectifs, les métrics, les couts, etc. Il est là pour donner une rapide overview. Il prend en compte un Lean canva :
![image](https://user-images.githubusercontent.com/58773222/191470125-4ca6fbe8-d87e-49da-92a6-706309fc1aef.png)


## Facteurs déterminants
Ce sont les facteurs qui vont décider et limiter le design car ils sont fondamentaux comme le fait que ça soit un système embarqué, un système militaire, les besoins en sécurité, le nombre d'utilisateurs. Liste non exhaustive :

* Environnement Cible
* Typologie d'application
* Expérience Utilisateurs 
* BNombre utilisateurs
* Disponibilité
* Performance
* Durée de vie
* Sécurité
* ROI
* Compétence
* Sécurité
* Interaction avec des SI existant/externes

## Liste Macroscopique de fonctionnalité

C'est le fait de décrire les différentes fonctionnalités du système (Ex : Cuisine, Service, Livraison, Approvisionnement, Payement, resevation, etc).

## Vues Architecturales
Le détail des composants, leur déploiement et leur relations etnre eux (Fonctionnelles, techniques, motivation des choix)

## Flux échanges / Protocoles utilisées
Il est important d'y refléchir et de les définir quand cela répond à un besoin ou une particularité. Exemple, Whatsapp qui communique en websocket car il y a besoin de réponse pour savoir si un message est livré ou lu.

## Mecanismes de sécurités

## Monitoring & Metrics
Cela revient un peu avec les métriques de qualités mais il est important de définir un système de Monitoring et comment on récupère les logs, est ce que cela colle par rapport à nos besoins (Ecrire dans un fichier, export dans un service externe, batch les fichiers logstash), qu'est ce qu'on a besoin de monitorer.

Comment stocker les logs :

Fichiers:
* Plus rapide
* Format libre
* Prévoir la rotation de log
* Attention aux entrées/sorties ==> Ressources importants
* Gestion des acces concurrents

Base de donnée :
* Structure imposée ou non
* Recherche Rapide
* Question de Purge des données

Solution Externe type ELK
* Accessible au travers de multiples protocoles (HTTPs ou autre)
* Agrégation de logs depuis plusieurs applications 
* indexaiton automatique des logs
* outils associés
* Plus couteux

Si on stock que des éléments liées à l'application elle-même, un simple fichier est suffisant

Si on stock

## Metriques de qualités

Ce sont les métriques qu'on utilise pour déterminer les métriques pour mesurer la qualité d'un système, quelles variables on utilise pour mesurer nos objectifs. Il y a un exemple de thème avec les normes ISO 25010
![image](https://user-images.githubusercontent.com/58773222/191449262-7891f6fe-e614-4a31-86d3-5015a92b551c.png)



## Liste des composants
Un tableau Excel des différents éléments. Ce


## Stratégie de sauvegarde et de restauration
