# Scripts et tests (avancé)
Pour ce chapitre, nous allons utiliser un endpoint très simple possible de l'API postman-echo :
`GET https://postman-echo.com/status/<code>` en modifiant le code HTTP demandé.
Nous testerons la réponse de l'API avec les critères suivants :

- le statut HTTP de la réponse doit être celui demandé lors de la requête
- le corps de la réponse doit contenir seulement un attribut `status` avec la valeur correspondante au code demandé dans la requête
- le temps de réponse ne doit pas être inférieur à 200ms pour toutes les requêtes sauf pour le statut 510 qui doit avoir un temps de réponse inférieur à 600ms)

## Implémentation du test basique

---

L'exemple fourni ainsi que les critères de test sont suffisamment simple : le test le sera donc aussi. Les trois critères du test seront conservés dans des constante déclarées au début du script et utilisés par la suite dans les tests :

```javascript
const requestedStatus = pm.variables.get('requestedStatus');
const maxResponseTime = 200;
const statusSchema = {
    "title": `GET Status Schema for status ${requestedStatus}`,
    "type": "object",
    "properties": {
        "status": {
            "type": "number",
            "minimum": requestedStatus,
            "maximum": requestedStatus,
        }
    },
    "additionalProperties": false,
    "required": [
        "status"
    ]
}

pm.test(`Status should be '${requestedStatus}'`, function () {
    pm.response.to.have.status(requestedStatus);
});

pm.test(`Response body should validate JSON Schema '${statusSchema.title}'`, function () {
    pm.response.to.have.jsonSchema(statusSchema);
});

pm.test(`Response time is less than ${maxResponseTime}ms`, function () {
    pm.expect(pm.response.responseTime).to.be.below(maxResponseTime);
});
```

Lançons la requête et vérifions que les résultats de test sont concluants :

![résultats de test 1](/images/chap.5/1-test_results_1.png)

Créons maintenant cinq autres requêtes, chacune testant un statut différent. Afin d'éviter de dupliquer le code du script de test, nous allons l'externaliser en **variable globale** afin de pouvoir le réutiliser dans **toute la collection**.

## Réutilisation de code (DRY)

---

Afin de réutiliser du code Javascript dans nos scripts de test, nous allons utiliser les **variables globales** car ce sont les seules qui permettent l'utilisation de la fonction javascript `eval()`. [En savoir plus sur la fonction `eval()`](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/eval)

Pour ce faire, ouvrons cette fois l'édition de la **collection** afin que la variable contenant le code javascript à exécuter soit disponible pour toutes les requêtes de la collection :

![collection edition](/images/chap.5/2-collection_edition.png)

Entrons le code suivant dans le script de pré-requête afin d'ajouter une fonction de test prenant deux paramètres en entrée et testant nos trois critères :

```javascript
postman.setGlobalVariable("testGetStatusResponse", (requestedStatus, maxResponseTime = 200) => {
    const statusSchema = {
        "title": `GET Status Schema for status ${requestedStatus}`,
        "type": "object",
        "properties": {
            "status": {
                "type": "number",
                "minimum": requestedStatus,
                "maximum": requestedStatus,
            }
        },
        "additionalProperties": false,
        "required": [
            "status"
        ]
    }

    pm.test(`Status should be '${requestedStatus}'`, function () {
        pm.response.to.have.status(requestedStatus);
    });

    pm.test(`Response body should validate JSON Schema '${statusSchema.title}'`, function () {
        pm.response.to.have.jsonSchema(statusSchema);
    });

    pm.test(`Response time is less than ${maxResponseTime}ms`, function () {
        pm.expect(pm.response.responseTime).to.be.below(maxResponseTime);
    });
});
```

Pour chaque requête GET status du chapitre 5, le script sera le même :

```javascript
const requestedStatus = pm.variables.get('requestedStatus');

// Dans le script de la requête pour le statut 510, on ajoute un second paramètre lors de l'appel à la fonction (i.e. eval(globals.testGetStatusResponse)(requestedStatus, 600))
eval(globals.testGetStatusResponse)(requestedStatus);
```

Si le modèle de retour de l'API `GET https://postman-echo.com/status/<code>` vient à changer, il n'y aura alors qu'un seul endroit où changer le schéma.

On peut bien entendu aller beaucoup plus loin dans la mutualisation des tests et implémenter des fonctions beaucoup plus dynamique comme par exemple une fonction de validation "générique" des schémas, prenant en paramètre le nom d'un schéma et allant récupérer le schéma à valider dans les variables d'environnement, et bien d'autres cas !

Voici pour illustration la dernière requête du dossier `Chapitre 5` de la collection `Introduction à Postman`, lancée et montrant les résultats de test dans le panel du bas :

![dernière reaquête chapitre 5](/images/chap.5/3-dry_1.png)

## À venir

---

Dans le prochain chapitre nous allons utiliser Runner Postman afin de lancer automatiquement l'ensemble des requêtes créées jusqu'à maintenant et voir succintement comment.