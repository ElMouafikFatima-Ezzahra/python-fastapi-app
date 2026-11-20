# TP6 — Variables d’environnement, inputs et outputs

## Q1. Quand les variables écrites dans `GITHUB_ENV` deviennent-elles disponibles ?

Le runner lit le fichier `GITHUB_ENV` à la fin de la step qui y écrit, puis ajoute les variables à l’environnement des steps suivantes du même job. Pendant `Set environment variables`, les deux commandes `echo` écrivent dans le fichier et laissent l’environnement du shell courant tel quel. Dans `Print environment variables`, `APP_NAME` et `BUILD_DATE` sont disponibles.

## Q2. Quelle est la portée de `GITHUB_ENV` ?

La portée se limite aux steps suivantes du job qui a écrit dans `GITHUB_ENV`. Le job `verify-env` démarre avec son propre environnement. Le résultat attendu dans sa step `Print APP_NAME` est donc `APP_NAME=`, avec une valeur vide.
