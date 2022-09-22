# Cas Pratique Architecture 

## Assurance (Services d'offres de différents type update tous les 6 mois

Une assurance à plusieurs clients (Mobile, Desktop, Browser + portail) qui doivent pouvoir accéder à une série d'offres qui sont dans plusieurs services.

![image](https://user-images.githubusercontent.com/58773222/191707739-3aa272bc-7ca2-4ec8-9a82-93c4aece483b.png)


### Problème classique

1. Il faut pouvoir stocker les offres dans une base de donnée parce qu'on veut éviter de faire une série d'appel et de re-attaquer, reuniformiser les services qui fournissent les offres
2. Une base de donnée est liée à son service et doit être géré uniquement par son service


### Solution Simplifiée

![image](https://user-images.githubusercontent.com/58773222/191708077-2beaf564-7cd9-40fb-9acb-9b19e172ceae.png)

Il y a un extracteur qui utilise une API gateway qui gère l'authentification et tout pour récupérer les API et un File Gateway pour gérer la récupération des fichiers. cette solution n'est pas très demandante. Elle consiste en 2 parties avec une base de donnnée:

* La récupération des données (Gateways + Extracteur)
* L'exposition des données (Offers Services)

### Solution plus compl_te

![image](https://user-images.githubusercontent.com/58773222/191708675-592ba7a3-0b4f-4bf0-9a33-14141778c878.png)

Le fait de passer par l'API Gateway au lieu de directement l'Offer services présetne plusieurs avantages :

* Une meilleur sécurité, l'API n'est pas exposé, on a une meilleur sécurité. On est en DMZ, c'est à dire que seul la Gateway est exposé
* Facilement redondable, on peut avoir plusieurs gateway facilement contrairement au service
* On peut passer par un messages services si on a besoin d'asynchrone
* Point central pour les metrics et les logs
