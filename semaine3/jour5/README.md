# Formation devOps
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 3 - GIT JIRA et CI

### Jour 5 : Jest ###

---

**1 - JEST BEGIN**

[ ] <ins>### Install ###</ins>

Vous avez eu l’occasion de découvrir la notion de test end-to-end avec Cypress et il est maintenant temps de se focaliser sur un type de test en particulier : les tests unitaires, qui font partie intégrante de la notion de tests e2e.

Les tests unitaires ont pour seul objectif de vérifier le retour d’une fonction créée par les développeurs, sans pour autant vérifier son intégration dans le projet d’un point de vue utilisateur final.

Ce challenge constitue l’occasion de prendre en main le fonctionnement global de Jest, un framework de tests unitaires pour les projets web & mobile en JavaScript.

👉 Récupérez la ressource "jestbegin.zip" depuis l’onglet dédié sur Ariane et décompressez l’archive.

Cette archive contient un simple projet JavaScript avec quelques fonctions qui permettent d’effectuer l’addition, la soustraction ou la multiplication de deux nombres.

👉 En vous basant sur la documentation, installez Jest via la commande yarn, tout en étant positionné dans le répertoire du projet.

👉 Ajoutez la section suivante dans le fichier "package.json" afin que la commande yarn test puisse exécuter Jest.

"scripts": {

  "test": "jest"

},
