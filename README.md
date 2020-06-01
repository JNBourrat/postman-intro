# Introduction à Postman

## Pourquoi Postman ?

Les API font partie intégrante du travail de tout développeur web et une chose est sûre : elles sont de plus en plus nombreuses et de plus en plus complexes avec une multitude de façon de s'y authentifier (Oauth, clé API, token), de headers à gérer, de cookies, d'environnements (local, développement, intégration, recette, production), etc.

Avant de commencer le développement et de coder un quelconque connecteur à une API tierce pour une nouvelle fonctionnalité dans votre application, il peut être très avantageux de s'assurer du bon fonctionnement de la-dite API.
Dans une optique similaire, pour notre propre API cette fois-ci, on peut imaginer un processus de conception & développement dans lequel l'ensemble des requêtes nécessaires à la création d'une nouvelle fonctionnalité soit créées en amont du développement avec des tests afin de valider les signatures et la sécurité des endpoints.

Plusieurs solutions sont disponibles : [Insomnia](https://insomnia.rest/), [l'extension VSCode "REST Client"](https://marketplace.visualstudio.com/items?itemName=humao.rest-client), [Paw](https://paw.cloud/)...
L'une des applications les plus populaires, et celle sur laquelle nous allons nous pencher est [Postman](https://www.postman.com/downloads/).
Elle permet de créer des requêtes très rapidement, de gérer et maintenir des collections en équipe et de créer des cas de test et scénarios.

Cette introduction prendra la forme de plusieurs chapitres constitués d'une page chacun et démontrant une notion ou un thème par l'exemple. Une collection et un environnement sont également téléchargeables et importables dans Postman afin que les explications puissent être suivies directement sur l'application de bureau.

L'API sur laquelle se basera cette introduction est l'API conseillée par Postman pour tester l'outil et sa documentation se trouve ici : https://postman-echo.com

## Pré-requis

- Avoir téléchargé [Postman](https://www.postman.com/downloads/)
- Notions basiques de Javascript pour l'écriture des tests
- Notions basiques du protocole HTTP
- Notions basiques des APIs RESTful et du cotenu JSON

## Chapitres

- [0 - Comment importer la collection et l'environnement de cette introduction](/chapitres/00-importer_collection_et_environnement.md)
- [1 - Requêtes et collections](/chapitres/01-requetes_et_collection.md)
- [2 - Variables et les environnements](/chapitres/02-variables_et_environnement.md)
- [3 - Les scripts et les tests (basique)](chapitres/03-basics-scripts_et_tests.md)
- [4 - Les scripts et les tests (intermédiaire)](chapitres/04-validation_json_schema.md)
- [5 - Les scripts et les tests (avancé)](chapitres/05-advanced-scripts_et_tests.md)

## À venir ?
- [6 - Le Runner]() ?
- [7 - Le travail collaboratif sur une collection]() ?
- [8 - Les possibilités d'intégration de postman dans un CI/CD et le monitoring]() ?
- [9 - Les serveurs mock ?]() ?
- [10 - La génération de documentation]() ?
- [11 - Proxy/intercepteurs ?]() ?
