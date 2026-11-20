# TP7 — Actions tierces et actions personnalisées

## Q1. Pourquoi `actions/checkout` fonctionne-t-elle sans `with` dans ce workflow ?

Par défaut, `actions/checkout` récupère le dépôt et la révision associés à l’exécution. Ces valeurs suffisent ici. Dans `Setup Node.js`, `with` permet de demander explicitement Node.js 20 et d’obtenir la même version majeure même si l’image du runner évolue.

## Q2. Pourquoi `verify` doit-il télécharger `report.txt` ?

Sur GitHub Actions, chaque job hébergé dispose de son propre espace de travail. `report.txt` est créé pendant `build` et ne fait pas partie du dépôt. `needs: build` fixe l’ordre d’exécution. `upload-artifact` publie le fichier sous le nom `build-report` et `download-artifact` le récupère dans `verify`.
