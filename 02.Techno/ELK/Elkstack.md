Autres points à voir :
* Replica
* Snapshot
* Split & Shrink Sharding
* FileBeat + autres solutions 
* Filter avancé dans logstash
* Autres fonctions de kibana (APM, Metricsn Visualisation)

# Introduction ELK

ELK: Elastic Search, Logstash, Kibana. C'est le stack ELK qui permet de collecter des informations et les restituer que ça soit des logs, des métriques ou des SIEM (Sécurity Information and Event Management).

C'est un stack très complet et qui est très populaire dans l'industrie surtout pour les logs. Elle est gratuite mais il y a aussi une version payante qui est xpack.

## Definition

**Cluster:** ensemble des serveurs (noeuds/nodes) qui ont le même id cluster, il communique via un port

**Nodes:** Un serveur ayant un service Elastic, il y a plusieurs types (master, data, client)

**Index:** Une instance de base de donnée qui va être distribué et on peut en avoir plusieurs par serveur et cluster 

**Shards:** Découpage logique d'un index (1 à plusieurs shards) qui sont répartis sur plusieurs nodes du cluster qui permet d'avoir des meilleurs performances

**Réplicas:** Clone de shards qui permet d'avoir de la redondance en cas de problème mais aussi de la performance en interrogeant différents shards qui ont les mêmes données

**Documents:** éléments le plus petit

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

La force de logstash est dans son systeme de transform. Si c'est juste pour de l'envoie de log autant utiliser filebeat qui est plus léger.


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

### Elastic Search
Suivre le processus du site. On peut paramètrer les 3 fichiers de config pour configurer Elastic:
* jvm.options pour changer la puissance de la machine
* elasticsearch.yml pour changer la config de base (nom du cluster, nodes, hôte ou encore emplacement des logs/datas)
* log4j2.properties pour le logging

Une fois installé, il faut installer le .bat sur windows.

