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

Chaque niveau se regroupe dans plusieurs vues qui sont les suivantes:(Modele de Kruchten  4 + 1) 

* Vue de réalisation => Diagram des composants et leurs relations (tech)
* Vue Logique => Interaction des différents objets métiers (métier)
* Vue des cas utilisations => Diagram des cas d'utlisations (métiers)
* Vue des processus => Processus & thread, etat(transitions (technique)
* Vue de déploiement => Diagram du déploiement hardware (tech)


L'architecture peut avoir des contraintes lié au code, à l'hardware mais c'est une couche d'abstraction au-dessus et ce n'est pas l'oeuvre d'une personne, il faut prendre les avis des gens, construire ensemble pour voir  les différnets pitfalls en avance, chacun ses maitrises, et tout n'est pas sur un seul schéma. C'est important de comprendre les besoins et les gens. Il n'y a pas de normes et d'éléments absolus.

Il faut pas se perdre dans les documents et faire plein de spécifications détailles et de se figer dans un système absolu.


## Documentation
On utilise différents languages pour modéliser des systèmes comme :*
* UML (Standard même dans les cas particuliers)
* SysML (systeme Machine)
* AADL (Beaucoup orienté calcul)

Une architecture doit dont être documenté (DAT => dossier d'architecture technique). Il peut aussi avoir un Guide de Design des composants pour ajouter des objectifs, des particularités sur chaque composants ce qui permet d'avoir des guidelines pour l'implementation low-level

### DAT
Le DAT doit avoir :

#### Vision du produit
Una page max. C'est un résumé du projet rapide pour pouvoir comprendre de quoi parle le sujet, quels sont les cibles, les objectifs, les métrics, les couts, etc. Il est là pour donner une rapide overview. Il prend en compte un Lean canva :
![image](https://user-images.githubusercontent.com/58773222/191470125-4ca6fbe8-d87e-49da-92a6-706309fc1aef.png)


#### Facteurs déterminants
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

#### Liste Macroscopique de fonctionnalité (Vue Architecturale)

C'est le fait de décrire les différentes fonctionnalités du système (Ex : Cuisine, Service, Livraison, Approvisionnement, Payement, resevation, etc). Cela inclut la motvation du choix des styles et le détai des composants avec leur déploiements.

#### Metriques de qualités

Ce sont les métriques qu'on utilise pour déterminer les métriques pour mesurer la qualité d'un système, quelles variables on utilise pour mesurer nos objectifs. Il y a un exemple de thème avec les normes ISO 25010
![image](https://user-images.githubusercontent.com/58773222/191449262-7891f6fe-e614-4a31-86d3-5015a92b551c.png)

#### Monitoring & Metrics

Cela revient un peu avec les métriques de qualités mais il est important de définir un système de Monitoring et comment on récupère les logs, est ce que cela colle par rapport à nos besoins (Ecrire dans un fichier, export dans un service externe, batch les fichiers logstash), qu'est ce qu'on a besoin de monitorer.

#### Liste des composants
Un tableau Excel des différents éléments. Ce

### Mecanismes de sécurités


#### Flux échanges et protocoles utilisées
Il est important d'y refléchir et de les définir quand cela répond à un besoin ou une particularité. Exemple, Whatsapp qui communique en websocket car il y a besoin de réponse pour savoir si un message est livré ou lu.


## Composants principaux 

### Application Client Lourd (Composant Desktop)
ça peut être une grosse application ou juste un bash sans aucune interaction. Il peut aussi avoir un potentiel traitement métier (elle peut aussi être extraite). Cela centralise l'IHM (Interface Homme Machine)

Contraintes à prendre en compte :
* Environnement Cible (OS, Machine ressource limitée ou non)
* Portabilité: 
    * Langage de programmation nativement portable comme .NET Core, Java
    * Recompiler selon les OS avec un livrable adaptée
    * Plusieurs versions par OS
* Déploiement et mises à jour
    * Déploiement depuis site distant (Interroge Service externes pour vérifier les versions et on télécharge et installe les nouveaux fichiers aux démaragge de l'appli)
    * Système de Notification lors d'une montée de version (Donc c'est pas l'appli qui vérifie, c'est le service qui envoie un message à l'appli)
    * Forcer le déploiement/maj depuis le réseau (Solution réseau)
    * Systeme de gestions de plugins (déploiement à chaud/froid)
* Sécurité
    * mécanisme d'authentification
    * Chiffrement de la communication
    * Chiffrement / hashashe des données sensibles (Chaine de connexion, etc) 
    * Sécurisation du code source (Obfuscation du livrable) et s'il y a du code vraiment super secret,c'est pas à mettre sur la machine


##### Définitions :

**Chiffrement symétriques** : 1 clé secrète unique pour crypter et decrypter (Encryptage : AES, DES, RC4/RC5, Misty1)

Bob (Crypte message avec cléSecrete) ==> Alice (Decrypte avec cléSecrete)

**Chiffrement Asymétriques**: Chaque acteur génère 2 clés (Privée/public). Les clés publiqus sont communiquées mais elles ne permettent que d'encrypter mais pas de decrypter un message. Encryptage : RSA

Bob (crypte message avec cléPubAlice) ====> Alice (Decrypte avec cléPrivAlice)
Bob (Decrypte message avec cléprivBob) <=== Alice (Crypte message avec CléPubBob)

**Hash** : Transforme une donnée initiale en une empreinte non-déchiffrable. Encryptage : MD5 (Trop vieux), SHA-256, SHA-512, Bcrypt

Exemple : mot de passe

### Composant Web
Une application client léger deployé sur un serveur. En gros, c'est une application côté serveur qui va récupérer et formatter un résultat et fourni cette réponse sous un format spécifique (html/css/js) qui est compatible avec l'application Client (Browser).

Il y a aussi des technologies côté client comme Angular. Au premier appel, tout le code va etre téléchargé côté client qui permet de requeter directement des services web qui vont fournir des données brutes et le formattage se fera côté client, ce qui permet d'alléger le traffic réseau et la charge du serveur et cela permet de créer de l'interactivité mais selon le type de machine, cela peut ralentir pour certains clients et tout le code est téléchargée côté client (en clair) donc Aucune donnée sensible

Contraintes:

* Navigateur doit pouvoir supporter les fonctionnalités ou utiliser des librairies (polyfills) pour combler le manque
* Portabilité : uniquement si on utilise une technologie non-portable (Ex : Framework => Windows / IIS)
* Déploiement : remplacement de l'application sur le serveur (Besoin d'uptime ou non)
    * facilité le déploiement de l'application en intégrant dans un contenur l'application et son environnement d'execution
* Gestion des sessions: Est ce que les données sont utiles côté serveur ou non ? ou est ce qu'on le store (Client, Base de donnée, Cache centralisée, etc)
    * Le volume des données impacte où on stock les données (10mb max en général côté serveur)
    * Finalité des données (Traitement métier ou non), est ce qu-elle est nécessaire côté serveur ? (peut-on la perdre?)
    * Persistance des données (besoin de garder/conserver les données sur la durée)
    * Cout (cela donne des couts en plus niveau hardware)
    * Où stocker les données : Serveur ou Client ? ==> Cache distribuée (voire bdd mais plus rare)
* Sécurité
    * Crypter les échanges (HTTPS) - utilisation de certificats SSL (Secure socket Layer, port TCP protégé). Les émetteurs est forcement un tier de confiance et pas le site. Les communications sont encryptés avec une clé publique. Premiere
    * Crypter les données stockées
    * Authentification

#### définition :

**session HTTP**: Espace mémoire pour chaque visiteur (PHP non automatique), elle peut être stockée côté serveur ou côté application client (LocalStorage / SessionStorage). Le suivi des sessions 'effectue grâce à un ID unique vehiculé dans un cookie ou URL. cela peut être aussi garder avec une affinité de session dans le Load Balancing, comment créer de la redondance et de la persistance de donnée (Distributed Cache System, Base de donnée, RAM serveur Web)

**Communication HTTPS (Modele OSI):**
![image](https://user-images.githubusercontent.com/58773222/191521517-15b51bf2-1bba-438c-92c7-d9833b7d7882.png)

Plus on monte en couche, plus c'est rapide mais moins maniable

**Certificat SSL** : Premiere requete estnon chiffrée et le serveur fournit le certificat. Le browser va verifier s'il est correct et va récupérer la clé publique dans le certificat. Il pourra ainsi envoyer de requetes privées aux serveurs, cependant si c'est asymétrique le client ne pourra voir l'information, donc il envoie aussi une clé symétrique crypté avec la clé publique au serveur.

Les échanges suivant auront lieu avec la clé symétrique, donc le premier échange se fait en asymétrie puis le chiffremeent est symétrique.

**Authentification**
Les users peuvent etre dans une base de donnée ou dans un Annuaire LDAP (Lightweight Directory Access Protocol) avec Users, Groupes (openLdap, Active Directory)

Appli qui veut se connecter avec plusieurs éléments. Cela peut directement aller chercher dans la BDD ou l'annuaire.


### Load Balanceur

Réparitteur de charge sur plusieurs serveurs

Contraintes:
* Types : Materiel vs Logiciel
    * Material : Redirige des requte HTTP/TCP mais plus rapide
    * Logiciel : plus customisable 
    * Souvent c'est décidé par l'architecte systeme mais on peut se mettre d'accord en fonction dfes besoins
    * Considératiosn de conceptions : failover, reprise avec incident, affinité de session, etc


### Bibliotheque

Ensemble d'entités et fonctions métiers packagées dans une archive (Dll/so, jar) ou repertoire

Contraintes:
* Comptabilités de version / dependances
* Chargement Static ou Dynamique ==> Consommation de ressourcs vs réactivité
    * Static: au déméragge 
    * Dynamique : au besoin 
* Interopérabilité entre langages. Posible ou alors créer une interface (SOAP/REST ou tout autre protocole pour communiquer et fournir les données) qui permet de passer par un code normalement inutilisable 


### Application mobile
APplication deployée chaque terminal mobile donc tres proche de l'application lourd (tpe desktop) mais il y a des contraitnes en plus

**Contraintes supplémentaires**
* Fonctionnalités supportées par le device (NFC, BLuetooth)
* Type d'usage (connecté, non connecté)
* Mode de développement (natif, web mobile donc responsive, hybride qui permet d'avoir une grosse base tronc commun et adapter le reste pour générer du natif) comme Cordova, Xamarin, MAUI
    * Hybride suffit dans la majeure partie des cas mais il peut être limité en performance (accéder à l'équipement du telephone)

### Web Service

Application Web sans IHM deployée sur un serveur web qui expose un ensemble de méthodes


Définitions :

**SOAP** Simple Object Access Protocol, c'est un protocol de communication basée sur du XML (req formalisée avec entête, corps et potentiellement pièce jointe). C'est assez lourd. Le Web Service doit avoir un STub Utilitaire conv qui est un .wsdl pour pouvoir importer les définitions. Cette importation va créer un stub (contrat d'interface) dans le client. Si un jour, le service client à changer, il faut prévenir tous les clients que le contrat à changer pour le mettre à jour sinon cela ne marchera pas donc ce n'est plus utilisée car c'est compliqué pour les applications distribuées à beaucoup de clients

**REST**(Representational State Transfer) Architecture basée sur le protocole HTTP. Le format de donnée est pas imposée, pas d'enveloppe spécifique, on utilise les concepts de base HTTP (entête et corps), on peut avoir du XML ou avoir un format plus léger comme du JSON ou même juste du texte/binaire.
Avantages : pAs de contrat d'interfaces formel côté client ce qui permet de changer sans à avoir à informer tous les clients

**GRAPHQL**: Alternative à REST qui permet de créer des requêtes pour extraire des données de plusieurs sources en un seule appel (Tres lourd donc peu utilisée) mais c'est un bon choix quand il y a un vrai besoin.


### Autres 
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

## Différents styles

### Appels & Retours
Cela concerne la plupart des architectures orientés services ou composants distribuées. On peut avoir de l'orienté objet ou de l'orienté composants (DDD => Domain Driven Design qui est le fait de séparer (decouple) les éléments)

### Architecture en couche
C'est les architectures qui sont divisées en plusieurs tiers.

### Architecture centrée sur les données
C'est une architecture qui est moins utilisé à l'heure actuelle avec une base de donnée centrée sur les données avec plein d'éléments autour.

### Flot de donnée
C'est beaucoup utilisé dans des batch processing, c'est quand on a des données qui va traverser une série de composants pour arriver à l'output final

## Gestion de projet

Il existe 2 types d'approches :
* Approche predictive (Cycle en V, cascade), prévoir les phases séquentielles avec un engagemenesur un planning précis. L'architecture se fait au moment de la conception Global.
* Approche agile : Construire un processus itératif et incrémental qui consister à découper le projet en itération. L'architecture est faite au démarrage du projet et est remis en cause à chaque début de sprint voir même review de sprint 

## UML
![image](https://user-images.githubusercontent.com/58773222/191460878-8279d849-1811-4f0c-955c-dcc7e67c81f0.png)

Exemple de logiciel : Modelio (UML), Draw, Yed

Types de liasons :
* Généralisation (Extends en dev qui est de l'héritage un peu) et pas forcement extends de l'UML qui est une couche en plus
* Inclusion c'est forcement inclus
* Extension c'est une possibilité d'avoir en plus


## Les vues

### Vue Utilisations
Un cas d'utilisation représente une séquence d'interaction des utilisateurs avec le systèmes. Diagram UML

### Vue Logiques
Identification les différents éléments et mécanismes du systèmes à réaliser (Diagram statics, composites, etc) C'est les différents éléments du systèmes. Elle est representée par des diagrames statiques d'objets enrichis de descriptions dynamiques (composite, activité)

### Vue de processus
Décrit les interactions entre les différents processus ou threads/taches. Cela permet d'exprimer la synchronisation et l'allocation. Processus est la logique et les threads sont l'unité physique qui executent les processus, donc multithreading ou pas. L'idée est donc de mettre en avant et les relations entre les éléments, ce qui est dépendant de quel processsus, etc
Cela permet de vérifier le respect de contraintes, la fiabilité, efficacité et performance.

Les diagrams utilisés sont dynamiques (activité, séquence, communication, etc)

#### Vocabulaire 

Le multi threading est du mutli tâches (round-robin techniquement) ce qui est pas forcement synonyme de performance. L'objectif est de libérer le thread principal pour executer une tache de fond. Cela peut poser des problèmes avec le context switching et c'est aux développeurs de créer et synchroniser les threads. C'est utile quand le processeur a du downtime pa exemple.

Le parallélisme utilise le multi threading mais délègue la gestion des threads à l'OS. Gestion des classe manuelle (C# => Thread ou alors Parallel pour gérer l'OS). Par contre, en parallélisme on perd le contrôle de la séquence, donc même uen boucle for ne s'éxecute pas forcement dans le bon ordre car l'ordinateur répartit la charge sur plusieurs threads donc une énumération ne sera plus dans l'ordre dans le parallélisme.

Threading => Libérer un thread et d'effectuer une autre tache spécifique
Parallélisme => Performance
Asynchronisme => pas de communication bloquante, c'est à dire qu'on a pas besoin d'attendre la réponse d'un autre élément et on utilise des callback pour effectuer les actions à ce moment la


### Vue de réalisation

Ce sont l'organisation des composants dans l'environnemenet et cela permet de gérer la configuration. Les diagrams suivent une certaine rigueur, exemple :
![image](https://user-images.githubusercontent.com/58773222/191467109-05632b29-11cc-4c23-9604-24a08fd6ba4b.png)

L'idée c'est de montrer les points d'extensions du système. C'est plutôt du fonctionnel et comment on va implémenter

### Vue de déploiement

Cela représente le système et son environnement, les contraintes geographiques, réseaux, tolérancex aux fautes/pannes et le type de livrable (.rar, .exe, etc). On peut y inclure les protocoles de communications et les cardinalités (qui appellent quoi avec la redondance)
![image](https://user-images.githubusercontent.com/58773222/191467879-b5d09b57-8340-41ac-9fd7-6e52de553da8.png)


## Développer un modèle architecturale
