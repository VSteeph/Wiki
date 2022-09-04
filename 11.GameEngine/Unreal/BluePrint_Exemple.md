# Rendre un élément indépendant du FrameRate

On utilise l'event Tick pour chaque Frame et on utilise le delta en seconds entre chaque Frame. On multiplie cette valeur par la vitesse et on plug le resultat là où on veut utiliser la variable (équivalent du Time.Deltatime x speed):


![image](https://user-images.githubusercontent.com/58773222/188307737-74615d63-8db3-4e24-8f15-0dcc821fe714.png)
