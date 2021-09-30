# Docker

Source : https://www.youtube.com/watch?v=WcQ3-M4-jik

Download: https://www.docker.com/get-started

images: https://hub.docker.com/

## Preparation

Installer Docker et la virtualisation ainsi que le package WSL :
https://docs.docker.com/desktop/windows/troubleshoot/#virtualization
https://docs.microsoft.com/en-us/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package

I lfaut aussi activer dans le BIOS la virtualisation (dans les option du CPU, SVM par exemple)

C'est préférable de faire fonctionner Docker avec Linux plutôt que Windows même sous windows car il y a plus de container et c'est plus léger sauf s'il y a besoin de Windows en particulier (Exemple: .NET Framework, mais pour .NET Core, Go linux)

On peut arrêter la machine virtuelle pour avoir moin de ram avec :

wsl --shutdown et il suffit de faire wsl pour le relancer (powershell)

## Docker Vs Virtual machine

Une virtual machine ont a une couche OS et par-dessus cette couche, on trouve les applications. Le bloc entier est une virtual machine mais c'est quelque chose de très large avec beaucoup d'éléments.

Docker essaye de limiter ce qui est limitable. Si on part du principe qu'une machine virtuelle s'execute sur une autre machine qui a aussi un OS et une couche applicative (qui contient le software), ce qui est de la duplication et ça dans le code ou pour tout, c'est du nono.

Docker recupere l'OS de l'host donc celui de base et ne veut pas re-installer un nouvel OS entierement, il va ajouter un layer à l'OS de l'host ce qui permet d'avoir une version allégé avec le minimum possible (pas d'UI, pas d'utilities), puis on ajoute des mini layers d'exactement ce dont on a besoin. Chaque layer correspond à des environnements et des depedencies. Cela permet d'avoir la version la plus allégée possible d'une machine virtuelle.

Toutes les informations nécesssaires forment une image. C'est à dire une version super allégée de Linux avec SQL & Apache2 qui marchent et absolument rien d'autres. Docker est donc une série de layer.

C'est à dire que Docker Linux prend la base du Subsysteme de Linux windows et ajoute le minimum de Linux (1er layer).

### Avantages de Docker

Docker permet d'avoir un systeme donc allégé et de récupérer uniquement les éléments dont on a besoin. C'est donc des layer beaucoup plus léger et en plus, ces layers sont indépendants. C'est donc plus rapide, plus léger.

En plus des éléments, Docker permet d'avoir une configuration de base et donc un environnement identique peu importe qui l'installe et ou.

Par exemple, un web serveur est un container de 55mb, mais si on prend 2 container qui utilise la même image (même webserver) on a pas 110mb car on copie et reutilise les éléments, cela sera juste les différences entre les 2 (donc souvent juste certains fichiers). On peut donc avoir 10 différents containers de web services pour 60mb

## Créer une image

Une image est un layer supplémentaire. On a le base OS, le web serveur layer et un file layer. Une image est en readonly. Cela permet de créer un point dans le temps qui est stable et toujours identique. On peut donc executer l'image et toujours avoir la même base. Le container peut évoluer mais l'image est toujours le même et on part toujours du même point de départ.

L'intérêt des iamges est aussi de les upload sur un repo public ou private pour qu'elle puisse etre facilement récupérable/déployer sur un environnement de test,prod ou local.

### Configuration

