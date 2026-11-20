# TP6 — Variables d’environnement, inputs et outputs

## Q1. Quand les variables écrites dans `GITHUB_ENV` deviennent-elles disponibles ?

Le runner lit le fichier `GITHUB_ENV` à la fin de la step qui y écrit, puis ajoute les variables à l’environnement des steps suivantes du même job. Pendant `Set environment variables`, les deux commandes `echo` écrivent dans le fichier et laissent l’environnement du shell courant tel quel. Dans `Print environment variables`, `APP_NAME` et `BUILD_DATE` sont disponibles.

## Q2. Quelle est la portée de `GITHUB_ENV` ?

La portée se limite aux steps suivantes du job qui a écrit dans `GITHUB_ENV`. Le job `verify-env` démarre avec son propre environnement. Sur GitHub Actions, sa step `Print APP_NAME` a affiché `APP_NAME=`, avec une valeur vide. [Exécution](https://github.com/ElMouafikFatima-Ezzahra/python-fastapi-app/actions/runs/44788425804)

## Q3. Que se passe-t-il si deux écritures utilisent `>` dans `GITHUB_OUTPUT` ?

Chaque écriture avec `>` tronque le fichier avant d’y écrire. Avec deux commandes successives dans la même step, seule la dernière valeur reste dans le fichier. L’opérateur `>>` ajoute chaque ligne à la suite des précédentes.

## Q4. Comment `full_version` passe-t-elle du job `build` au job `deploy` ?

Les variables de `GITHUB_ENV` restent dans le job qui les définit. La step `version` écrit `full_version` dans `GITHUB_OUTPUT`, le job `build` publie cette valeur dans `jobs.build.outputs`, et `deploy` la lit via `needs.build.outputs.full_version` grâce à `needs: build`.

## Q5. Que se passe-t-il si on retire `needs: build` ?

`deploy` peut démarrer indépendamment de `build` et ne reçoit plus sa sortie. Dans l’essai GitHub Actions sans `needs: build`, le workflow a réussi, mais `deploy` a affiché `Deploying  to staging`, avec une version vide. Avec la dépendance, il a affiché `Deploying 1.0.0-2026-11-20 to staging`. J’ai ensuite rétabli `needs: build` sur la branche. [Sans dépendance](https://github.com/ElMouafikFatima-Ezzahra/python-fastapi-app/actions/runs/44788731741) · [Avec dépendance](https://github.com/ElMouafikFatima-Ezzahra/python-fastapi-app/actions/runs/44788425804)
