# Dependency Inversion

C'est le but que les modules à haut niveau ne doivent pas dépendre de module bas niveau. Les 2 doivent dépendre d'abstraction et l'abstraction ne doit pas se concentrer sur les détails.

Un High-level module signifie qu'il appelle quelque chose d'autres. Exemple, la classe commande qui appelle la classe EmailManager pour envoyer un Email. C'est à dire que des qu'il y a une dependence avec une autre classe, c'est un high-level module et s'il y en a pas, c'est un low-level module.

Cela signifie qu'un high-level module depend d'un low level et donc on peut pas changer le low level sans casser le high level.

Le but de DI est de changer ça et d'inverser la tendance pour dépendre d'abstraction. Cela est possible grâce aux interfaces qui respecte le fait de faire dépendre d'abstraction et de ne pas faire dépendre l'abstraction sur les détails.

## Mettre en place une DI

* Il faut que la classe low-level integre une interface avec son implémentation
* C'est l'interface qui est utilisée et referencée plutôt que la classe low level

## Dependency Inversion set up

Quand les étapes ci-dessus sont faites, il existe toujours une indepencen qui est le fait d'instancier la classe, exemple :

ICustomerService = new CustomerService() mais il faudra instancier un objet à un moment ou un autre.

Dependency Inversion regroupe ces informations pour facilement changer et cela impactera l'ensemble du code. On peut utiliser une factory pour ça.

Exemple :

```c#
public class Factory
{
  public static IPerson CreatePerson()
  {
    return new Person();
  }
  
  public static IMessagerSender CreateMessageSender()
  {
    return new Emailer(CreateLogger());
  }
  
  public static Ilogger CreateLogger()
  {
    return new logger();
  }
}

public class main
{
  IPerson person = Factory.CreatePerson();
  person.FirstName = "john";
}
```

## Benefices

C'est facile de changer le code et remplaçant des éléments sans avoir peur de casser ou d'avoir des dependances cassées qui alourdissent le processus de changement.

# Depency Injection
