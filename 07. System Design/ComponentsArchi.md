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


Définitions :

**SOAP** Simple Object Access Protocol, c'est un protocol de communication basée sur du XML (req formalisée avec entête, corps et potentiellement pièce jointe). C'est assez lourd. Le Web Service doit avoir un STub Utilitaire conv qui est un .wsdl pour pouvoir importer les définitions. Cette importation va créer un stub (contrat d'interface) dans le client. Si un jour, le service client à changer, il faut prévenir tous les clients que le contrat à changer pour le mettre à jour sinon cela ne marchera pas donc ce n'est plus utilisée car c'est compliqué pour les applications distribuées à beaucoup de clients

**REST**(Representational State Transfer) Architecture basée sur le protocole HTTP. Le format de donnée est pas imposée, pas d'enveloppe spécifique, on utilise les concepts de base HTTP (entête et corps), on peut avoir du XML ou avoir un format plus léger comme du JSON ou même juste du texte/binaire.
Avantages : pAs de contrat d'interfaces formel côté client ce qui permet de changer sans à avoir à informer tous les clients

**GRAPHQL**: Alternative à REST qui permet de créer des requêtes pour extraire des données de plusieurs sources en un seule appel (Tres lourd donc peu utilisée) mais c'est un bon choix quand il y a un vrai besoin.


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