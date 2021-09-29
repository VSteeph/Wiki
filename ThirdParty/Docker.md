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

Docker permet d'avoir un systeme donc allégé et de récupérer uniquement les éléments dont on a besoin. C'est donc des layer beaucoup plus léger et en plus, ces layers sont indépendants.

Par exemple, un web serveur est un container de 55mb, mais si on prend 2 container qui utilise la même image (même webserver) on a pas 110mb car on copie et reutilise les éléments, cela sera juste les différences entre les 2 (donc souvent juste certains fichiers). On peut donc avoir 10 différents containers de web services pour 60mb

## Créer une image

Une image est un layer supplémentaire. On a le base OS, le web serveur layer et un file layer. Une image est en readonly. Cela permet de créer un point dans le temps qui est stable et toujours identique. On peut donc executer l'image et toujours avoir la même base. Le container peut évoluer mais l'image est toujours le même et on part toujours du même point de départ.

### Configuration

* Créer un fichier qui permet d'avoir un set up, le fichier s'appelle : dockerfile (sans extension)
* Avoir une image de base pour pouvoir ajouter les layers. Il faut le premier layer, qui peut être un OS et construire par dessus ou une image déjà construite qu'on peut récupérer sur le site de docker
* On prend les informations dans le container pour créer le dockerfile, on peut utiliser uen version spécifique avec un tag ou directement le latest
** from httpd:2.4 (le 2.4 est le tag, ça peut donc être aussi httpd:latest
* on choisit aussi les fichiers qu'on recupere avec COPY path destination 

Il y a aussi toutes les informations et configuratiosn dans le dockerfile
 
### Build

Une fois que la configuration est fini, on va build l'image dans la console avec :
docker build -t name:tag . // exemple : docker build -t hello-docker:1.0.0 . // il ne faut pas oublier le . à la fin pour mettre la fin

## Run un Docker

Il est important de préciser qu'un container prend une image et l'execute mais si on détruit un container, on repart de l'image. ça veut dire que les fichiers sont supprimés des que le container est détruit. Les fichiers enregistrés dans un container sont temporairement et pour l'execution, pas du stockage de donnée.

Pour l'executer, on utilise 

docker run -d --name NomDuContainer -p PortMachineHost:PortDansLeContainer NomDeLimage:TagDeLImage
Ex : docker run-d --name first-container -p:8080:80 hello-docker:1.0

-d est pour disconnect pour continuer à être executer en background même si on ferme le programme qu'il l'a lancé, sinon le docker est lié au programme.

--name est le nom du controller

-p est le port du container (utile pour les webservices) avec le port à l'intérieur du container (exemple : 8080:80 veut dire c'est le port 8080 de la machine host et le port 80 du contrôller

## Manage running Container

docker ps -a permet d'avoir la liste de tous les containers et le statut (Créer, expirer, etc)

en général, on utilise les 3 premiers éléments du containerID pour le referencer et on peut utiliser ce genre commande :

docker stop id ou docker start id

On peut aussi faire docker rm id pour supprimer le container, on peut aussi supprimer une image avec docker rmi id (remove image)


