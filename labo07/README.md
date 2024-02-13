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

## 2. Expressions régulières simples (40 mins)

Complétez les 15 leçons et les 8 problèmes sur le site https://regexone.com.

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


