# Exercices réalisés dans le cours de Freya (Source à la fin du fichier Vector)

## Part 1

### Radial Trigger

**Consigne:**

Créer un Trigger qui permet de savoir si un point est à l'intérieur ou à l'extérieur du cercle 

**Solutions:**

Il suffit de comparer la distance entre le point et le centre du cercle avec le rayon du cercle, donc si 

Point - CentrePosition < Radius alors le point est à l'intérieur du cercle sinon il est en dehors

**Bonus:**

Pour optimiser ce systeme dans le cas où il y a beaucoup de vérifications :
* On peut utiliser SqrMagnitude et le comparer au radius² pour éviter de faire des racines carrés (opérations couteuses)
* On peut utiliser x \* x et y \*y au lieu de Mathf.Pow qui est un petit moins couteux
* On peut utiliser un système de message pour ne vérifier que quand l'élément a changé de position et pas à chaque frame

### 
