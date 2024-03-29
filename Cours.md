# Bonnes Méthodes du Web & Versioning

## Liens

- *Url Site Markdown : https://www.markdownguide.org/cheat-sheet/*




## Définitions

- *Versioning : La gestion de versions consiste à garder une trace des modifications apportées au code (style base de données). Enregistrements des changements ainsi que des personnes qui les ont faîtes.* 



## Cours

Versioning : 

Traçabilité, collaboration, backup & rétablissement, branching & merging

Nomenclature de Versioning :

Majeure, Mineure, Correctif (Alpha, beta, snapshot)

SVM (SCM?) = Type de Logiciel semblable à GIT


Aperçu des Systèmes de Versioning :

### Subversion (SVN) : Système de contrôle de Versions centralisées

Un serveur centralise toutes les versions (Si le serveur tombe, tout est perdu)

Opérations & Fonctionnalités : 

Checkout/Update/Commit : Récupérer le code / Mettre à jour copie de travail / Envoyer modification (Localement)

Branching & Merging : Branches de projets & Fusions avec les mises à jour envoyées

Dépôts & Repositories = Code source

### Git : Système de contrôle de Versions distribuées

Github / GitLab

### Git en détails :

La principale différence entre Git & d'autres SCMs, réside dans la façon dont Git considère les données. 

Conceptuellement, la plpart des autres SCMs stockent les informations sous la frome d'une liste de modification apportées à chaque fichier au fil du temps.

Alors que Git considère les données comme un ensenble dans un ensemble de snapshot 

#### Avec Git la quasi-totalité des opérations sont locales

#### Git se de gérer l'intégrité des données

Avant la plupart des opérations effectuées, Git effectue une "somme de contrôle" puis obtiens une signature unique qui sert de réf. On peut ainsi vérifier l'intégrité des données. Cela signifie qu'il est impossible de modifier le contenu d'un fichier sans que Git ne le sache.

Le mécanisme utilisé par Git est appelé une empreinte SHA-1. Une chaine de caractères composées de 40 caractères hexadécimaux qui ressemble à cela :

```sh
24d9da66557578921dadfe42b5
```

#### Avec Git très peu d'opérations sont destructives

#### Git à trois états principaux dans lesquels peuvent se trouver vos fichiers :

- **Modifier** : Modifier fichiers dans répertoire (Working Directory)
- **Indexer** : Ajouter les fichiers où les changements auront lieux
- **Valider** : Validations des fichiers

.git -> Zone de travail ->

#### La première utilisation de Git

Git possède un outil appele Git config qui permet de configurer les paramètres de Git sur votre système. Ces params peuvent être stockés dans trois endroits différents :

- [chemin]/etc/gitconfig : Contient les valeurs appliquées a tous les utilisateurs & tous les projets.

- Fichier ~/.gitconfig : Spécifique à l'utilisateur.

- Fichier config dans le repertoire Git d'un dépot en cours d'utilisation (.git/config)

Sur les OS Windows, Git recherche le fichier .gitconfig ( ~ = Tilde)


#### Montrer où est localisé la config git
```sh
git config --list --show-origin
```

#### Configurer votre identité

La première chose que vous devriez faire lorsque vous installez Git est de définir votre nom d'utilisateur & votre adresse e-mail. Ceci est important car chaque validation dans Git utilise cette information et elle est immuablement attachée aux commits que vous validez :

```sh
$ git config --global user.name "John Doe"
$ git config --global user.email "mon@email.com"
```

#### Votre éditeur de texte

VI / VIM : (I = mode insertion, ECHAP = Quitter mode insertion, ":" = mode commande (si pas en mode insertion/edition) "wq" pour sauvegarder & quitter.)
Nano

```sh
git config --global core.editor emacs
```

Sur Windows vous êtes obligés de spécifier le chemin complet de l'éditeur de texte.

```sh
git config --global core.editor "'C:/Program Files/Notepas++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
```

#### Le nom de branche par défaut

```sh
git config --global init.defaultBranch main
```

#### Vérifier vos paramètres

```sh
git config --list

git config user.name
```

#### Obtenir de l'Aide

```sh
git help <commande>
man git <commande>

```

## Les Bases de Git

### Démarrer un projet

#### Initialiser un dépot

```sh
git init
```

#### Supprimer un dépot

```sh
rm -rf .git/
```

#### Vérifier l'état du dépots

```sh
git status
```

