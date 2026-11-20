# TP6 — Variables d’environnement, inputs et outputs

## Q1. Quand les variables écrites dans `GITHUB_ENV` deviennent-elles disponibles ?

Le runner lit le fichier `GITHUB_ENV` à la fin de la step qui y écrit, puis ajoute les variables à l’environnement des steps suivantes du même job. Pendant `Set environment variables`, les deux commandes `echo` écrivent dans le fichier et laissent l’environnement du shell courant tel quel. Dans `Print environment variables`, `APP_NAME` et `BUILD_DATE` sont disponibles.

## Q2. Quelle est la portée de `GITHUB_ENV` ?

La portée se limite aux steps suivantes du job qui a écrit dans `GITHUB_ENV`. Le job `verify-env` démarre avec son propre environnement. Le résultat attendu dans sa step `Print APP_NAME` est donc `APP_NAME=`, avec une valeur vide.

## Q3. Que se passe-t-il si deux écritures utilisent `>` dans `GITHUB_OUTPUT` ?

Chaque écriture avec `>` tronque le fichier avant d’y écrire. Avec deux commandes successives dans la même step, seule la dernière valeur reste dans le fichier. L’opérateur `>>` ajoute chaque ligne à la suite des précédentes.

## Q4. Comment `full_version` passe-t-elle du job `build` au job `deploy` ?

Les variables de `GITHUB_ENV` restent dans le job qui les définit. La step `version` écrit `full_version` dans `GITHUB_OUTPUT`, le job `build` publie cette valeur dans `jobs.build.outputs`, et `deploy` la lit via `needs.build.outputs.full_version` grâce à `needs: build`.

## Q5. Que se passe-t-il si on retire `needs: build` ?

`deploy` perd sa dépendance à `build` et la référence `needs.build.outputs.full_version` sort de son contexte. Dans l’essai local sans `needs: build`, `actionlint` a signalé que la propriété `build` était absente de `needs`. La vérification a réussi après restauration de la dépendance.
