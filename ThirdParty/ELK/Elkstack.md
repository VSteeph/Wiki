# Introduction ELK

ELK: Elastic Search, Logstash, Kibana. C'est le stack ELK qui permet de collecter des informations et les restituer que ça soit des logs, des métriques ou des SIEM (Sécurity Information and Event Management).

C'est un stack très complet et qui est très populaire dans l'industrie surtout pour les logs. Elle est gratuite mais il y a aussi une version payante qui est xpack.

## Definition

Cluster: ensemble des serveurs (noeuds/nodes) qui ont le même id cluster, il communique via un port

Nodes: Un serveur ayant un service Elastic, il y a plusieurs types (master, data, client)

Index: Une instance de base de donnée qui va être distribué et on peut en avoir plusieurs par serveur et cluster 

Shards: Découpage logique d'un index (1 à plusieurs shards) qui sont répartis sur plusieurs nodes du cluster qui permet d'avoir des meilleurs performances

Réplicas: Clone de shards qui permet d'avoir de la redondance en cas de problème mais aussi de la performance en interrogeant différents shards qui ont les mêmes données

## Stack

### ElasticSearch

* Base de donnée NoSQL (Distribuée). L'avantage c'est d'être distribuée à grande échelle et plus le cluster est grand, plus sa résillience est forte.
* Fortes volumétries
* Spécialistes dans les recherches "plaint-text" 
* Utilisent des outils d'index/sharding/replicas
  * Sharding est le découpage des index pour distribuer ces index (sorte de db) sur tous les nodes du cluster
  * Replicas qui permet d'éviter les perdres de données
* Moteur Lucene qui a une limite de 2 milliard de document donc très puissant
* Requete sont au format REST (Format JSON)


### LogStash
* Un principe ETL (Extract, Transform, Load)
* Il extrait d'un Input, il filtre les informations et les envoie à Elastic ce qui correspond à ces étapes : Input/Filter/output
* Plusieurs plugins d'entrées comme Nginx, postgres qui permet de typer les entrés qui arrivent pour les traiter plus facilement
* Peut faire des filtres et des grok (grok c'est pour parser les données en champ)


### Kibana
* Outil de Visualisation et de Requêtes
* Spécialié au stack ELK (Avec options de management)
* Dashboard & Visualisation


Il peut avoir des variations comme en remplaçant le logstash par des beats comme filebeat (pour récupérer des logs), metricbeats pour des metrics, etc

## Concurrents:
* ElasticSearch avec comme qualité recherche (surtout plain text) qui est lié à sa capacité d'indexation
* Cassandra avec comme qualité le gros volume
* mongodb qui est plus polyvalent
* Redis in memory donc beaucoup plus rapide

La force d'ElasticSearch vient du fait de son indexation où tous les mots sont indexés et la qualité de sa recherche grâce à :
* TF (Term Frequency): fréquence des mots
* IDF (Inverse difference Frequency): moins un mot est commun, plus il a du poids



## Installation ELK


