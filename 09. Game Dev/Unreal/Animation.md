# Animation

## Character Animation

On utilise des Skeletal Mesh pour gérer. On peut avoir un Skeletal Master et avori des Skeletal Mesh qui en dérivent. Si on va dans le Content Drawer, clic droit, on peut voir un sous menu Animation avec plein d'éléments

## Animation BluePrint

On crée l'animation Blueprint par rapport à un Skeleton Mesh. Dans ce blueprint, on a acces à l'Asset Browser qui liste toutes les animations du skeleton mesh
![image](https://user-images.githubusercontent.com/58773222/191116366-69b311a6-bca8-49ad-9e3c-ac5b641b55fd.png)

On peut ensuite Drag les animations et les mettre en place. Pour fusionner les animations, on utilise l'animGraph colmme un blueprint graph avec des nodes comme Blend. On peut toujours convertir un élément en varaible en cliquant directement sur l'élément et faire "promote to variable" comme l'Alpha dans le blend :
![image](https://user-images.githubusercontent.com/58773222/191118424-90c8862a-1192-45e0-871d-5a8715f5aa4f.png)

Exemple simpliste de state avec des variables:
![image](https://user-images.githubusercontent.com/58773222/191118848-99f2ce52-19bd-4eb6-8ac1-d01fd06b2e90.png)

Enfin, il est important de relier l'APB (Animation BluePrint) au Blueprint du personnage (Component Mesh) 

![image](https://user-images.githubusercontent.com/58773222/191119752-6923f7c0-3890-4548-89e2-d3c8d911863d.png)

## Animation Blending Space

Pour mieux gérer le blending entre les animations, on peut créer un Blend Space (Content Drawer => Clic Droit => Animation => Blend Space) (Nomenclature BS_x), il faut le relier au bon mesh.

Cela permet de mélangfer une ou plusieurs animations basé sur des valeurs de plusieurs inputs. On a acces à plusieurs vazlues (Horizontal & Vertical Axis)

## Convertir une Animation

Il est possible de retarget des animations en selectionnant une animation et en utilisant l'option retarget Animation Assets ou Asset Actions > Export puis reimporter les animations quii ont été exporté en doublon en les reliant à un nouveau Skeleton (à partir du moment où ils sont dans un format compatible)
