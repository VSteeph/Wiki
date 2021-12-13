# Azure Service Bus 

## Nuget Package

Microsoft.Azure.ServiceBus

## Qu'est ce qu'un service Bus?

Si on a un site qui crée un compte et qu'on a un systeme d'envoie de mail. Si on doit changer l'email Services, on doit relancer tout le site. Si on a un microservices qui s'occupe des emails, on peut juste le relancer.

Le principe d'un Sender est qu'il va faire une queue des taches à faire et même si le receveur est down, il va récupérer la liste des éléments à faire et catch up.
