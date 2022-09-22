## Composants principaux 

## Application Client Lourd (Composant Desktop)
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


#### Définitions :

**Chiffrement symétriques** : 1 clé secrète unique pour crypter et decrypter (Encryptage : AES, DES, RC4/RC5, Misty1)

Bob (Crypte message avec cléSecrete) ==> Alice (Decrypte avec cléSecrete)

**Chiffrement Asymétriques**: Chaque acteur génère 2 clés (Privée/public). Les clés publiqus sont communiquées mais elles ne permettent que d'encrypter mais pas de decrypter un message. Encryptage : RSA

Bob (crypte message avec cléPubAlice) ====> Alice (Decrypte avec cléPrivAlice)
Bob (Decrypte message avec cléprivBob) <=== Alice (Crypte message avec CléPubBob)

**Hash** : Transforme une donnée initiale en une empreinte non-déchiffrable. Encryptage : MD5 (Trop vieux), SHA-256, SHA-512, Bcrypt

Exemple : mot de passe

## Composant Web
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

### définition :

**session HTTP**: Espace mémoire pour chaque visiteur (PHP non automatique), elle peut être stockée côté serveur ou côté application client (LocalStorage / SessionStorage). Le suivi des sessions 'effectue grâce à un ID unique vehiculé dans un cookie ou URL. cela peut être aussi garder avec une affinité de session dans le Load Balancing, comment créer de la redondance et de la persistance de donnée (Distributed Cache System, Base de donnée, RAM serveur Web)

