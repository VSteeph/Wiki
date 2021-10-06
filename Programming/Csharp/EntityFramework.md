# Entity Framework

## Librairies

Actuelleemnt, les librairies .NET Standard sont les mieux si possible car elles marchent pour les projets en .NET Core ou .NET Framework

## DbContext

Pour accèder aux données, on utilise un DbContext. On peut lui donner un constructor avec les options de bases ou généré ses propres options (DbContextOptions). Le DbContext contient le type de données avec des DbSet (qui correspond à des tables)
