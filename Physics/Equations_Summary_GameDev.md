# Ensemble d'équations pouvant être utile lors de la création d'un jeu et leur source :

## Forces 

### Jump

**Initial velocity requise :** Sqr(Gravity \* 2 _* Desiredheight) // 2 peut etre négatif lorsque la gravité est négatif

---

### [Gravité](https://en.wikipedia.org/wiki/Equations_for_a_falling_body)

**Gravité :**  9,806 65 m/s^2  // m/s^2  correspond à l’accélération, c’est à dire le nombre de m/s gagné par s 
**Vitesse de chute overTime :**  Force de gravité * temps

---

### Collisions

**Coefficiant de restitution :** Coeff de restitution = Relative velocity after collision / relative velocity before collision [Source](https://en.wikipedia.org/wiki/Coefficient_of_restitution)

** Relative velocité apres une collision** coeff de resitutition * relative velocity avant la collision

**Velocité Object A**: (masseA + (masseB * initialVelocityB) + masseB * CoefRestitution(initialVelocityB - initialVelocityA)) / masseA + masseB

**Velocité Object B**: (masseA + (masseB * initialVelocityB) + masseA * CoefRestitution(initialVelocityA - initialVelocityB)) / masseA + masseB
