# TP7 — Actions tierces et actions personnalisées

## Q1. Pourquoi `actions/checkout` fonctionne-t-elle sans `with` dans ce workflow ?

Par défaut, `actions/checkout` récupère le dépôt et la révision associés à l’exécution. Ces valeurs suffisent ici. Dans `Setup Node.js`, `with` permet de demander explicitement Node.js 20 et d’obtenir la même version majeure même si l’image du runner évolue.

## Q2. Pourquoi `verify` doit-il télécharger `report.txt` ?

Sur GitHub Actions, chaque job hébergé dispose de son propre espace de travail. `report.txt` est créé pendant `build` et ne fait pas partie du dépôt. `needs: build` fixe l’ordre d’exécution. `upload-artifact` publie le fichier sous le nom `build-report` et `download-artifact` le récupère dans `verify`.

## Q6. Pourquoi exécuter `actions/checkout` avant l’action locale ?

GitHub résout `./.github/actions/build-info` à partir de l’espace de travail du job. `actions/checkout` y récupère le dépôt et rend le fichier `action.yml` accessible à la step qui appelle l’action.

## Q7. Pourquoi indiquer `shell: bash` dans chaque step `run` de l’action composite ?

Le schéma d’une action composite impose à chaque step `run` de préciser son interpréteur. `shell: bash` indique au runner comment exécuter le script, quel que soit le workflow qui appelle l’action.

## Partie 4 — Durées mesurées sur GitHub Actions

La step `Run build info action` a commencé et s’est terminée à `18:04:11 UTC`. GitHub affiche **0 s** à la précision de la seconde. Elle a produit `my-app-1.0.0`.

La step `Run Docker hello action` a pris **4 s** (`18:04:16` à `18:04:20 UTC`). Ces quatre secondes comprennent la construction de l’image et le lancement du conteneur qui a affiché `Hello, world`. L’action composite exécute ses commandes directement sur le runner. [Exécution GitHub Actions](https://github.com/ElMouafikFatima-Ezzahra/python-fastapi-app/actions/runs/44789237673)
