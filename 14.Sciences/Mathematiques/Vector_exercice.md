# Exercices réalisés dans le cours de Freya (Source à la fin du fichier Vector)

## Part 1

### Radial Trigger

**Consigne:**

Créer un Trigger qui permet de savoir si un point est à l'intérieur ou à l'extérieur du cercle 

**Solutions:**

Il suffit de comparer la distance entre le point et le centre du cercle avec le rayon du cercle, donc si 

Point - CentrePosition < Radius alors le point est à l'intérieur du cercle sinon il est en dehors
```C#
    private void OnDrawGizmos()
    {
        if(target != null)
        {
            Vector3 TargetToTrigger = transform.position - target.position;
            distanceFromTargetToTrigger = Vector3.SqrMagnitude(TargetToTrigger);
        }

        if (distanceFromTargetToTrigger > (radius * radius))
            Gizmos.color = Color.red;
        else
            Gizmos.color = Color.green;

        Gizmos.DrawWireSphere(transform.position, radius);
    }
```
**Bonus:**

Pour optimiser ce systeme dans le cas où il y a beaucoup de vérifications :
* On peut utiliser SqrMagnitude et le comparer au radius² pour éviter de faire des racines carrés (opérations couteuses)
* On peut utiliser x \* x et y \*y au lieu de Mathf.Pow qui est un petit moins couteux
* On peut utiliser un système de message pour ne vérifier que quand l'élément a changé de position et pas à chaque frame

### LookAt Trigger

**Consignes:**

Créer un trigger qui détecte si un élément le regarde avec une précision manipulable

**Solutions**

Pour cela, il faut utiliser le Dot Product et comparer le résultat avec la précision demandée. Si la précision est plus importante, alors le trigger ne s'active pas, sinon il s'active :

```C#
        if (target != null)
        {
            //TargetToTriggerDir rename
            Vector3 TargetToTriggerDir = transform.position - target.position;
            // Rename Lookness
            float dotFromTargetAndTrigger = Vector3.Dot(target.forward, TargetToTriggerDir.normalized);
            if (dotFromTargetAndTrigger >= threshold)
                isBeingLookedAt = true;
            else
                isBeingLookedAt = false;
        }
```

### Spaces transformations

**Consignes:**

Il faut créer les fonctions qui permettent de convertir un point en localSpace d'un autre point puis à nouveau en World Space. C'est à dire refaire les fonctions Unity :
transform.InverseTransformPoint (Local Space)
transform.TransformPoint (World Space)

Partie 2 :

Convertir un point en local Space ou en World Space. C'est à dire qu'on conserve les valeurs du Vecteur et on le trace dans un autre réferentiel
Vecteur(2,1) n'est pas tracé au même endroit quand il est en local Space ou en world Space

**Solutions:**

Pour InverseTransformPoint, c'est à dire passer obtenir le Local Space à partir du World Space, il suffit de :
* Ajouter le Vecteur de référence au vecteur actuel
* Tourner le Vecteur de la rotation du vecteur actuel

Et il suffit de faire la logique opposé dans l'autre cas. Dans le cas de scale, ne pas oublier de multiplier/diviser par la scale.

Partie 2 :

Tracer en local :

On calcule dans un premier temps l'offset du vecteur qui est en multipliant chaque élément par l'axe correspondant, c'est à dire :
* x => x * transform.right
* y => y * transform.up
* z => z * transform.Forward

Ensuite, on ajoute le vecteur de référence à l'offset.

Tracer en World:

On effectue le même processus en enlevant le vecteur de référence dans lequel il se trouve

## Part 2


