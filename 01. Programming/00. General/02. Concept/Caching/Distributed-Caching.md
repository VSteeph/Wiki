# Caching

## Source

* https://www.youtube.com/watch?v=U3RkDLtS7uY

## What is a cache

Lorsqu'il y a un serveur et une base de donnée, l'utilisateur demande une donnée, le serveur va faire une requete en base de donnée pour fournir les donnés à l'utilisateur. Il y a plusieurs scénarios dans lequel on peut utiliser un cache :

- **Objectif : économiser des appels réseaux** Récupération de données très souvent demandées, exemple : la météo du jour. On enregistre les données dans le cache pour éviter beaucoup d'opérations. Pour cela, on peut avoir un cache dans le serveur (in-memory cache), cela stock les informations en clé-value. 
- **Objectif : éviter des lourdes calculations** Exemple, on veut récupérer la moyenne d'age de tous les utilisateurs. Tres couteux, donc on le fait une fois et on le store dans le cache.
- **Objectif: alléger la charge de la base de donnée** Exemple, on a beaucoup de serveurs qui font des appels en base de donnée donc grosse charge sur la base de donnée. On peut avoir plusieurs services de cache distribuées pour alléger la charge en base de donnée qui eux appels la base de donnée

L'objectif principal d'un cache pour éviter l'attente d'un client et d'accélerer le temps de réponse pour avoir des réponses le plus rapide possible.

## Limites du cache

Les avantages d'un cache peuvent donner envie de stocker l'ensemble des informations dans le cache mais on ne peut pas trop faire ça car le matériel(hardware) sur lequel fonctionne les caches est beaucoup plus cher qu'une base de donnée, ils sont souvent sur des SSD.

De plus, plus on stock d'informations sur le cache, plus les recherches vont être longues et donc autant appeler la base de donnée.

## Cache-Policy

La base de donnée a une source infinie de donnée alors que le cache doit avoir les données les plus relevants basés sur les informations qui vont arriver dans le futur, il y a donc une part de prediction. Cela amène plusieurs questions :

- Quand on fait une entrée dans le cache (entry / load)
- Quand est ce qu'on sort une donnée du cache (evict)

Ces réponses aux questions sont la cache-policy. La performance d'un cache dépend uniquement de cette policy. Il y a plusieurs Policy :

- LRU (Least Recently Used) Cela veut dire que quand on ajoute une information, elle est mise en haut (la plus récente 1s) et on sort l'information qui est la plus ancienne tout en bas (1h, 1J, 1mois). C'est une des plus utilisé et simple.
- LFU (Least Frequently Used) C'est utilisé tres rarement en cas pratique

Il y a aussi d'autres policy qui performent tres bien parfois même mieux que LRU comme:
- Sliding Windows Based Policy

## Probleme

Si on a une mauvaise policy, c'est que le cache est juste un extra call qui ralentit et donc c'est négatif. 

Si le cache est trop petit, les informations vont s'écraser en permanance et donc cela limitera les informations. Ce concept s'appelle "Trashing" où le cache load/delete les données sans utiliser les résultats en permnance

Le dernier problème est lié à la consistency des informations lorsqu'une information est mise à jour en base de donnée et qu'elle devient outdated mais est toujours utilisé

## Ou placer le cache

Le cache peut être placé proche de la database ou proche du serveur :

- Cache in-memory du serveur, c'est les résultats les plus rapides possibles mais cela va prendre la mémoire du serveur. Cela pose aussi le problème du serveur failure, qu'est ce qu'il se passe pour le cache et les données . Qu'est ce qui se passe si les caches sont pas en sync et que selon le front, les informations ne sont pas les mêmes. C'est aussi simple à implémenter

- Global Cache (entre les 2) Distributed Global Cache:  L'avantage c'est que tous les fronts requetent sur le cache, c'est limité en taille donc il query les DB on-miss. C'est plus rapide que la base de donnée avec un systeme come Redis. Cela permet d'aller plus vite mais avec moins de problème qu'un in-memory serveur et ne pose aucun porblème  en cas de crash, donc plus lentement mais plus précis.

Global Cache est plus safe et c'est assez rapide quand même. C'est aussi plus facile à scale et permet de garder les serveurs en tant que container sans avoir leur donnée bloqué par le site.

Si besoin de simplicité à implementer et de résultat tres rapide, on peut mettre dans le cache

## Data Consistency

Il y a plusieurs façons de gérer la Data consistency avec plusieurs façons :

- Write Through
- Write back
- Write around

### Write Through
Les données sont mis à jour en DB & dans le cache. L'i/O est confirmé uniquement quand les données ont été écrits aux 2 endroits

### Write-around
les données sont écrits dans la base de donnée uniquement. L'I/O est confirmé quand les données sont écrits dans la base de donnée.

Ensuite, il faut s'assurer de faire une entry dans le cache. Par exemple, on spécifie que l'entrée est fausse  ou alors on evict la donnée du cache

Le problème c'est que cela coute cher car cela nécessite des changements et refaire des appels en direct et pas en async.

### Write-back
Les données sont écrites dans le cache en premier puis propagé à la base de donnée en async. La confirmation se fait quand les données sont écrites dans le cache puis à nouveau dans la DB.

En gros, 
Quand on a besoin de faire une mise à jour dans la base de donnée, on hit cache et on voit qu'il y a une différence entre les 2 donc il y aura un data inconsitency si on fait une mise à jour dans la base de donnée.
On fait une mise à jour sur l'entry cache puis on push le changement dans la base de donnée

Potentiel probleme : Impossibilité s'il y a plusieurs caches qui existent

