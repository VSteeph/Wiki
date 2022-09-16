# Rendre un élément indépendant du FrameRate

On utilise l'event Tick pour chaque Frame et on utilise le delta en seconds entre chaque Frame. On multiplie cette valeur par la vitesse et on plug le resultat là où on veut utiliser la variable (équivalent du Time.Deltatime x speed):


![image](https://user-images.githubusercontent.com/58773222/188307737-74615d63-8db3-4e24-8f15-0dcc821fe714.png)


# Créer un Event
Il faut créer le node Custom Event et changer son nom :
![image](https://user-images.githubusercontent.com/58773222/188307776-596785df-5111-456e-b283-84d850fc6cdf.png)

# Utiliser un Event
Il faut une référence à l'objet qui a cet event et chercher le node qui a le nom de l'event : 

![image](https://user-images.githubusercontent.com/58773222/188307805-cd42a939-a645-45ae-8463-8370472bec06.png)


# Cibler un type d'éléments dans les collisions ou en général
On peut cibler un type d'élément ou de blueprint spécifique au lieu de faire des traitements générique avec le node Cast To NomDeVotreElement. Par exemple, si je veux que ma collision ne touche que mon player qui a comme nom de blueprint BP_ThirdPersonCharacter, je vais chercher le node Cast_To_BP_ThirdPersonCharacter avec le "Other Actor" :

![image](https://user-images.githubusercontent.com/58773222/188307858-cd7680f1-3edb-413d-9583-a0fbcd54e36e.png)
