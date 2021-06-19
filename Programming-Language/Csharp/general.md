# Types

## Dynamic
Certains langages comme JS, Python permettent de déclarer des nouvelles méthodes, proprietés au run time, ce sont des langages dynamiques. Cela signifie que le systeme s'assure de la présence de la variable au moment du run-time et non de la compilation (dynamic type checking vs static type checking)

C# permet de déclarer des variables en dynamique et permet de déclarer ou modifier des méthodes, properties au run time. Cela permet aussi d'executer du Ruby(IronRuby) et du python (IronPython) sur la platform .NET.

```
dynamic text ="hey";
Console.WriteLine(text.Length);
```

L'intérêt est lorsque les objets sont dynamiques, c'est à dire qu'ils peuvent évoluer pendant le runtime.

La façon de créer un objet dynamique manuellement est d'utiliser un dictionnaire<string,object> ou string est le nom de la variable et object la valeur. Cela peut même être jumelés avec des delegates

Tous les types peuvent être dynamique, il suffit d'implémenter l'interface IDynamicMetaObjectProvider. C'est extremement bas niveau et nécessite du metaprogramming avec de l'analyse du code avec d'autres codes.

Il y a 2 options plus haut niveau à la place qui sont ExpandObject & DynamicObject.

### ExpandoObject
```
dynamic expando = new ExpandoObject();
expando.Name = "george";
expando.Age = 21;
expando.HaveABirthday = new Action(() => expando.age++);

expando.HaveABirthday();
```

Cela fonctionne comme le dictionnaire dont on a parlé en un peu plus clean car cela prend en compte IDynamicMetaObjectProvider. Cela signifie que l'on peut cast un ExpandoObject en IDictionnary<string, object> et avoir acces à des méthodes comme enumerate

```
IDictionnary<string, object> expandoAsDic = (IDictionnary<string,objecy>)expando;
expandoAsDic.Remove("Age");
// on peut aussi faire des foreach pour le parcourir
```

### DynamicObject
Une autre solution est d'hérité de DynamicObject qui est un peu plus puissant. C'est une classe abstraite qui a plein de méthodes virtuals que l'on peut override. Il est impossible de créer un DynamicObject.

DynamicObject permet de customiser le comportement sur certains aspects. Par exemple, comment recuperer les values, les set, appeler les méthodes, etc. Il y a juste besoin d'override ce que l'on veut changer.

```
using System.Dynamic;

public class CustomPropertyObject : DynamicObject
{
  private Dictionnary<string,string> data;

  public CustomPropertyObject(string[] names, string[] values)
  {
    data = new Dictionnary<string, string>();
    //remplir le dictionnary avec le names & values
  }

  public override bool TryGetMember(GetmemberBinder binder, out object result)
  {
    if(data.containsKey(binder.name))
    {
      result = data[binder.name]
      return true;
    }
    else {
      result = null
      return false;
    }
  }

  public override bool TrySetMember(SetMemberBinder binder, object value)
  {
    if(!data.containsKey(binder.name))
    {
      return false;
    }
    data[binder.Name] = value.toString(); //safe type
    return true;
  }
}
```

voici la lsite des méthodes possibles à override (tout sur la doc Microsoft):
- GetDynamicMemberNames
- TryUnaryOperation (overload Operator)
- TryBInaryOperation (overload Operator)
- TryConvert
- TryGetIndex & TrySetIndex
- TryInvokeMember
- TryInvokeMember
- TryCreateInstance (Not in C#)
- TryDeleteMember (Not in C#)
