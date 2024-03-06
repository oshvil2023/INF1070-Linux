# Laboratoire 7 : Expressions régulières, la suite

## 1. Miner des adresses de courriel (30 mins)

* Récupérez un document pdf sur le web qui contient des courriels avec
  `wget`
* Par exemple:
  [ici](http://www.international.uqam.ca/pages/docs/cooperation/2016-02-25_Liste_participants_post_aiea_uqam.pdf)
* Convertissez le fichier en format texte avec `pdftotext` (extra)
* Extrayez les courriels à l'aide de `grep` et placez-les dans un fichier, une
  adresse courriel par ligne.
* Pas besoin d'utiliser une expression régulière infaillible, l'important,
  c'est que ça fonctionne pour la plupart des adresses !
* En particulier, il se peut que vous manquiez certains courriels qui sont mal
  alignés en raison de césures par exemple

  ```
  grep -iE "[.a-z0-9-]+@" professor.txt
  ```

## 2. Expressions régulières simples (40 mins)

Complétez les 15 leçons et les 8 problèmes sur le site https://regexone.com.

lecon 1:

```
abc
# ou
123
```

lecon 2:

```
# ... = trois caracteres et \. = le caractere . specifiquement
...\.
```

lecon 3:

```
# Soit c, m, ou f. Apres ces caracteres, an doit obligatoirement figurer
[cmf]an

# ou 
# Exclure d, r et p. Mais "an" doit figurer
[^drp]an

```

lecon 4:

```
[^b]og
# ou
[hd]og
```

lecon 5:

```
# Trois caracteres
# [A-C] pour le premiere caractere
# [n-p] pour la deuxieme caractere
# [a-c] pour la troisieme caractere
[A-C][n-p][a-c]
```

lecon 6:

```
waz{3,5}up
```


lecon 7:

```
aa+b*c+
```


lecon 8:

```
\d+ files? found\?
```


lecon 9:

```
\d\.\s+abc
```

lecon 10:

```
^Mission: successful$
```


lecon 11:

```
^(file.+)\.pdf$
```


lecon 12:

```
(\w+(\d+))
```

lecon 13:

```
(\d+)x(\d+)
```

lecon 14:

```
I love (cats|dogs)
```

lecon 15:

```
.*
```

## 3. Mots croisés et expressions régulières (30 mins)

Complétez quelques grilles de « mots croisés » sur le site
https://regexcrossword.com/.

## 4. Golf (20 mins)

En utilisant le moins de caractères possibles, essayez d'obtenir une
correspondance pour des ensembles de mots donnés: https://alf.nu/RegexGolf.

*Note:* Dans un premier temps, essayez de trouver une expressions qui
fonctionne, peu importe sa longueur, puis ensuite, réduisez la longueur.

## 5. Extra (∞ mins)

En ERE pur (pas PCRE), extrayez les chaînes qui commencent par `ba` et finissent
par le `ud` ou le `rd` le plus proche.

Rappel: en PCRE `grep -P --color 'ba.*?[ur]d'` fonctionne, mais comment faire en
ERE ?

Testez avec `cobalourdeaubobardumbadaududosbarbustandardoise`. Note : l'option `--color` de `grep` est plus utile que l'option `-o` pour détecter rapidement les différences.

~~~
$ echo 'cobalourdeaubobardumbadaududosbarbustandardoise' | grep -Po 'ba.*?[ur]d'
balourd
bard
badaud
barbustandard
~~~

Attention. Il est assez facile de trouver une expression régulière qui semble
fonctionner mais qui en fait est fausse. La chaîne de test suivante est plus
complète (mais pas parfaite encore):

~~~
cobalourdeaubobardumbadaududosbarbustandardoiseuurddrdbaddbaddrurubabadrurudddrurudbaururbadrurudddurddbarurubadddrbaurdddrudrdubarurdddrdbarddrdbaururba
~~~

Pour tester, comparez encore une fois votre expression régulière ERE avec la
version PCRE:

~~~
$ echo cobalourdeaubobardumbadaududosbarbustandardoiseuurddrdbaddbaddrurubabadrurudddrurudbaururbadrurudddurddbarurubadddrbaurdddrudrdubarurdddrdbarddrdbaururba > cobal
$ grep -Po 'ba.*?[ur]d' cobal
balourd
bard
badaud
barbustandard
baddbaddrurubabadrurud
baururbadrurud
barurubadddrbaurd
barurd
bard
~~~

Si vous trouvez quelque chose qui fonctionne, envoyez-moi votre expression en
privé à votre professeur sur le slack.
*Note*: la version la plus courte trouvée fait 24 caractères, des plus
longues fonctionnent aussi.


