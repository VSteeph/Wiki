# Threading & Asynchronous

>Un ordinateur peut utiliser plusieurs thread, mais ce n'est pas vraiment en parallèles, c'est juste qu'un thread va effectuer ses taches puis un autre, et c'est l'ordinateur qui va gérer la charge de travail en passant d'un thread à l'autre. C'est différent du "Parallel Processing" (à vérifier)

## ThreadPool
.Net utilise une collection de thread pour executer des taches génériques et optimise le nombre de thread (Class : ThreadPool)

Exemple :
```
ThreadPool.QueueUserWorkItem(data => {
  score[] highscores = GetHighScore();
  }, null);
```

On peut aussi l'appeler avec une fonction normal et pas une lambda

## Event-based Async

L'idée est de s'inscrire aux events corrects qui ont une méthod Asynchronous

```
HighScoreManager highScoreManager = new HighScoreManager();
highScoreManager.highScoresLoaded += OnHighScoresLoaded;
highScoreManager.LookUpScoresAsync();
```

## AsyncResult Pattern
Page 254 de C# Player guide

La logique grossière est le drive, où on prend un ticket au premier guichet puis on recupere le résultat.

Exemple en code :
```
HighScoreManager highScoreManager = new HighScoreManager();
Func<Score[]> scoreLookUpDelegate = highScoreManager.LookUpScore();
IAsyncResult asyncresult = scoreLookUpDelegate.BeginInvoke(null,ull);
HighScores = scoreLookUpDelegate.EndInvoke(asyncResult)
```
## Callback
Créer un callback avec une fonction lambda par exemple et la passer en paramètres

## Task-based Asynchronous Pattern (TAP)
2 nouvelles classes ont vu leur apparition : Task & Task<TResult>. Task est la classe qui effectue la tache et Task<TResult> y ajoute une promesse de résultat. (Task pour return void)

```
public Task<Score[]> LookUpScore()
{
  return Task.Run(() => {
    // code
    return new Score[length];
    })
}
```

Suite à cela, on obtient une variable qui a une promesse de résultat d'un type de variable, ce qui donne 2 options
```
Task<Score[]> scoresTask = LookUpScores();
scoresTask.Wait();
highScore = scoreTask.result;
```
Mais elle fait perdre le côté async (elle existe néanmoins)
```
Task<Score[]> scoresTask = LookUpScores();
scoresTask.ContinueWith(task => highScore = task.result);
```
Cela s'executera quand la tache sera terminé

## Async & await
En ajout au Task, ces mots clés permettent d'avoir un code plus clean
```
score[] highscore = await LookUpScore();
```
Cela permet de découper l'exécution d'une fonction en plusieurs parties en attendant une taches

```
public async void GetHighScore()
{
  // Premiere partie
  score[] highscore = await LookUpScore();
  // Derniere partie
}
```

La derniere partie ne s'exectuera que quand le score sera recuperé.

Practice : On peut utiliser async sur tout ce qui a un return void ou un awaitable valid.

## "Ancienne approche"
Pour faire du multi-threading, il faut créer un thread
```
using System.Threading;
Thread thread = new Thread(functionName);
thread.Start();
```
Cela prend un delegate en paramètre, c'est à dire une fonction void avec aucun paramètres
```
thread.Join();
```
Cela permet de freeze le thread en attendant que les autres finissent leur executions (Join les 2 threads).

On peut avoir beaucoup de thread en même temps mais c'est couteux de les créer et il est impossible de savoir quand les context switch (passage d'un thread à l'autre) va se produire, donc il faut vraiment que cela soit indépendant car le résultat ne sera jamais le même.

Pour arrêter un thread, on peut utiliser
```
Thread.Sleep(timeInMilliSeconds)
```
Il est possible d'utiliser le parametrizedThreadStart qui est de type void et prend un seul objet en paramètres (donc tout est possible), du moment que le cast est bon.
```
Thread thread = new Thread(countdown);
thread.Start(50)
```
Cela va prendre 50 en tant qu'objet, il ne faudra pas oublier de le recast en int apres
```
public Countdown(object input) {
int n = (int)input)
....
}
```
