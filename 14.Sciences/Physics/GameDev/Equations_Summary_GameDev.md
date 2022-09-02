# Ensemble d'équations pouvant être utile lors de la création d'un jeu et leur source :

## Forces 

### [Jump](https://www.real-world-physics-problems.com/physics-of-jumping.html)

**Initial velocity requise :** Sqr(Gravity \* 2 _* Desiredheight) // 2 peut etre négatif lorsque la gravité est négatif


### [Projectile Motion](https://www.real-world-physics-problems.com/projectile-motion.html) (Peut servir pour un saut horizontal) 

**Horizontal Velocity**: Initialvelocity * Cos(Angle)

**Horizontal Velocity**: InitialVelocity * Sin(Angle)

[More](https://gamedev.stackexchange.com/questions/134323/how-to-calculate-vector-of-projectile-initial-velocity) VO = initial velocity // Po = Inital Position // pt = target Position

**Time To reach**: t = -Vo.y - Sqr(V

**initial velocity x** (Ptx - pox) / t

**Initial velocity z

---

### [Gravité](https://en.wikipedia.org/wiki/Equations_for_a_falling_body)

**Gravité :**  9,806 65 m/s^2  // m/s^2  correspond à l’accélération, c’est à dire le nombre de m/s gagné par s 

**Vitesse de chute overTime :**  Force de gravité * temps donc chute += force de gravité * deltaTime

---

### Collisions

**Coefficiant de restitution :** Coeff de restitution = Relative velocity after collision / relative velocity before collision [Source](https://en.wikipedia.org/wiki/Coefficient_of_restitution)

**Relative velocité apres une collision** coeff de resitutition * relative velocity avant la collision

**Velocité Object A**: (masseA + (masseB * initialVelocityB) + masseB * CoefRestitution(initialVelocityB - initialVelocityA)) / masseA + masseB

**Velocité Object B**: (masseA + (masseB * initialVelocityB) + masseA * CoefRestitution(initialVelocityA - initialVelocityB)) / masseA + masseB
