# Methodology

Le principal problème dans le Systeme Design est comment scale un système pour qu'il puisse faire face à la demande. Pour cela, il y a plusieurs étapes qui ajoutent en complexité au fur et à mesure qu'on avance, cela permet d'assumer plus de traffic, d'avoir un système plus scalable et plus résilient en échange de complexité :

* Optimisation des process existants et améliorer l'output avec les même ressources => Vertical Scaling
* Préparer les charges de travail en dehors des peak hours => Preprocessing & CronJob
* Garder des backup et éliminer les Single Point of Failure => Master/Slave Architecture
* Mettre à disposition plus de ressources qui existe déjà (serveurs) => Horizontal Scaling
* Spécialisé les ressources dans un domaine (Exemple: serveur pour les Commande CLick'n'Collect et un pour les commandes MarketPlace) => Microservices architecture, ce qui permet de scale individuellement les domaines les plus demandant
* Gros Backup qui copie le système actuel pour en faire un Système de backup, cela ajoute beaucoup de complexité surtout dans la communication => Distributed System (Positioning donc plus proche pour plus rapide response time, élimine single point of failure et backup plan)
* Place central pour permettre de distribuer les requêtes de façon intelligentes basé sur un critère response time (Load + Distance) => Load Balancing
