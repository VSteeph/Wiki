# Microservices

Source : https://www.youtube.com/watch?v=j6ow-UemzBc
Sources: https://www.youtube.com/watch?v=DgVjEo3OGBI

## MicroServces uilités

Cela part du principe de Single Responsibility "Regrouper les éléments qui changent pour la même raison et séparer celles qui choses pour des raisons différentes. Un microservices est donc responsable pour faire un élément et est donc de petite taille en général. Les microservices peuvent avoir besoin d'informations et de parler à d'autres mais ils sont indépendants et les changements dans l'un ne causent aucun probleme dans un autre. Un microservices fait partie d'un tout (systeme) et il est self-contained, autononme.


## Avantage des microservices

Facile à changer, très facile à proposer d'autres contrats (alors que monolithe impossible de donner le contrat à une autre boite), très simple à déployer et changer. On peut adapter la technologie utilisée (déconseillée sauf si entreprise différentes) et très facile à scale, s'il y a un services qui est utilisée de manière intensive on peut upgrade le hardware juste poru ce service ou le rework en fonction des besoins (software vs hardware)

Le systeme est plus robuste car s'il y a un probleme, il y a qu'un seul élément qui plante et le tout est très simple à changer si on veut un autre services à la place.

## Desvantages microservices

Les microservices sont plus compliquésà  implémenter et à designer car il faut bien tout isoler et penser l'architecture. Cela peut mener à une analysis paralysis où on ne fait rien et on ne fait qu'analyser et comprendre comment faire l'architecture, cela demande dond beaucoup de knowledge de domaine. Les microservices sont indépendants mais doit toujours être liés à quelque chose (paradoxe) et l'ajout des microservices ou consolidification d'un microservices est beaucoup plus à décider

Les microservices sont distribués sur le réseau et DONC le réseau peut fail ou ralentir et les CI/CD, petit tweak sont plus durs à utiliser que sur un monolithe


Il est important que les hybrides avec quelques microservices autour d'un monolithe se fait.


## Implementation

### Package utilisé:

* AutoMapper.Extensions.Microsoft.DependencyInjection
* EntityFrameworkCore
* EntityFrameworkCore.Design
* EntityFrameworkCore.InMemory
* EntityFrameworkCore.Sqlserver


### infos en vrac

Contient Donnée:

* Models: données (internal representation de la donnée)
* Data Transfer Object : Vue externe des representations des données (DTO)




