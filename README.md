# Tournoi de bots de Dix

Le défi de ce tournoi est de programmer des stratégies automatiques capables de jouer au [jeu du Dix](https://wiki.aediroum.ca/wiki/Jeu_du_10).
Les soumissions sont acceptées du **lundi 4 mars 2024 à 00h00** au **dimanche 31 mars 2024 à 23h59**.
Au terme de cette période, le jury évaluera les soumissions en utilisant [Onze](https://github.com/matteodelabre/onze).
Un événement spécial sera organisé pour dévoiler les vainqueurs.

## Règlement

### Soumission

- Chaque personne peut soumettre au plus 3 bots uniques
- Les soumissions peuvent être faites en équipe
- Format de chaque soumission
    - Archive `tar.gz` ou `zip` d’**au plus 10 GiB**
    - Doit contenir un script `compile` et un script `run`

### Environnement

- Conteneur _Arch Linux_ à jour avec [base-devel](https://archlinux.org/packages/core/any/base-devel/)
- Langages
    - Bash
    - C (gcc)
    - C++ (g++)
    - Java
    - Julia
    - Prolog (SWI Prolog)
    - Python 3
    - Rust
    - OCaml
    - Haskell (GHC)
    - _(d’autres langages pourront être ajoutés sur demande)_

### Compilation

- L’archive est décompressée et le script `compile` est exécuté une seule fois
- Ressources
    - CPU: 4 processus ou threads
    - GPU: Aucun
    - Mémoire: 16 GiB
    - Temps: 10 min
    - Réseau: Aucun accès
    - IPC: Aucune communication avec d’autres processus
    - Système de fichiers
        - Lecture seule, sauf le répertoire du bot en lecture/écriture
        - Limite d’espace total à 25 GiB

### Exécution

- Le script `run` est utilisé pour exécuter le bot
- Ressources
    - CPU: 1 processus, 1 thread
    - GPU: Aucun
    - Mémoire: 4 GiB
    - Temps
        - Startup time de 10 s pour chaque processus avant de commencer les games
        - 100 ms par bot par tour (continue de s’exécuter pendant le tour des autres joueurs)
    - Réseau: Aucun accès
    - IPC: Aucune communication avec d’autres processus
    - Système de fichiers: Tout en lecture seule

### Évaluation

- Chaque bot affronte chaque autre bot soumis dans le tournoi, y compris lui-même
    - Évaluation de deux bots C et J
    - Première série: Joueurs C, J, C, J
    - Deuxième série: Joueurs J, C, J, C
    - Au début de chaque série on remet la seed aléatoire à la même valeur
    - Chaque série est composée de 10 parties de 500 points
        - Round (brasse): ~5 s
        - Partie (500 points): ~1 min
        - Série (10 parties): ~10 min
        - Total (2 séries): ~20 min
    - Score de l’affrontement 
        - Nombre de parties gagnées moins nombre de parties perdues
        - Si égalité, somme des différences de points sur toutes les parties
- Classement final
    - Somme des scores finaux pour chaque affrontement avec un autre bot
    - Classement par score total décroissant
    - Possibilité d’ajustement de l’ordre des bots en fonction de si un bot bat d’autres bots qui sont classés plus haut que lui

### Récompenses

- Trophée pour le bot gagnant
- Récompense monétaire pour les 3 premières personnes distinctes du classement
    - 100\$, 75\$ et 50\$
    - Les membres d’une équipe partagent leur récompense à leur discrétion
    - **Les récipiendaires acceptent que leur code source soit publié**
- Mentions spéciales
    - Bot au code le plus court parmi le 25% des premiers bots
    - Bot qui joue le plus vite en moyenne
    - Bot qui fait avancer l’état de l’art en matière de technique du jeu de 10
