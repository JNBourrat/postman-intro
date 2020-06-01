# Requêtes et Collections

## Qu'est-ce qu'une requête dans Postman ?

Une requête dans Postman n'est rien d'autre qu'une requête HTTP classique. Pour initier la création d'une requête, il suffit de cliquer sur le symbole '+' en haut de l'écran, comme pour créer un nouvel onglet :
![creation-requete.png](/images/chap.1/1-creation-requete.png)
Afin de paramétrer cette requête, différentes informations doivent être rentrées :

1. La méthode HTTP est à sélectionner dans la liste déroulante. Pour l'exemple, nous laisserons la méthode `GET`

![creation-requete.png](/images/chap.1/2-methode-http.png)

2. L'url est à insérer dans la barre d'adresse. Ici nous allons choisir de faire une requête sur l'API de postman `GET https://postman-echo.com/get`

3. Les paramètres de requêtes peuvent être ajoutés directement via l'onglet 'Params'. Ils s'ajouteront directement à l'url s'ils sont cochés comme on peut le voir dans la capture d'écran ci-dessous.

![send-request.png](/images/chap.1/3-send-request.png)

Si on "envoie" cette très simple requête grâce au bouton "Send" à droite de la barre d'adresse, nous pouvons alors avoir accès à nombre d'informations dans le panneau en bas de l'écran : le body de la réponse, le temps de réponse, la taille, les cookies, les headers de réponse.

D'après la documentation de l'API, la body de la réponse doit contenir les paramètres de requête dans l'objet `args`, les headers et l'url de la requête envoyée lors du clic sur le bouton `Send`.

Sans s'en apercevoir, en cliquant sur ce bouton `Send`, nous avons déclenché -entre autres choses- l'évaluation d'un script de Pré-requête et d'un script de Test. Ces scripts sont codés en Javascript et accompagnent chaque requête Postman suivant le diagramme suivant :

![req-resp.png](/images/chap.1/4-req-resp.png)

Nous ne nous pencherons pas sur le sujet de ces scripts, qui arriveront dans le chapitre 3 mais il est important de noter leur existence.

Afin d'enregistrer cette première requête on peut cliquer sur le bouton "Save", il faudra cependant créer ce qu'on appelle une "Collection" en cliquant sur le bouton `+ Create Collection`.

![save-request.png](/images/chap.1/5-save-request.png)

## Qu'est-ce qu'une collection dans Postman ?

Une collection dans Postman est une façon de regrouper les requêtes en un ensemble pouvant être facilement partagé et organisé.
Les requêtes peuvent être ensuite regroupées en sous-dossier dans la collection comme dans l'exemple ci-dessous.

![premiere-collection.png](/images/chap.1/6-premiere-collection.png)

Il existe deux types de collections :

- Les collections dédiées au test d'API. Ces collections sont destinées en général aux développeurs et aux testeurs afin des s'assurer du bon fonctionnement. Elles exploitent les capacités suivantes du logiciel :
  - Les scripts (de test et de pré-requête)
  - Le runner et l'automatisation de scénarios
  - Le logging des informations de requête (notamment utile pour débugger lors d'erreurs)
  
- Les collections dédiées à la documentation. Ces collections sont utilisées afin de communiquer le fonctionnement d'une API avec des exemples de réponses, d'erreur et des descriptions compréhensibles par les utilisateurs potentiels de l'API

Dans cette introduction, nous allons nous pencher sur le premier type de collection, celui destiné au test et au développement d'API.

L'exemple pour ce premier chapitre est très basique afin de comprendre la base d'une requête dans Postman. L'exemple s'étoffera au fur et à mesure de cette introduction avec par exemple des `Path parameters`, des méthodes HTTP différentes, l'ajout de headers, etc.
Dans le prochain chapitre nous parlerons des [variables et des environnements](02-variables_et_environnement.md).
