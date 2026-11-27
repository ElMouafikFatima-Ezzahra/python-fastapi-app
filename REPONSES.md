# TP8 — Stratégies GitHub Actions

## Q1 — Combien de jobs sont générés ?

Six jobs sont générés dans la matrice de base.

- Ubuntu : Python 3.11, 3.12 et 3.13.
- Windows : Python 3.11, 3.12 et 3.13.

## Q2 — Combien de jobs au total ?

Six. On retire Windows avec Python 3.11 et on ajoute Ubuntu avec Python 3.14 en mode expérimental.

## Q3 — Que se passe-t-il si on exclut Python 3.14 ?

La combinaison reste présente. GitHub applique `exclude` à la matrice de base, puis ajoute Ubuntu avec Python 3.14 via `include`.

## Q4 — Quelle différence observe-t-on avec fail-fast ?

Avec `true`, les quatre jobs Ubuntu ont réussi. Windows avec Python 3.13 a échoué et Windows avec Python 3.12 a été annulé. Avec `false`, les quatre jobs Ubuntu ont réussi et les deux jobs Windows ont échoué sur le même test. Aucun job n’a été annulé.

J’utiliserais `true` pour arrêter rapidement un contrôle après un échec bloquant, et `false` pour obtenir le résultat de chaque configuration.

## Q5 — Pourquoi utiliser max-parallel en entreprise ?

1. Réserver une partie de la capacité des runners aux autres workflows.
2. Éviter de saturer un service partagé, par exemple une base de données de test.

## Captures d’écran

- [Partie 1 — Matrice de base](screenshots/tp8-matrix-partie1.png)
- [Partie 2 — Include et exclude](screenshots/tp8-matrix-partie2.png)
- [Partie 3 — Fail-fast activé](screenshots/tp8-fail-fast-true.png)
- [Partie 3 — Fail-fast désactivé](screenshots/tp8-fail-fast-false.png)
- [Partie 4 — Max-parallel](screenshots/tp8-max-parallel.png)