On peut utiliser un Docker volume pour avoir plusieurs nodes simplement ( https://www.youtube.com/watch?v=tdyzluB9PkQ)

### Kibana & ELK

Cela s'installe en suivant les étapes. On lance le fichier .bat sur windows et ils sont chacun un dossier config qu'il faut configurer. Kibana doit être relié à ELK et logstash doit avoir les sources de données renseignés.


# Configuration

## Configuration Logstash

Logstash marche sur le principe de Input/filter/output. La partie filter contient aussi la partie GROK qui permet de variabiliser une ligne de log. On peut avoir 2 fichiers de configurations dans logstash:

* Dossier pattern qui ont des fichiers avec des patterns (qui sont des regex qui permettent de capturer des éléments pour les sauvegarder dans des variables). Cela permet de les appeler plus simplement
* FIchier config de logstash

On peut travailler un pattern grâce à un grok debugger comme : https://grokdebug.herokuapp.com/. Cela permet de voir à quel variable peut correspondre les éléments et comment sera diviser dans les logs. Cela permet de donner une meilleur structure au logs.

Il y a aussi des exemples de pattern sur le site pour partir d'une base.

### Fichier Config logstash

On a plusieurs éléments dans la config :

**INput pour réupérer les données:**

```
input {
	file {
		path =>"C:\log\test\log.log" ===> qui donne l'emplacement du fichier
		start_position => "beginning" ==> A partir de quand on prend les informations
		sincedb_path => "/dev/null" ====> Si logstash prend un repère pour pas prendre des logs en doublon. Avec dev/null, il reprend depuis le début, il a pas de repère.
	}
}
```


**Filter pour changer les données:**

```
filter{
	grok{
		patterns_dir =>"path" ==> emplacement du pattern
		match => { "message" => "%{IPORHOST} %{NGUSER:ident} } ==> ce qu'on fait pour match le pattern
	}
}
```

**Output pour envoyer les données:**

```
output {
  elasticsearch {
    hosts => ["http://localhost:9200"]
    index => "%{[@metadata][beat]}-%{[@metadata][version]}-%{+YYYY.MM.dd}"  ==> cela donne un suffixe qui permet d'avoir un index par jour et ce qui fait gagner en performance et facilite le ménage de logs
  }
}
```

on peut mettre autant de file qu'il y a de fichier et on peut faire un mapping et un output unique pour tous les inputs 

Exemple final:

```
input {
   file{
   path => "tmp/log1.log"
   add_field => { "[@metadata][es_index]' => "front1-%{+YYYY.MM.dd}"}
   }
      file{
   path => "tmp/log2.log"
   add_field => { "[@metadata][es_index]' => "front2-%{+YYYY.MM.dd}"}
   }
      file{
   path => "tmp/log3.log"
   add_field => { "[@metadata][es_index]' => "front3-%{+YYYY.MM.dd}"}
   }
}

filter {
   dissect {
      mapping => {
         "message" => "%{sourceip} %{date} %{other}"
        }
  }
}

output {
    elasticserach {
        hosts => ["127.0.0.1:9200]
	ilm_rollover_alias => "myilm"
	ilm_pattern => "00001"
	ilm_policy => "myilm-policy"
	manage_template => true
	template => "/etc/logstash/app.json"
	template_name => "mytemplate"
    }
}

```

## Configuration Kibana

Pour pouvoir regarder les index, il faut avoir un index pattern dans Management => Stack Management. En écrivant, le début de l'index on peut ajouter des symboles comme * pour dire qu'on recupère tous les index sans prendre en compte la date, exemple :

* preprod* va récupérer les index qui ont pour format prepreprod-2021-12-01, preprod-2021-12-02 et etc

En suite, il faut déterminer comment on gère le timestamp (par défaut @timestamp). A partir de la, on aura la liste des champs utilisées par cet index.

Les informations sont visualisables dans le discover. Chaque champ est accessible avec la nomenclature "champ: valeur", ex => response: 404

# Index Templates

Dans Kbiana, l'index Tempalte se trouve dans l'index management, l'onglet Index template. On peut décider de créer un nouveua template ou d'en modifier un existant. Pour en modifier un, il faut cliquer sur un index puis Manage => Edit.

On y voit plusieurs champs, voici les principaux :

Nom du template
* La liste des index concernées (Accepte les index patterns)
* Components : (Mappings & Settings peuvent être bien)
* En appuyant sur Next, on arrive à un JSON qu'on peut modifier pour rendre le template plus complet en ajoutant un ILM ou un rollback Alias.

Exemple:

```JSON
{
  "index": {
    "format": "1",
    "lifecycle": {
      "name": "ilm-history-ilm-policy",
      "rollover_alias": "ilm-history-2"
    },
    "hidden": "true",
    "number_of_shards": "1",
    "auto_expand_replicas": "0-1",
    "number_of_replicas": "0"
  }
}
```

On peut les créer soit dans Kibana soit dans logstash. Par défaut, ElasticSearch et Logstash décident le mapping seul. Si on exploite les données, c'est bien d'avoir un template avec un type de données fixes, sinon on peut être dans un mapping dynamic.

Le dynamic mapping peut être à "true", "false" ou "strict". Si on est à true, on peut ajouter des champs sans poser de problèmes mais on peut pas changer sur ce qui est déjà mappé. Si on est à false, tout ce qui n'est pas dans le mapping est ignoré. Le strict lui refuse et déclenche une erreur si y a d'autres éléments.

Logstash permet de gérer le mapping comme ceci :

```
output {
manage_tempalte => true
template => "/template/template.json"
template_name => "templateName"
}
```

## Construire un Template

Pour associer un fichier template à logstash, il faut le créer. Il a plusieurs paramètres :

```JSON
{
    "index_patterns": ["app*"], ==> ce qui est ous les index patterns qui auront ce template
    "template": "app", => nom du template
    "version": 1,
    "settings": {
        "index.refresh_interval": "5s" ==> permet de changer le temps de refresh, utile pour le testing, sinon pas besoin à part être lourd en performance
},
"mappings": {
   "dynamic": true, ==> le dynamic mapping
   "properties": {
       "@timestamp": {
          "type": "date"
	  },
       "@version": {
          "type": "text",
	  "fields": "text",
	   "keyword": {
	   	"type": "keyword",
		"ignore_above":256
		}
	  },
       "date": {
          "type": "text",
	  "fields": "text",
	   "keyword": {
	   	"type": "keyword",
		"ignore_above":256
		}
   }
```
A noter que s'il y a d'autres champs dans le filter du configue de logstash, ils seront ignorés ou créeront une erreur en fonction du dynamic mapping.

# Index Lifecycle Management (ILM)

C'est une nouvelle feature d'ELK qui est geré soit directement dans logstash soit dans kibana. L'ILM est la gestion dans le temps des données. Il a plusieurs degrés de la données:

* hot: données qui est récent, toujours alimenté et interrogés regulièrement (Cela correspond à l'archivage du fichier de log)
* warm: pas de mise à jour mais est toujours interrogé (Fichier de log archivé)
* Cold: Pas de mise à jour, peu interrogé mais on l'a garde par sécurité, on peut utiliser du stockage lent.
* Delete: Plus besoin, elle est supprimée

Cela va de paire avec le rolling qui va changer le nom de l'index exemple :
* nomIndex_0001
* nomIndex_0002
* nomINdex_0003

Cela a pour utilité de créer un lien symbolique et de pouvoir injecter les données dans le derneir index. C'est à dire qu'on va interroger l'alais qui est le dernier index plutôt que les autres.

C'est configurable dans Kibana dans Index Lifecycle Policies (Space Management) et on peut choisir les actions et le temps avant d'effectuer un rollover avant chaque phase. On peut choisir de supprimer le fichier, de freeze les données ou même de réduire le nombre de shards ou même de changer sur un node moins puissant.

Pour que tout marche il faut un Alias et un index template.

On crée donc un Index Template dans Kibana. On y configure le nombre de shards, replicas, nom, alias, la politque à appliquer (ILM) et un mapping:

Settings :
```JSON
{
  "index": {
    "format": "1",
    "lifecycle": {
      "name": "logstah-policy",
      "rollover_alias": "logstah-policy-2"
    },
    "hidden": "true",
    "number_of_shards": "1",
    "auto_expand_replicas": "0-1",
    "number_of_replicas": "0"
  }
}
```

Mappings:

```JSON
{
  "properties": {
    "@timestamp": {
      "type": "date"
    },
    "@version": {
      "type": "keyword"
    }
  }
}
```

## ILM via logstash

On précise un template avec toutes les informations : index, shards, replicas, les mappings et on peut suivre un template pour toutes les entrées selon une logique avec des variables

On ajoute les informations dans l'output du logstash config :

```
output {
   elasticsearch {
      hosts => ["ip"]
      ilm_rollver_alias => "rolloverALias"
      ilm_pattern => "000001"
      ilm_policy => "ILM_policy_name"
      manage_tempalte => true
      template => "/path/of/template"
      template_name => "mytemplatename"
   }
}
```
