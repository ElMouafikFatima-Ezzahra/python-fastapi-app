# TP7 — Sécurité des actions tierces

Le 20 novembre 2026, le dépôt `actions/setup-node` comptait 5 028 étoiles. Le code source TypeScript se trouve dans `src/`. La fiche Marketplace affiche le badge **Verified** pour le créateur `actions`. [Dépôt](https://github.com/actions/setup-node) · [Code source](https://github.com/actions/setup-node/tree/main/src) · [Fiche Marketplace](https://github.com/marketplace/actions/setup-node-js-environment)

L’essai local a remplacé temporairement `actions/checkout@v4` par `actions/checkout@main`. La variante passe la validation YAML. Le workflow a ensuite été rétabli sur `@v4` et validé de nouveau.

## Q3. Pourquoi préférer `@v4` à `@main` ?

`@main` suit chaque changement de la branche de développement, y compris des changements qui n’ont pas été publiés dans une version. `@v4` suit la version majeure 4 et peut avancer vers des correctifs de cette série. Pour figer précisément le code exécuté en production, on peut épingler le SHA complet d’un commit vérifié. [Guide GitHub](https://docs.github.com/en/actions/reference/security/secure-use)

## Q4. Que garantit le badge « créateur vérifié » ?

Il indique que GitHub a vérifié l’identité du créateur comme organisation partenaire officielle. La sécurité du code et de ses dépendances demande une vérification séparée. [Fiche Marketplace](https://github.com/marketplace/actions/setup-node-js-environment)

## Q5. Quelles vérifications faire avant d’utiliser une action inconnue en production ?

1. Examiner le code au SHA choisi, y compris `action.yml` et les scripts effectivement exécutés, pour voir à quels fichiers, secrets et services réseau l’action accède.
2. Consulter l’historique des versions et les avis de sécurité du dépôt et de ses dépendances. Vérifier que le commit choisi contient les correctifs pertinents.