#### Ajouter tout ce qui se trouve dans le répertoire actuelle dabs le prochain commit

```sh
$git add .
```

#### Supprimer un fichier du prochain commit

```sh
$git rm -cached [fichier]
```

#### Faire un commit

```sh
$git commit
```

#### Cloner un dépot

```sh
git clone https://github.com/R1t0ru/Git_test.git
```

De manière générale on peur résumer le cycle de vie des fichiers dans Git comme suit : 

![alt text](Screenshot/shemas.png)

## Git hub

Profile -> Settings -> Developer Settings -> Personal access tokens, Tokens (classic)

#### Lier un dépot distant avec un dépot local

```sh
git remote add origin <url>
```

Il faudra choisir quel type d'accès utiliser :

- https : pour un accès en lecture seule (read-only)
- ssh : pour un accès en lecture/ecriture (read/write) (clé dans ~/.ssh/id_ed25519) (Clé ssh publique = Identification de la machine)
- Personal Access Token (PAT): pour un accès en lecture/ecriture

Pour lister les remotes :

```sh
git remote -v
```

Pour supprimer un remote :

```sh
git remote rm <remote-name>
```


HEAD = Branche principale

Premier push (permet d'informer git que la branche main doit être synchronisée vers le dépot git (si non existante, création de la branche)) :

```sh
git push -u origin main|master 
```

Pour les push suivants :

```sh
git push 
```

Pour cloner un depot :

```sh
git clone https://github.com/bendahmanem/ISITECH-2324-B2-DEV-Versioning
```

#### Ignorer des fichiers

Pour ignorer des fichiers il suffit de créer un fichier .gitignore et d'y ajouter les fichiers et les dossiers a ignorer.

Le fichier .gitignore agit de façon récursive sur les sous-dossiers.

#### Consulter l'état des fichiers

```sh
git status
```

```sh
git diff
```

Git status présente l'état global du dépot, modifié ou non. Git diff présente les modifications apportées aux fichiers.

On peut utiliser git diff de façon plus précise :

```sh
git diff --staged
```

#### Valider des modifications

```sh
git commit -m "message"
```

#### Effacer des fichiers

Pour éliminer un fichier il faut utiliser les commandes suivantes :

```sh
rm <fichier>

git status

git rm <fichier>
```

Cette dernière commande indexe le fichier pour qu'il soit supprimé dans le prochain commit.

Il existe une autre forme de suppression de fichier :

```sh
git rm --cached <fichier>
```

Cette commande va supprimer le fichier de l'index mais pas du disque dur.

#### Visualiser l'historique des commits

```sh
git log
```

Options de commande log :

```sh
git log --stat
```

```sh
git log --pretty=oneline
```

Cette commande affiche chaque commit sur une seule ligne.

```sh
git log --pretty=format:"%h %s" --graph
```

Cette commande affiche affiche l'historique sous forme d'un graphe.


####

```sh
git commit --amend
```


```sh
git reset HEAD <fichier>
```

Cette commande permet de retirer un fichier de l'index.

#### Désindéxer des éléments déjà commits

```sh
git checkout <branche>
```

#### Création de tags (étiquettes)

En plus d'identifier les commits par des identifiants uniques, Git vous permet aussi d'étiqueter un certain état de l'historique (commit) comme étant important. Cela peut être utile pour marque des versions de votre code source.

```sh
git tag -a v1.0 -m "Version 1.0"
```

On peut lister les tags avec la commande suivante :

```sh
git tag -l "v1.8.5*"
```

Visualiser une étiquette :

```sh
git show v1.4
```

![alt text](Screenshot/image-4.png)


#### Les branches

Lorsque vous faîtes un commit, Git enregistre un objet de commit qui contient un pointeur vers l'arbre de contenu qui représente l'état de votre projet à ce moment-là.Ce pointeur de commit contient le nom SHA-1 du commit parent ou des commits parents qui ont précédé ce commit (plusieurs parents si fusion). Git peut remonter l'histoire du projet avec les commits.

Pour créer une nouvelle branche :

```sh
git branch <nom-branche>
```

Git branch crée une nouvelle branche par défaut mais ne fait pas aller sur celle-ci.

Pour basculer sur une branche :

```sh
git checkout <nom-branche>
```

Pour créer une branche et basuler dessus :

```sh
git checkout -b <nom-branche>
```

##### Fusionner des brances

On va commencer à travailler sur l'issue 53 et effectuer un premier commit :

```sh
git commit -m "commit 3"
```
On va ensuite rebasculer sur la branche master afin d'effectuer un hotfix :

```sh
git checkout master
```

/!\ Ne jamais travailler sur la branche de prod directement /!\

```sh
git branch hotfix
git commit -m "commit 4"
```

Nous sommes satisfait du hotfix et nous alllons le valider

```sh
git checkout master
git merge hotfix
```

La branche hotfix n'a plus lieu d'être et nous allons la supprimer :

```sh
git branch -d hotfix
```

On va maintenant retourner sur iss53 et continuer à travailler dessus :

```sh
git checkout iss53
```

On effectue un nouveau commit afin de valider notre travail :

```sh
git commit -m "commit 5"
```


On va maintenant retourner sur master & effectuer un merge avec iss53

```sh
git checkout master
git merge iss53
```

La stratégie de merge est alors différente de celle utilisée précedemment : Merge commit

Au lieu d'avancer la branche master, Git crée un nouveau col

On peut supprimer la branche iss53 :

git branch -d iss53

#### Résoudre des conflits

Un conflit à lieu lorsque deux branche différentes ont modifiées la même partie du même fichier ou si un a été supprimé dans une branche alors qu'il a été modifié dans une autre.

Physiquement, un conflit est représenté par des caractères spéciaux qui apparaissent dans le fichier.

Après résolution du conflit il suffit de commit.

Vous avez un outil qui permet de résoudre les conflits avec git :

```sh
git mergetool
```

Pour afficher toutes les branches :

```sh
git branch -a
git branch --all
```

Commande `git fetch <distant>` : Elle permet de synchroniser vos travaux, elle va rechercher le serveur qui héberge `<distant>` et va récupérer les modifications qui ont été effectuées sur le serveur distant.

#### Pousser des modifications

```sh
git push <distant> <branche>

git push origin master

git push -u origin master
```

Pour récupérer les modifications effectuées sur le serveur distant a propos de nouvelles branches ou de branches existantes :

```sh
git fetch <distant>
```

Pour récupérer des modifications & les fusionner avec vos branches locales :

```sh
git pull <distant> <branche>
```

La règle d'or lorsqu'on débute avec Git :

`commit` -> `pull` -> `push`

Lorsque vous récupérez des branches distantes avec `fetch`, vous ne créez pas automatiquement une branche locale qui suit la branche distante. Vous devez créer une branche locale & la lier à la branche distante.

```sh
git checkout -b <nom-de-branche> <distant>/<nom-de-branche>

Branch <nom-de-branche> set up to track remote branch <nom-de-branche> from <distant>.
```

On a un raccourci pour cette commande :

```sh
git checkout --track <distant>/<nom-de-branche>
```

Si branche locale n'existe pas encore :

```sh
git checkout <nom-de-branche>
```

Afin de visualiser tout ça on peut utiliser la commande suivante :

```sh
git branch -vv
```

Afin de visualiser tout ça on peut utiliser la commande suivante :

```sh
git fetch --all

git branch -vv
```

Analysons cette commande suivante :

```sh
git push origin -delete <nom-de-branche>
```

#### Rebase le travail

Avec Git il y a deux manières d'intégrer les modifications d'une branche dans une autre :

- La fusion (merge)
- Le rebasage (rebase)

Après un merge on obtient cela :

```sh
git checkout master

git merge experiment
```

Avec le rebase on aurait entré les commandes suivantes :

```sh
git checkout experiment

git rebase master
```

Voici ce qu'il se passe :

Image-20

Puis le résultat final :

Image-22

Rebase est comme un merge mais supprime une partie de l'historique git, historique divergeant en historique synchronisé.

Rebase linéarise les commites.


La commande qui correspond au rebase cité en cours :

```sh
git rebase --onto master server client
```

Essaye d'extraire la branche client de la branche server et de la rebaser sur la branche master.

img 24

```sh
git checkout master
git merge client
```

img 25

On peut aussi rebaser la branche server sur la branche master :

```sh
git rebase master server
```

img 26

Vous pouvez ensuite merge server dans master :

```sh
git checkout master
git merge server
```

#### Rebase or not Rebase

La seule règle à respecter avec la commabde Rebase: ne jamais rebase des modifications qui ont été publiées sur un serveur distant (push)

Conventionalcommits.org
Commitizen dans le projet
GitHub Pages

Faire attention aux dons d'accès aux personnes avec qui on travaille 