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
