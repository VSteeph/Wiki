## Basic command
```
git config (pour set  up la config)
git init (initalize un repo en tant que git)
git status (état des fichiers, ce qui a changé, ajouté, supprimé, etc)
git add (stage un ou des fichiers)
git commit -m "message" (créer un commit, description du commit présent)
git push origin
git log (affiche les informations des commits)
git branch name (create a branch)
```

## Basic commandes options
```
git init folderName (init un nouveau dossier)
git add --all (Permet d'ajouter tous les fichiers nouveaux/modifiés)
git add *.txt (pour ajouter tous les fichiers txt danns le dossier)
git add docs/ (pour ajouter tous les fichiers dans le dossiers docs)
git add docs/*.txt (mélange des 2)
git add "*.txt" (Ajoute tous les fichiers text dans le projet Entier)
git checkout HEAD -- filename (Reset le fichier au dernier commit)
git checkout -- . (reset tous les fichiers)
git commit -a -m "message (-a signifie staged all)
git commit --amend (ajoute les fichiers staged avec le dernier commit)
```

-- permet de préciser une liste de fichier apres une commande

^ signifie le parent, ^^ signifie 2 parents en avant mais cela peut aussi être traduit par `~`X où X est le nombre de parent.
git rev-parse "HEAD^^^" est equivalent à git rev-parse HEAD`~`3


## Git Merge
Fusionne 2 branches ensemble, il faut se mettre sur la branche que l'on veut avoir à la fin et
`git merge secondBranch`
Cela crée donc un commit unique qui aura 2 parents


## Git Rebase
Git rebase permet de rebaser une branche sur une autre. Par exemple, sur la branche B, faire git rebase master va rebaser la branche B sur le master. C'est à dire que la branche B sera update jusqu'à master et tous les commits vont être ajoutés par dessus la dernière version de master
```
Git checkout branchName
git rebase branchNameToBasedOn
```

Git rebase peut aussi permettre de modifier des commits sur la même branche avec  (i pour interactive) PAS LE FAIRE UNE FOIS QUE C EST PUSH
```
git rebase -i HEAD~3 (pour remonter 3 commits en avant)
git rebase Head^ (^signifie parent)
```
Cela va ouvrir un editeur avec les commandes qui vont être effectuer lorsque cela sera valider. Il y aura plusieurs commandes à disposition :
```
git pick (pour choisir un commit, cela permet de changer l'ordre par exemple)
git reword (utiliser un commit mais changer le commit message)
git edit (utiliser commit mais stop for ammending?)
git squash (use commit mais fusionne avec commit précedent)
git fixup (comme squash mais n'affiche pas dans logs)
git exec (run command shell)
```
De la même manière, cela va déplacer les 3commits dans une zone temporaire et effectuer les commandes choisies dans l'editeur comme un rebase normal.


## Git Reset
Cela permet de reset un commit. Par exemple
```
git reset HEAD^(permet de revenir au commit précédent, ^ est le parent)
git reset HEAD^ --hard (permet de delete le commit précédent)
```

Pour reset et supprimer le dernier commit, on fait
git reset -hard fc60 (cela va retourner au commit fc60..., 4lettres suffisent)
Cela va changer ou va pointer le Head mais aussi le working tree.
```
git reset --soft (permet de garder les changements non commit)
```
Le reset s'effectue sur la branche où on est !!

## Git Revert
Fonctionne de manière similaire à git reset mais créer un nouveau commit de ce qui a été enlevé
```
git revert HEAD~3 (revert les 3 derniers commits, Head + 3 parents)
```

## Git Stash
Cela perrmet de mettre les changements en cours dans un stash (one time), faire la merg, puis avec git pop de remettre les changements ou push un changement spécifique sans perdre son changement

## Git Submodules
https://www.git-scm.com/docs/git-submodule

## Advanced command
### Reflog
git reflog (montre tous les steps, pas que les commits)
Cela peut s'utiliser en complément de reset avec les HEAD@{x} pour remettre à l'étapes que l'on souhaite
```
git reset --hard HEAD@{3} pour revenir à l'étape 3
```

### update-ref
Si le git s'est perdu au niveau du head, on peut replacer la head avec "update-ref"
```
git update-ref refs/heads/master hash (master pour le nom de la branche)
```

### rev-parse
Recupérer le curent parse d'une branche
```
git rev-parse branchName
```

### cherry-pick
Permet de récupérer un commit spécifique et l'ajouter à une branche
```
git cherry-pick master (Prend le dernier commit de master et l'ajoute)
```
On peut aussi sélectionner un ou plusieurs commits
```
git cherry-pick commit1 commit2 (en se mettant sur la branche ou l'on veut les ajouter)
```
