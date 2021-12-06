# ELK

ELK: Elastic Search, Logstash, Kibana. C'est le stack ELK qui permet de collecter des informations et les restituer que ça soit des logs, des métriques ou des SIEM (Sécurity Information and Event Management).

C'est un stack très complet et qui est très populaire dans l'industrie surtout pour les logs. Elle est gratuite mais il y a aussi une version payante qui est xpack.

## ElasticSearch

* Base de donnée NoSQL (Distribuée). L'avantage c'est d'être distribuée à grande échelle et plus le cluster est grand, plus sa résillience est forte.
* Fortes volumétries
* Spécialistes dans les recherches "plaint-text" 
* Utilisent des outils d'index/sharding/replicas
  * Sharding est le découpage des index pour distribuer ces index (sorte de db) sur tous les nodes du cluster
  * Replicas qui permet d'éviter les perdres de données
* Moteur Lucene qui a une limite de 2 milliard de document donc très puissant
* Requete sont au format REST (Format JSON)


## LogStash
* Un principe ETL (Extract, Transform, Load)
* Il extrait d'un Input, il filtre les informations et les envoie à Elastic ce qui correspond à ces étapes : Input/Filter/output
* Plusieurs plugins d'entrées comme Nginx, postgres qui permet de typer les entrés qui arrivent pour les traiter plus facilement
* Peut faire des filtres et des grok (grok c'est pour parser les données en champ)


## Kibana
* Outil de Visualisation et de Requêtes
* Spécialié au stack ELK (Avec options de management)
* Dashboard & Visualisation

