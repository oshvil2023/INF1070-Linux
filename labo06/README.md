# Laboratoire 6 : Expressions régulières

## Exercice 1 : Français (60 mins)

Sous Debian (et dérivés) le paquet `wfrench` fournit `/usr/share/dict/french`
qui contient de nombreux mots de la langue française.

Si vous n'arrivez pas à installer le paquet `wfrench` (parce que vous n'avez
pas les droits d'installation, par exemple), vous pouvez le télécharger [dans
ce dépôt](./french).

En utilisant la commande `grep` et les expressions régulières basiques (BRE)
vues en classe:

```
# /usr/ est un repertoire privil´egi´e.
# Root est par d´efaut capable d'y faire des modifications.
cp /usr/share/dict/french ~/Desktop/french
# ou bien `a partir de gitlab
wget https://gitlab.info.uqam.ca/inf1070/labs/-/blob/master/labo06/french
```

- Quels mots contiennent « `titi` » ?
  Exemple: « `dentition` »
```
grep titi french
```
- Quels mots contiennent deux fois « `ren` » avec une seule lettre entre les
  deux `ren` ?
  Exemple: « `égrenèrent` »
```
# avec grep, . veut dire n'importe quel caractere
# et .* veut dire n'importe quels caracteres (plusieurs).
grep ren.ren french
```
- Quels mots contiennent un « `k` » et plus loin un « `w` » ?
  Exemple: « `kiwi` »
```
grep k.*w french
# aussi acceptable mais non optimal
grep .*k.*w french
```
- Quels mots contiennent un « `k` » et « `w` » dans n'importe quel ordre ?
  Exemple: « `tomahawk` » (Aide: utilisez l'option `-e` de grep)
```
# -e pour dire que c'est une expression r´eguli`ere
# \| signifie op´erateur ou.
# | a besoin d'etre echapp´e d'ou le \.
grep -e ".*k.*w\|.*w.*k" french
```
- Quels mots finissent par « `latif` » ?
  Exemple: « `législatif` »
```
grep latif$ french
```
- Quels mots commencent et finissent par « `dé` » ?
  Exemple: « `débordé` »
```
grep ^d´e.*d´e$ french
```
- Quels mots de 10 lettres commencent et finissent par « `ent` »  ?
  Exemple: « `entretient` »
```
grep -P '^.{7}ent$' french
# ou
# -E pour dire expression reguliere etendue.
# ^[[:alpha:]]{7}ent(symbole_dollar) veut dire une chaine de 7 caracteres
# (peut importe) qui se terminent par ent.
grep -E '^[[:alpha:]]{7}ent$' french
# ou
grep '^.......ent$' french
```
- Quels mots finissent par « `st` » mais ne contiennent pas d'autre « `s` » ou
  « `t` » ?
  Exemple: « `compost` »
```
grep -P '^[^st]*st$' french
```
- Quels mots contient trois trais d'union (« `-` ») ?
  Exemple: « `je-ne-sais-quoi` »
```
grep -E '^.*-.*-.*-.*$' french
```
- Quels mots ont trois « `e` » séparés par des « t » en ignorant les accents ?
  Exemple: `netteté`
```
grep -P '^.*[e´e`e^e¨e]t+[e´e`e^e¨e]t+[e´e`e^e¨e].*$' french
```

En utilisant l'option `-o` de grep, des tubes, et les commandes `sort` et
`uniq`:
- Quelle est la dernière lettre la plus fréquente ?
```
grep -o .$ french | sort | uniq -c
```
- Quelle est l'avant-dernière lettre (celle qui précède la dernière) la plus
  fréquente ?
```
grep -Po '..$' french | sort | grep -o ^. | uniq -c
```

## Exercice 2 : Regexone (15 mins)

Rendez-vous sur le site https://regexone.com/ et complétez les leçons 1 à 5.

#### lecon 1
```
```
#### lecon 2
```
Objective:
Task	Text	 
Match	cat.	
Match	896.	
Match	?=+.	
Skip	abc1
...\.
```
#### lecon 3
```
Objective:

