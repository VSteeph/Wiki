# Entity Framework

## Librairies

Actuelleemnt, les librairies .NET Standard sont les mieux si possible car elles marchent pour les projets en .NET Core ou .NET Framework

## DbContext

Pour accèder aux données, on utilise un DbContext. On peut lui donner un constructor avec les options de bases ou généré ses propres options (DbContextOptions). Le DbContext contient le type de données avec des DbSet (qui correspond à des tables)

C'est importatn de le emttre dans un projet externe car c'est chiant de relier ça à l'UI. 

## Migration

L'avantage de Migration.tool permet de build la base de donnée à partir de Migration Script (Git de db, chaque script de migration correspond à un commit en gros)

Migration Up permet de monter en version et dwon de descendre. Evidemment, un rollback fait perdre des données si on drop des tables.

Il y a aussi un snapshot disponible

## SQL optimisation

nvarchar(max) bad is pas nécessaire

## Attributes

Pour avoir une bonne base de donnée, il est important de catégoriser les champs dans les models avec les attributes (tags), ils se trouvent dans
using System.ComponentModel.DataAnnotations;

voici des exemples:
[Required]
[MaxLenght(x)]
[Column(TypeName ="varchar(16")] qui est dans System.ComponentModel.DataAnnotations.Schema (Pasi deal d'ajouter du SQL dans un model mais c'est mieux d'opti)

et aussi l'ignorer avec :
[NotMapped) dans System.ComponentModel.DataAnnotations.Schema

ça parait minime mais ça scale avec plein d'utiilisateurs, donc c'est bien de le faire et ça coute pas grand chose de le faire directement.

## Danger

EFC utilise des procédures avec des hauts niveaux de privileges, donc cela veut dire que si on ship un produit (principalement un logiciel par exemple), il faut les credentials (log & user) et ces credentials doivent avoir un haut de niveau privilege et même si c'est encrypté, l'utilisateur a une partie de l'information de l'encryption + les credentials donc, c'est vraiment pas fou si c'est quelque chose de distribué, sur un serveur c'est pas un probleme.

Cela veut dire qu'un utilisateur peut utiliser sp_executesql et donc executer n'importe quel SQL (Drop, select, alter, etc)
