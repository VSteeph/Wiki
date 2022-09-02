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

Cela permet aussi de pas avoir un gros block mais plein de petits éléments qui ont fait un seul élément, sans aucune dépendence, qui font qu'une chose et self contained. On peut donc ajouter/enlever des éléments sans aucun soucis et rendre l'application modulable sans aucun risque.

Cela permet aussi d'utiliser la dépendency injection.

## Depency Injection

La dependency Injection évite le fait d'appeler une Factory et faire un factory. Cela permet d'injecter les dépendances qu'on souhaite utiliser aux bons endroits dans les classes.

DI vient aussi avec IOC (inversion of control) qui est comment appliquer le principe de Dependency Inversion, mais cela permet aussi de changer dynamiquement des dépendances en fonction de ce qu'on donne ou des circonstances.

Pour finir, cela facilite l'unit Testing pour pouvoir tester chaque composant indépendemment.

### Implementation

Pour implémenter une DI, il faut que toutes les classes implementent une interface, ainsi qu'un constructeur qui leur injecte les dépendences dans un champ private exemple 

```C#

public class BusinessLogic : IBusinessLogic
{
  Ilogger _logger;
  IDataAccess _dataAccess;
  
  public BusinessLogic(ILogger logger, IDataAcces dataAccess)
  {
    _logger = logger;
    _dataAccess = dataAccess;
  }
  
  public void ProcessData()
  {
    _logger.log("log");
    _dataAccess.LoadData();
  }
}
```

A partir de la, on pourrait ajouter une factory pour faire les appels Constructor mais on va voir une autre façon avec `AutoFac` (NuggetPackage) qui est un IOC container.

```C#
public static IContainer Configure() 
{
  var builder = new ContainerBuilder();
  builder.RegisterType<BusinessLogic>().As<IBusinessLogic>();
  return builder.Build()
}
```

En gros, ça veut dire que si le programme a besoin d'un IbusinessLogic, AutoFac va retourner un BusinessLogic, mais c'est un peu long si on a beaucoup de classe. Il y a donc des chemins plus rapide, exemple : 

```C#
public static IContainer Configure() 
{
  var builder = new ContainerBuilder();
  builder.RegisterAssemblyTypes(Assembly.Load(nameof(DemoLibrary)))
  .where( t=> t.Namespace.Contains("Utilities"))
  .As (t => t.GetInterfaces().FirstOrDefault(i => i.Name == "I" + t.Name));
  return builder.Build()
}
```
