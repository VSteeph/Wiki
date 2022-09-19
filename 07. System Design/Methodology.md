# Methodology générique

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

