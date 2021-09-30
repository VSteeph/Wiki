# AppSettings

Cela marche sur tous les .NET Core applications quasiment et peut être l'équivalent du .config

## Avantages

Cela permet d'avoir différents config entre le développement et la production ou d'avoir des différences entres certaines environnement de productions (Serveur FR vs Serveur US). Cela permet de ne pas changer et recompiler l'application à chaque changement.

C'est aussi plus sécurisé car cela permet d'extraire les informations sensibles du source code et on peut même encoder les appsettings et les décoder au moment de leur utilisation.