* Créer un fichier qui permet d'avoir un set up, le fichier s'appelle : dockerfile (sans extension)
* Avoir une image de base pour pouvoir ajouter les layers. Il faut le premier layer, qui peut être un OS et construire par dessus ou une image déjà construite qu'on peut récupérer sur le site de docker
* On prend les informations dans le container pour créer le dockerfile, on peut utiliser uen version spécifique avec un tag ou directement le latest
** from httpd:2.4 (le 2.4 est le tag, ça peut donc être aussi httpd:latest
* on choisit aussi les fichiers qu'on recupere avec COPY path destination 

Il y a aussi toutes les informations et configuratiosn dans le dockerfile

On peut aussi ajouter des variables d'environnement lock mais c'est mieux de mettre les variables dans le docker-compose car c'esrt plus simple à override.

On peut ajouter des commandes linux aussi avec run (autant qu'on veut), c'est les commandes qui sont effectués DANS le container, à ne pas confondre avec copy qui est entre l'host et le container

execute specifique commande en fonction du container (cmd dans node executer sever.js par exemple) pour servir d'entry point. On peut avoir plein de RUN mais un seul entry point.

Exemple:

```
FROM node:tag

ENV username=admin
    password=password
    
RUN mkdir -p /home/app

COPY ./home/app

CMD ["node","server.js"]
```
 
### Build

Une fois que la configuration est fini, on va build l'image dans la console avec :
docker build -t name:tag . // exemple : docker build -t hello-docker:1.0.0 . // il ne faut pas oublier le . à la fin pour mettre la fin

## Run un Docker

Il est important de préciser qu'un container prend une image et l'execute mais si on détruit un container, on repart de l'image. ça veut dire que les fichiers sont supprimés des que le container est détruit. Les fichiers enregistrés dans un container sont temporairement et pour l'execution, pas du stockage de donnée.

Pour l'executer, on utilise 

docker run -d --name NomDuContainer -p PortMachineHost:PortDansLeContainer NomDeLimage:TagDeLImage
Ex : docker run-d --name first-container -p:8080:80 hello-docker:1.0

-d est pour dettach pour continuer à être executer en background même si on ferme le programme qu'il l'a lancé, sinon le docker est lié au programme.

--name est le nom du controller

-p est le port du container (utile pour les webservices) avec le port à l'intérieur du container (exemple : 8080:80 veut dire c'est le port 8080 de la machine host et le port 80 du contrôller

Selon les images et le dockerfile, il y a différent éléments et parametres optionelles ou non à renseigner lors du run

## Manage running Container

docker ps -a permet d'avoir la liste de tous les containers et le statut (Créer, expirer, etc)

en général, on utilise les 3 premiers éléments du containerID pour le referencer et on peut utiliser ce genre commande :

docker stop id ou docker start id

On peut aussi faire docker rm id pour supprimer le container, on peut aussi supprimer une image avec docker rmi id (remove image)


## Docker commandes

* docker pull (pour récupérer une image)
* docker build (pour construire une image)
* docker run (pour créer un ccontainer) (-i permet de rendre intreactif si on a besoin d'input spécifique, et -it pour interactif + terminal)
* docker start/stop pour lancer/arrêter un container
* docker ps pour avoir la liste des processus
* docker logs (docker logs id ou name) pour récupérer les logs du container | tail pour avoir les derniers logs ou -f pour avoir le flux continu
* docker exec -it (pour avoir un terminal interactif qui permet d'ouvrir le bash du terminal comme un SSH en gros) & on quitte avec exit
* docker attach pour attacher le docker au programme 
* docker inspect
* docket network ls (pour avoir la liste des informations des networks des containers
* docker network create nom-du-reseau (pour créer un réseau)
* docker-compose -f pathDuFichier up (il peut ne pas être installer) (le up signifie ce qu'on fait avec ce yaml up pour lancer, down pour arrêter)

Il est important de préciser que comme les docker images sont très légeres, il n'y a pas toutes les commandes dans le terminal docker.

## environnement variable

On peut ajouter des variables d'environnement avec -e (exemple)
docker run -e App_Color=blue

on peut aussi changer une variable d'environnement avec
docker inspect nom (ou id)

## Compose
Pour ne pas lancer tous les containers à la main à chaque fois, on peut utiliser docker compose qui est un fichier yaml qui est la map des commandes de docker. ça a la structure suivante :

```yaml
version:'3' (Version de ddocker compose)
services:
    container-name:
        image: id ou lien du repositori où l'iamge est hebergé sinon il va par défaut sur dockerhub (il faut que l'nevironnement soit logged in sur le repo)
    second-container-name:
        image: image-use 
        ports:
            -8080:80
        environment:
            -Username...
            -Password...
        volumes:
           -db-data:/var/lib/mysql/data (named volume avec pour nom db-data
           
    volumes:
        db-data
```

Le docker compose s'occupe de créer un common network pour tous les containers du compose et on exeute le fichier avec docker-compose

## Interagir entre les containers

Docker crée un network isolé sur la machine host, donc quand on déploie plusieurs containers sur le même docker, les containers peuvent échanger des informations sans port, internet et directement avec le protocole de docker et leur id container, tandis que que pour tout ce qui est endehors la machine (appli ou même container) échange les informations avec un protocole classique.

Il est possible de créer des networks sur docker avec la commande: docker network create name

## Data-Persistance

Comme on a vu les données d'un container disparaisse lorsque le container s'arrête, ce qui est bien pour avoir un environnement fresh et toujours identique mais moin bien quand on veut sauvegarder des données, surtout quand le container est une base de donnée.

Pour cela, on a besoin de Docker Volumes. Un container a un virtual File Systeme (/var/lib/mysql/data par exemple) et sur la machine host on a un physical File systeme. Volumes permet de relier le Virtual File systeme à un dossier du physical file systeme, donc quand docker écrit sur son dossier, les données sont repliquées sur le dossier physique et inversement. C'est à dire que s'il y a un changement sur le dossier physique, le dossier virtuel est modifié.

### Mettre en place docker volumes

Il y a plusieurs types de dockers volumes:

Façon 1 (host volume):
docker run -v HostDirectory:Container directory (ex: docker run -v /home/Container-1/data:/var/lib/mysql/data, cela permet de décider où on veut et de controller ce dossier

Facon 2 (anonyme volume):
docker run -v VirtualPath et docker s'occupe de tout , c'est un volume anonyme. ex: docker run -v /var/lib/mysql/data

Façon 3 (named volume): 
Version improve qui permet de créer le dossier du volume anonmye (named volumes))
docker run -v name:path (ex : docker run -v name:/var/lib/mysql/data

En général, c'est les named volume qui sont utilisé car il y a des avantages à laisser docker gérer les volumes directories directement. On peut évidememnet l'intégrer à Docker Compose.

On peut associer un named volume à plusieurs container.

## Debugging
