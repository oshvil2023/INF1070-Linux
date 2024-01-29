# Laboratoire 4 : Commandes, fichiers et dossiers

## Exercice 1 : Fichiers (60 mins)

### 1.1 : Création

- Créez un fichier `bonjour` qui contient « `Bonjour le monde` ».

```sh
# Il y a pleusieurs options pour creer le fichier.
# touch, echo, vim, etc.
echo "Bonjour le monde" > bonjour
```

- Afficher le contenu du répertoire avec `ls -l`.

- Quelle est la taille du fichier `bonjour`?

```sh
# 4eme colonne de la commande `ls -l`
```

- Afficher le contenu des fichiers `bonjour` avec la commande `cat`.

```sh
cat bonjour
```

- Afficher aussi le numéro d'[inode](https://linoxide.com/linux-command/linux-inode/) du fichier `bonjour` en utilisant la commande  `ls -li` (l'inode 
  est le nombre affiché au début de la ligne).

```sh
# noeud d'index = inode. chaque fichier a un inode unique.
# Les inodes contiennent notamment les metadonnees des
# fichiers (droits d'acces, emplacement, etc.)
ls -li
```

- Éditez le fichier `bonjour` pour avoir « `Salut le monde` ».

```sh
# utiliser un editer un editeur de texte (vim, nano, gedit, etc.)
nano bonjour
```

- Qu'affiche maintenant `ls -l` ? Est-ce que la taille du fichier `bonjour` à changé ? Est-ce 
  que la date a changé?

```sh
# La taille est passee de 17 a 15. Oui, l'heure a change.
ls -l
```

- Et si on affiche aussi l'inode avec la commande `ls -li`, est-ce que le numéro a changé?

```sh
# Non, ca change pas.
ls -li
```

### 1.2 : Renommage, type et extention

- Renommez (suggestion: utilisez la commande `mv`) le fichier `bonjour` en `ave`. 
```sh
# mv permet normalement de deplacer un fichier dans un emplacement donne
# mv effectue un renommage si le second argument est dans le meme repertoire.
mv bonjour ave
```
- Qu'affiche maintenant `ls -l` ?

- Selon vous, quel est le type du fichier `ave`?

- En utilisant la commande `file ave`, vérifier le type du fichier.

- Renommez le fichier  `ave` en `ave.png`

- Quel est le type du fichier `ave.png`?

- Vérifier le type avec la commande `file ave.png`. Est-ce que le type a changé?

- Que se passe-t-il si on affiche le contenu de `ave.png` ou si on essaye de l'éditer avec 
  vim par exemple?
  
- Quelle extension donneriez-vous à ce fichier (`ave.png`)?

- Renommez le fichier `ave.png` en `ave.txt`

- Que se passe-t-il si on affiche le contenu de `ave.txt` ou si on essaye de l'éditer ?

- Vérifier le statut avec la commande `stat ave.txt`
- Créer un fichier  `jour.txt` avec le contenu `Bonjour`
- Créez un fichier  `soir.txt` avec le contenu `Bonsoir`
- Créez un fichier  `nuit.txt` avec le contenu `Bonne nuit`
- Tapez la commande `ls -l` pour voir le contenu du répertoire
- Avec la commande `cat`, affichez respectivement le contenu des fichiers
> - `cat jour.txt`
> - `cat soir.txt`
> - `cat nuit.txt`
- Renommez le fichier `jour.txt` en `soir.txt` avec la commande `mv jour.txt soir.txt`
- Affichez le contenu du dossier avec `ls -l`. 
- Affichez le contenu du fichier `soir.txt`. Qu'est-ce qui a changé?
- Renommez le fichier `ave.txt` en `nuit.txt` avec la commande `mv -b ave.txt nuit.txt`
- Affichez le contenu du dossier avec `ls -l`. 
- Avez vous un fichier `nuit.txt~` dans le dossier?
- Que contient  `nuit.txt`?
- Que contient  `nuit.txt~`?

### 1.3 : Copie

- Tapez la commande `cp nuit.txt ave.txt` pour copier  le fichier `nuit.txt`vers `ave.txt`
- Afficher les statuts des fichiers `nuit.txt` et  `ave.txt`. Est-ce que les dates 
  sont identiques?
- En utilisant l'option `-p` de la commande `cp`, copier le fichier `soir.txt` vers 
  `matin.txt`
- Afficher les statuts avec la commande `stat`
- En utilisant l'option `-b` de la commande `cp` copier le fichier `nuit.txt`vers `matin.txt`
- Affichez le contenu du dossier avec `ls -l`
- Avez-vous un fichier `matin.txt~` dans le dossier?
- En utilisant l'option `--suffix=old` copiez le fichier  `matin.txt~` vers `ave.txt`.
- Affichez le contenu du dossier avec `ls -l`
- Avez-vous un fichier `ave.txtold` dans le dossier?

## Exercice 2 : Répertoires (60 mins)

### 2.1 : Répertoires

- Avec la commande `mkdir`, créez un répertoire `dir` et déplacez `ave.txt` dedans.

- Vérifiez le statud de `dir/ave.txt` avec la commande `stat`.
- Une utilisant l'opption `-p` de la commande `mkdir`, créez une seule commande le 
  dossier et le sous dossier `cours/inf1070`
- Copiez le fichier `dir/ave.txt` vers `cours/inf1070/avenue.txt`
- Allez dans le dossier `dir`
- Tout en étant dans le dossier `dir`, utilisez un chemin relatif pour créer un sous 
  dossier `inf1120`dans le dossier `cours`
- Revenez sur le dossier parent. 
- Avec la commande `tree cours`, affichez la structure de du dossier `cours`
- Avec une seule commande, créez un dossier ayant la structure suivante.
~~~csh
 Web
├── inf3190
│   ├── examen
│   ├── quiz
│   └── tp
└── INF5190
    └── evaluation
~~~

<!-- Solution
mkdir -p Web/{inf3190/{tp,quiz,examen},INF5190/evaluation}
--> 
- Allez dans le dossier `evaluation`
- A partir du dossier `evaluation`, tapez une seule commande pour aller dans le dossier 
  `quiz`
- A partir du dossier `quiz`, où vous amène la commande `cd -` sans aucun utre argument 
  ni option?




