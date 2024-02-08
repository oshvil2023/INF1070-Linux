# Laboratoire 5 : Chercher, filtrer couper

## Exercice 1 : Dictionnaires de mots (30 mins)

### 1 : Récupérer une liste de mots

Consultez le répertoire `/usr/share/dict/`. Il devrait contenir différents
fichiers textes contenant des dictionnaires. Pour cet exercice, nous utiliserons
le dictionnaire contenu dans le fichier `/usr/share/dict/words`, mais s'il n'est
pas disponible sur votre machine, vous pouvez choisir n'importe lequel.

Pour installer un dictionnaire  français dans `/usr/share/dict`:

~~~csh
sudo apt install wfrench
~~~

Si vous avez déjà installé une autre langue (ex: anglais), vous pouvez changer le 
dictionnaire par défaut (ayant pour lien `/usr/share/dict/words`) avec la commande.

~~~csh
sudo select-default-wordlist
~~~

La commande `grep` vous sera utile ici. En particulier, deux caractères spéciaux
permettent d'identifier le début d'une ligne (caractère chapeau `^`) et la fin
d'une ligne (caractère `$`).

```
# american-english
cd usr/share/dict
```
### 2 : Questions

Répondez en particulier aux questions suivantes:

1. Combien de mots contient le dictionnaire?
```
# -l = line
wc -l
```
2. Combien de mots contiennent la chaîne `with`?
```
grep with american-english | wc -l
grep -c with american-english 
```
3. Combien de mots commencent par la chaîne `with`?

```
grep "^with" american-english | wc -l
```

4. Combien de mots terminent par la chaîne `with`?

```
grep "with$" american-english | wc -l
```
5. Combien de mots terminent par `'s`?
```sh
grep "'s"$ word | wc -l
```

Ensuite, à l'aide de la commande `column` effectuez les actions suivantes:

6. Placez tous les mots qui commencent par la lettre majuscule `T` et placez-les
   dans un fichier nommé `T.txt` en les répartissant sur 4 colonnes.

```
grep "^T" american-english | column -c 64 > T.txt
```

7. Placez tous les noms propres (mots qui commencent par une majuscule) et
   placez-les dans un fichier nommé `noms-propres.txt`. Combien y en a-t-il?

```
grep "^[A-Z]" american-english
```

## Exercice 2 : Base de données textuelle (60 mins)

[GeoNames](https://www.geonames.org/) est un projet qui fournit gratuitement
différentes bases de données sous format textuel sur des lieux géographiques un
peu partout sur la planète.

Pour cette question, voici quelques commandes qui pourraient vous être utiles.
N'hésitez pas à consulter leur manuel pour mieux connaître les options:

- `wget`, pour télécharger un fichier
- `wc`, pour compter le nombre de lignes, caractères, etc. d'un fichier
- `cut`, pour extraire une partie de ligne
- `grep`, pour sélectionner les lignes contenant un certain motif
- `sort`, pour trier des lignes selon certains critères
- `uniq`, pour supprimer les lignes consécutives identiques
- `head`, pour récupérer les première lignes d'un fichier
- `tail`, pour récupérer les dernières lignes d'un fichier

### 1 : Récupérer les fichiers

Rendez-vous sur la [page qui contient les
données](http://download.geonames.org/export/dump/).

À l'aide d'une commande, téléchargez en ligne de commande les fichiers
`readme.txt`, `countryInfo.txt` et `CA.zip`.

Consultez le fichier `readme.txt` afin de vous familiariser avec la structure et
le contenu des autres fichiers.

Consultez ensuite le fichier `countryInfo.txt` pour étudier son contenu.

Toujours en ligne de commande, décompressez le fichier `CA.zip` et ouvrez-le
pour vous familiariser avec son contenu. Notez sa taille et son nombre de
lignes.

### 2 : Nettoyage des fichiers

Comme les fichiers `countryInfo.txt` et `CA.txt` contiennent des champs vides,
il convient d'abord de les nettoyer en insérant des valeurs `N/A`.

Pour cela, utilisez le script exécutable [`clean`](./clean) et placez les
résultats dans les fichiers `country-clean.txt` et `CA-clean.txt`.

### 3 : Supprimer les commentaires

Entrez la commande

```sh
grep -v '^#' countryInfo.txt
```

Celle-ci utilise l'expression régulière `^#` qui correspond à toutes les lignes
qui commencent par le caractère `#`. En particulier, le caractère `^` indique le
début d'une ligne.

En lisant le manuel, vérifiez le rôle de l'option `-v`.

La commande qui utilise `grep` ci-haut vous sera utile pour la suite lorsque
vous ferez des requêtes sur les différents fichiers afin d'éliminer les lignes
qui contiennent des commentaires. N'hésitez pas à sauvegarder, si vous le
souhaitez, une version "nettoyée" de chacun des fichiers à l'aide d'une
redirection `>`.

### 4 : Requêtes sur des pays

En utilisant le moins de commandes possibles, répondez aux questions suivantes.

1. Quels sont les codes de 3 lettres des 10 pays dont la population est la plus
   importante?
   ```
   sort -t$'\t' -nk 9 country-clean2.txt | cut -f 2 | head -n 10
   ```
2. Quels sont les codes de 3 lettres des 20 pays dont la superficie est la plus
   grande?
   ```
   sort -t$'\t' -nk  8 country-clean2.txt | cut -f 2 | head -n 20
   ```
3. Combien existe-t-il de monnaie officielle différente sur notre planète?
```
cut -f 11 country-clean2.txt | sort -u | wc -l
```
4. Combien y a-t-il de pays par continent?
```
cut -f 9 country-clean2.txt | sort | uniq -c
```
### 5 : Requêtes sur le Canada

En utilisant le moins de commandes possibles, répondez aux questions suivantes.

1. Quels sont les fuseaux horaires possibles au Canada? Combien y en a-t-il?

```
cut -f 18 CA-clean.txt | grep -v "N/A" | sort -u | wc -l
```

2. Quels sont les lieux qui contiennent la chaîne `Longueuil`? Combien y en
   a-t-il?

```
grep Longueuil CA-clean.txt | wc -l
```

3. Quelles sont les données qui ont été modifiées en 2018?

```
grep 2018 CA-clean.txt | wc -l
```

4. Quelles sont les longitudes minimale et maximale, ainsi que les latitudes
   minimale et maximale des lieux décrits dans le fichier `CA.txt`?

```
# longitude maximale
cut -f 5 CA-clean.txt | sort -u | tail -n 1
# longitude minimale
cut -f 5 CA-clean.txt | sort -u | head -n 1
# latitude max
cut -f 6 CA-clean.txt | sort -u | tail -n 1
# latitude min
cut -f 6 CA-clean.txt | sort -u | head -n 1
```
