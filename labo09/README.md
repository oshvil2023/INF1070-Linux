# Laboratoire 9 : Processus

## 1. Processus et jobs (30 minutes)

- Démarrez un terminal et entrez la commande `ps`. Existe-t-il des liens de
  parenté entre les processus qui sont affichés?
- Confirmez votre réponse précédente en entrant `ps -F`.
- Lancez les processus `xeyes` et `gnome-calculator` en arrière-plan en une
  seule commande.
- Comparez les résultats des commandes `jobs`, `jobs -r` et `jobs -s`.
- Ramenez l'application `xeyes` en premier plan à l'aide de la commande `fg`.
- Interrompez `xeyes` avec `CTRL-Z`.
- Vérifiez l'état des jobs avec `jobs`.
- À l'aide de la commande `kill`, terminez l'application `xeyes`.
- Vérifiez l'état des jobs avec `jobs`.
- Terminez l'application `gnome-calculator`.
- Vérifiez l'état des jobs avec `jobs`.
- Relancez à nouveau une instance de `xeyes` et de `gnome-calculator` en
  arrière-plan.
- Ramenez `xeyes` en avant-plan avec `fg`, puis interrompez-la avec `CTRL-Z`.
- Entrez la commande `ps -f` et notez la valeur PID de `xeyes`.
- Lancez la commande `kill PID`, où `PID` est la valeur correspondante à
  `xeyes`.
- Est-ce que le processus a été interrompu? Pourquoi?
- Ramenez `xeyes` en avant-plan avec `fg`.
- Est-ce que `xeyes` est maintenant interrompu? Pourquoi?

## 2. Signaux (10 minutes)

- Lancez la commande `ls -R /`.
- Interrompez-la avec `CTRL-C`.
- Ensuite, lancez la même commande en arrière-plan `ls -R / &`.
- Que se passe-t-il si vous essayez de l'interrompre avec `CTRL-C`?
- Entrez `fg` suivi de `Enter`, pour remettre la commande en avant-plan, puis
  interrompez-la avec `CTRL-C`.

## 3. Terminer de force (20 minutes)

- Récupérez le script `love` disponible dans le répertoire courant.
- Rendez-le exécutable `chmod +x love`
- Lancez la commande `./love` normalement (en avant-plan).
- Interrompez-la avec `CTRL-C`.
- Forcez la terminaison du processus: 1. avec `kill` à partir d'un autre
  terminal, 2. en fermant le terminal, 3. avec `kill` à partir du terminal
  courant.
- Assurez-vous que le processus est bien terminé avec `ps -eF | grep love` (ou
  `pgrep -f love`)

## 4. Récursivité (20 minutes)

- Récupérez le script `fib` disponible dans le répertoire courant.
- Rendez-le exécutable `chmod +x fib`
- Lancez la commande `./fib 5` en arrière-plan et notez son `PID`.
- Lancez la commande `pstree PID`, où `PID` est l'identifiant du script lancé
  juste avant. Combien y a-t-il de processus `sleep` au total? Combien de
  processus `fib`?
- Terminez tous les processus fib avec `pkill` et `killall`
- Lancez les commandes `./fib 0`, `./fib 1`, ..., `./fib 7` en arrière-plan.
- Combien y a-t-il de processus `sleep` dans chaque cas? De processus `fib`?
- Proposez des formules qui indiquent le nombre de processus `sleep` et `fib`
  si on appelle la commande `./fib <n>`, où `<n>` est un nombre entier positif.
- Pourquoi `fib` n'apparait pas dans les premiers résultats de `top` ?

## 5. Ressources (20 minutes)

- Avec l'interface graphique, lancez chrome (ou chromium) avec plusieurs
  onglets
- Avec l'interface graphique, lancez libreoffice (ou openoffice) et ouvrez
  <http://www.openoffice.org/documentation/whitepapers/Creating_large_documents_with_OOo.odt>
- Dans une console. trouvez les processus associés à ces outils avec `ps` et
  avec `top`
- Combien de mémoire et de CPU utilisent-ils?
- Visitez <https://browserbench.org/MotionMark1.1/> et regardez en temps réel
  `top` 1. l'utilisation CPU et 2. la charge moyenne