match   can
match   man
match   fan
skip    dan
skip    ran
skip    pan

# Soit c, m, ou f. Apres ces caracteres, an doit obligatoirement figurer
[cmf]an
# ou
# Exclure d, r, ou p. Mais an doit figurer.
[^drp]an

([cmf]+[an]+)[^d]
([cmf]+[an]{2})[^d]
```
#### lecon 4
```
Objective:

match   hog
match   dog
skip    bog
Solutions:

[^b]og
# ou
[hd]og

([d-o]+)[^bg]
```
#### lecon 5
```
Objective:

match Ana
match Bob
match CpC
skip  aax
skip  bby
skip  ccz
Solutions:

# Trois caract`eres
# [A-C] premier caract`ere entre A et C
# [n-p] deuxi`eme caract`ere entre n et p
# [a-c] troisieme caractere entre a et c
[A-C][n-p][a-c]

([A-Ca-p]+)[^a-cx-z]
```
#### lecon 6
```
Objective:

match   wazzzzup
match   wazzzup
skip    wazup
Solutions:

([wa]+[z]{3,4}[up]+)
```
#### lecon 7
```
Objective:

match   aaaabcc
match   aabbbbc
match   aacc
Solutions:

(a+b*c+)
```
#### lecon 8
```
Objective:

match   1 file found?
match   2 files found?
match   x files found?
Solutions:

([\d\w+]\s[file?s]+\sfound\?)
```
#### lecon 9
```
Objective:

match   1.   abc
match   2.    abc
match   3.                   abc
skip    4.abc
Solutions:

([\d\.]+\s+[a-c]+)          # matches any whitespace
([\d\.]+[" "|\t]+[a-c]+)    # specifically matches spaces and tab-based whitespace
```
#### lecon 10
```
Objective:

match   Mission: successful
skip    Last Mission: unsuccessful
skip    Next Mission: successful upon capture of target
Solutions:

^([a-zA-z]+\:\s?successful)$
```
#### lecon 11
```
Objective:

match   file_a_record_file.pdf
match   file_yesterday.pdf
skip    testfile_fake.pdf.tmp    
Solutions:

([a-z+\_?]+)\.pdf$
([a-z+\_?]+)(?=\.pdf$)      # using positive lookahead
```
#### lecon 12
```
Objective:

match   Jan 1987    capture     Jan 1987, 1987
match   May 1969    capture     May 1969, 1969
match   Aug 2011    capture     Aug 2011, 2011
Solutions:

^([a-zA-z]+\s+([\d]+))$
```
#### lecon 13

#### lecon 14

#### lecon 15


## Exercice 3 : `man grep` (15 mins)

- Lancez le manuel de `grep` avec `man grep`. Notez que `man` utilise par
  défaut le paginateur `less` pour lire une page de manuel.
  Note: lancez `man` avec l'option `-LC` pour avoir la page en anglais.
  
- Effectuez une recherche (en commençant par `/`) afin trouver la définition de
  l'acronyme PCRE

- Utilisez la touche « `n` » pour chercher les occurences suivantes

- Ensuite, recherchez l'expression `\{n?,?m?\}`. Est-ce que la recherche dans
  `less` suit une convention POSIX?
```
/`\{n?,?m?\}`
```
- Cherchez les options courtes de grep qui utilisent une lettre majuscule.
  *Note:* Par défaut, `less` effectue des recherches insensibles à la casse.
  Pour désactiver ce comportement, il est possible de taper `-i` pour rendre la
  recherche sensible à la casse.
```
/-[A-Z]\b
```
- Cherchez les options longues de grep qui ont un `-` dans leur nom et prennent
  une valeur.
  Exemple: « `--max-count=NUM` » ou « `--after-context=NUM` », mais pas
  « `--fixed-strings` »
```
/--.*-.*=
```