**Communication HTTPS (Modele OSI):**
![image](https://user-images.githubusercontent.com/58773222/191521517-15b51bf2-1bba-438c-92c7-d9833b7d7882.png)

Plus on monte en couche, plus c'est rapide mais moins maniable

**Certificat SSL** : Premiere requete estnon chiffrée et le serveur fournit le certificat. Le browser va verifier s'il est correct et va récupérer la clé publique dans le certificat. Il pourra ainsi envoyer de requetes privées aux serveurs, cependant si c'est asymétrique le client ne pourra voir l'information, donc il envoie aussi une clé symétrique crypté avec la clé publique au serveur.

Les échanges suivant auront lieu avec la clé symétrique, donc le premier échange se fait en asymétrie puis le chiffremeent est symétrique.

**Authentification**
Les users peuvent etre dans une base de donnée ou dans un Annuaire LDAP (Lightweight Directory Access Protocol) avec Users, Groupes (openLdap, Active Directory)

Appli qui veut se connecter avec plusieurs éléments. Cela peut directement aller chercher dans la BDD ou l'annuaire.


## Load Balanceur

Réparitteur de charge sur plusieurs serveurs

Contraintes:
* Types : Materiel vs Logiciel
    * Material : Redirige des requte HTTP/TCP mais plus rapide
    * Logiciel : plus customisable 
    * Souvent c'est décidé par l'architecte systeme mais on peut se mettre d'accord en fonction dfes besoins
    * Considératiosn de conceptions : failover, reprise avec incident, affinité de session, etc


## Bibliotheque

Ensemble d'entités et fonctions métiers packagées dans une archive (Dll/so, jar) ou repertoire

Contraintes:
* Comptabilités de version / dependances
* Chargement Static ou Dynamique ==> Consommation de ressourcs vs réactivité
    * Static: au déméragge 
    * Dynamique : au besoin 
* Interopérabilité entre langages. Posible ou alors créer une interface (SOAP/REST ou tout autre protocole pour communiquer et fournir les données) qui permet de passer par un code normalement inutilisable 


## Application mobile
APplication deployée chaque terminal mobile donc tres proche de l'application lourd (tpe desktop) mais il y a des contraitnes en plus

**Contraintes supplémentaires**
* Fonctionnalités supportées par le device (NFC, BLuetooth)
* Type d'usage (connecté, non connecté)
* Mode de développement (natif, web mobile donc responsive, hybride qui permet d'avoir une grosse base tronc commun et adapter le reste pour générer du natif) comme Cordova, Xamarin, MAUI
    * Hybride suffit dans la majeure partie des cas mais il peut être limité en performance (accéder à l'équipement du telephone)

## Web Service

Application Web sans IHM deployée sur un serveur web qui expose un ensemble de méthodes

Contraintes:
* Même contraintes que pour une application Web
* Granularité : Micro-services (périmetres limité et indépendant donnée wise)


Définitions :

**SOAP** Simple Object Access Protocol, c'est un protocol de communication basée sur du XML (req formalisée avec entête, corps et potentiellement pièce jointe). C'est assez lourd. Le Web Service doit avoir un STub Utilitaire conv qui est un .wsdl pour pouvoir importer les définitions. Cette importation va créer un stub (contrat d'interface) dans le client. Si un jour, le service client à changer, il faut prévenir tous les clients que le contrat à changer pour le mettre à jour sinon cela ne marchera pas donc ce n'est plus utilisée car c'est compliqué pour les applications distribuées à beaucoup de clients

**REST**(Representational State Transfer) Architecture basée sur le protocole HTTP. Le format de donnée est pas imposée, pas d'enveloppe spécifique, on utilise les concepts de base HTTP (entête et corps), on peut avoir du XML ou avoir un format plus léger comme du JSON ou même juste du texte/binaire.
Avantages : pAs de contrat d'interfaces formel côté client ce qui permet de changer sans à avoir à informer tous les clients

**GRAPHQL**: Alternative à REST qui permet de créer des requêtes pour extraire des données de plusieurs sources en un seule appel (Tres lourd donc peu utilisée) mais c'est un bon choix quand il y a un vrai besoin.

**Requetes** : Service web avec systeme d'authentification, génération Token qui permet de rester identifier pendant un certain temps. JWT => En clair, Jeton signé et protoocle en HTTPS pour que cela soit crypté et pas recupéré

JWT vs OAuth2 : JWT (Json Web Token) qui est un standard pour définir un Jeton qui va être vehiculé mais il y a aucun protocole indiqué alors que OAuth2 est un protocole qui permet de gérer l'identification entierement et peut utiliser des JWT. OAuth2 impose d'avoir un serveur à part pour l'authentification alors qu'avec un serveur custom, on peut décider de l'endroit où un mec l'authentification. On peut aussi créer notre propre Token

OpenIdConnect (basé sur Oauth2)

## Autres 
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

## API Gateway
C'estune passerlle API qui sert de point dentrée unique pour les APIs

Contraintes :
* Performances
* Fonctionnalités offertes


## Web Socket
Protocole d'échange full duplex qui maintient une connexion TCP unique entre dfeux noeud, ce qui permet d'avoir du temps réel dans les deux sens. Mode Asynchrone, on réagit à un message reçu donc on peut avori des events, il est tres lourd comme il maintient une connexion ouverte (Aka whatsapp)

Problème du protocole HTTP:
* One way Protocole (on peut utilise l'Ajax  mais c'est surtout client => Serveur)
* Tres verbeux, beaucoup d'informations


## Middleware Orienté Messages

Systeme de communication asynchrone à base de message avec une file d'attente, ce qui permet de séparer l'émetteur et le consommateurs du messages.

Contraintes:
* Type de file d'attente
* Gestion de persisance
* Choix du protocole: AMQP, MQTT, HTTP, STOMP, JMPS
* Gestion de l'ordre des messages


## Entreprise Service Bus

Le bus est la pour interconnecter plusieurs applications multi-protocolaires avec un fort besoin d'agilité. Il est en général en asynchrone. Il est constitué d'un Message Broker avec des services pour rerouter et transformer les messages.

## Composant de stockage

* Serveur de fichier
* Base de donnée (Relationnelle ou NosQL)
* Cache (Volatile donc pas persistant)



Contraintes :
* Volume des données
* Structure de stockage


**SQL vs NoSQL :**

Le SQL a pas de standard donc chaque version a un sandard.

Le noSQL a 4 types de stockages :

* Clé-valeur => Redis
* graph => Neo4J 
* Colonne => Cassandra (nom, valeur, timestamp)
* Document => MongoDB => valeur de type JSON ou XML stocké en binaire (BSON ou BXMl)

Avantages :

* Scalable horizontal accrue
* Conception simplifiée
* Performances améliorée en cas de gros volume de données (1to par jour au moins)

Inconvenients:
* 

**Stockage d'image** :

* Colonne TEXT pour Base64 Encode un fichier en text-binaire avec 64 caracteres ce qui permet de récupérer le fichier selon le type
* Colonne de type blob qui stock le binaire du logo
* Colonne de type varchar qui contient le stock le chemin vers le fichier physique stocké sur un serveur de fichiers

1ere & 2eme solution : l'information est disponible immédiate mais dans la 1ere base c'est dur de restaurer les BDD quand on a des restauration. La 2eme prend du temps dans sa conversation.

La 3eme solution permet de séparer le contenu de l'emplacement mais cela demande de gérer 2 choses (avec stratégie de sauvegarde et restauration). Le fichier est déjà prêt

Protocoles pour parler à un serveur:

* FTP ou FTPs (sécurisé mais bon
* SFTP => FTP en tunnel SSH Secure Shell)
* SMB /INTFS (acces réseau local)
* CFT  (peu utilisé)
* HTTP / WebDav en mettant un serveur et laisser les serveurs exposer (Webdav extensions du HTTP Web-Based Distributed Authoring and Versioning, cela permet aux users d'editer en simultannée et versionner)

En général, c'est bien d'avoir son service de fichiers (gateway) qui peut récupérer les images en sFTP. Cela permet d'avoir un service qui est responsable de récupérer les fichiers. Cela permet de plus facilement s'etendre si on ajoute des applications
