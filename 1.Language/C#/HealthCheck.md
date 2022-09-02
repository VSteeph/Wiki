# Health Checks

Source: https://www.youtube.com/watch?v=Kbfto6Y2xdw

Cela permet de connaître l'état des serveurs et la stabilité de l'application. On peut même s'en servir pour dire au loadbalancer de redémarrer les serveurs. 

On peut décider de récupérer beaucoup d'informations sur le serveur comme :

* Est ce que le site est up?
* Est ce que les données sont bien récupérées?
* Est ce qu'il est rapide?
* Est ce que tous les composant de l'application fonctionnent correctement

UN healthcheck doit aussi être rapide et ne pas ralentir l'application. Plus ils ont executé fréquement, plus ils doivent être rapide
