Source: https://www.youtube.com/watch?v=UrQWii_kfIE

# Redis Implementaiton

## Préparation

Pour commencer le projet, on peut créer une blazor app (Blazor Server App) mais cela peut marcher avec n'importe quel web application (ASP) ou même desktop application.

Le principe d'un cache n'est pas forcement d'aller plus vite qu'une base de donnée mais c'est de ne pas ralentir un élément si la base de donnée ralentit suite à plusieurs requetes ou autres. Cela permet d'avoir de la constance dans les résultats et gagner du temps sur les éléments qui sont souvent sollicités.

Le cache n'est pas une nouvelle base de donnée. La base de donnée fait les queries, recupere les données à plusieurs endroits alors que dans le cache, ces éléments sont déjà faits et ont stockent juste les informations (souvent dans un key/value).
