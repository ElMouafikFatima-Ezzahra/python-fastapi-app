# TP7 — Actions tierces et actions personnalisées

## Q1. Pourquoi `actions/checkout` fonctionne-t-elle sans `with` dans ce workflow ?

Par défaut, `actions/checkout` récupère le dépôt et la révision associés à l’exécution. Ces valeurs suffisent ici. Dans `Setup Node.js`, `with` permet de demander explicitement Node.js 20 et d’obtenir la même version majeure même si l’image du runner évolue.

## Q2. Pourquoi `verify` doit-il télécharger `report.txt` ?

Sur GitHub Actions, chaque job hébergé dispose de son propre espace de travail. `report.txt` est créé pendant `build` et ne fait pas partie du dépôt. `needs: build` fixe l’ordre d’exécution. `upload-artifact` publie le fichier sous le nom `build-report` et `download-artifact` le récupère dans `verify`.

## Q6. Pourquoi exécuter `actions/checkout` avant l’action locale ?

GitHub résout `./.github/actions/build-info` à partir de l’espace de travail du job. `actions/checkout` y récupère le dépôt et rend le fichier `action.yml` accessible à la step qui appelle l’action.

## Q7. Pourquoi indiquer `shell: bash` dans chaque step `run` de l’action composite ?

Le schéma d’une action composite impose à chaque step `run` de préciser son interpréteur. `shell: bash` indique au runner comment exécuter le script, quel que soit le workflow qui appelle l’action.
