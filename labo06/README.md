# Laboratoire 6 : Expressions régulières

## Exercice 1 : Français (60 mins)

Sous Debian (et dérivés) le paquet `wfrench` fournit `/usr/share/dict/french`
qui contient de nombreux mots de la langue française.

Si vous n'arrivez pas à installer le paquet `wfrench` (parce que vous n'avez
pas les droits d'installation, par exemple), vous pouvez le télécharger [dans
ce dépôt](./french).

En utilisant la commande `grep` et les expressions régulières basiques (BRE)
vues en classe:

- Quels mots contiennent « `titi` » ?
  Exemple: « `dentition` »
- Quels mots contiennent deux fois « `ren` » avec une seule lettre entre les
  deux `ren` ?
  Exemple: « `égrenèrent` »
- Quels mots contiennent un « `k` » et plus loin un « `w` » ?
  Exemple: « `kiwi` »
- Quels mots contiennent un « `k` » et « `w` » dans n'importe quel ordre ?
  Exemple: « `tomahawk` » (Aide: utilisez l'option `-e` de grep)
- Quels mots finissent par « `latif` » ?
  Exemple: « `législatif` »
- Quels mots commencent et finissent par « `dé` » ?
  Exemple: « `débordé` »
- Quels mots de 10 lettres commencent et finissent par « `ent` »  ?
  Exemple: « `entretient` »
- Quels mots finissent par « `st` » mais ne contiennent pas d'autre « `s` » ou
  « `t` » ?
  Exemple: « `compost` »
- Quels mots contient trois trais d'union (« `-` ») ?
  Exemple: « `je-ne-sais-quoi` »
- Quels mots ont trois « `e` » séparés par des « t » en ignorant les accents ?
  Exemple: `netteté`

En utilisant l'option `-o` de grep, des tubes, et les commandes `sort` et
`uniq`:

- Quelle est la dernière lettre la plus fréquente ?
- Quelle est l'avant-dernière lettre (celle qui précède la dernière) la plus
  fréquente ?

## Exercice 2 : Regexone (15 mins)

Rendez-vous sur le site https://regexone.com/ et complétez les leçons 1 à 5.

## Exercice 3 : `man grep` (15 mins)

- Lancez le manuel de `grep` avec `man grep`. Notez que `man` utilise par
  défaut le paginateur `less` pour lire une page de manuel.
  Note: lancez `man` avec l'option `-LC` pour avoir la page en anglais.
- Effectuez une recherche (en commençant par `/`) afin trouver la définition de
  l'acronyme PCRE
- Utilisez la touche « `n` » pour chercher les occurences suivantes
- Ensuite, recherchez l'expression `\{n?,?m?\}`. Est-ce que la recherche dans
  `less` suit une convention POSIX?
- Cherchez les options courtes de grep qui utilisent une lettre majuscule.
  *Note:* Par défaut, `less` effectue des recherches insensibles à la casse.
  Pour désactiver ce comportement, il est possible de taper `-i` pour rendre la
  recherche sensible à la casse.
- Cherchez les options longues de grep qui ont un `-` dans leur nom et prennent
  une valeur.
  Exemple: « `--max-count=NUM` » ou « `--after-context=NUM` », mais pas
  « `--fixed-strings` »
