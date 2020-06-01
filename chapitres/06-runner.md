# Lancer les collections de façon automatisée


Nous avons déjà vu qu'une **collection** dans Postman n'était rien d'autre qu'un regroupement de requête pouvant être lancées dans un environnement particulier.

Il est possible de lancer **toutes les requêtes** d'une collection l'une après l'autre (ou selon un agencement pré-déterminé) de façon automatisée grâce à trois outils différents :

- le Runner de l'application de bureau Postman
- l'interface de ligne de commande [Newman](https://learning.postman.com/docs/postman/collection-runs/command-line-integration-with-newman/)
- le [monitoring](https://learning.postman.com/docs/postman/monitors/intro-monitors/)

Ceci couplé à l'écriture de scripts nous permet alors de créer des suites de tests, passer des données entre plusieurs requêtes API et construire des scénarios reflétant la véritable utilisation de notre API.

## **Utilisation du Runner**

---

### **Avant de lancer le runner**

Avant de lancer le runner nous allons ouvrir la console Postman grâce au bouton en bas à gauche de l'écran :

![bouton console postman](/images/chap.6/0-console.png)

Les requêtes et les `console.log()` des scripts se loggueront dans la fenêtre qui vient de s'ouvrir.

### **Lancer le runner**

Le runner de Postman permet de lancer un ensemble de requêtes en série et de visualiser les résultats des tests qui leur sont associés.

Afin de lancer le runner, il suffit de cliquer sur le bouton `Runner` en haut à gauche de la fenêtre.
 ![bouton du runner](/images/chap.6/1-Runner-button2.png)

Une nouvelle fenêtre de dialogue s'ouvre alors. Cette première fenêtre présente les paramètres du Runner disponibles. Suivons les instructions suivantes afin de configurer le runner :

- Sélectionner la collection `Introduction à Postman` en cliquant dessus dans la partie de gauche
  - Toutes les requêtes de la collection devraient alors s'afficher sur la droite de la fenêtre
- Sélectionner l'environnement [Env A] Postman Echo téléchargé sur le repo
- Cocher la case `Save responses`

![fenêtre de réglage du runner](/images/chap.6/2-reglages_runner.png)

Avant de cliquer sur le bouton permettant de lancer le runner, observons la partie gauche de la fenêtre de réglage.
L'**ordre par défaut** est l'ordre dans lequel sont déclarées les requêtes dans la collection. Dans cette fenêtre, cela veut dire que les requêtes s'éffectueront l'une après l'autre depuis le haut vers le bas comme l'indique la flèche rouge :

![ordre requetes](/images/chap.6/3-ordre_requetes.png)

Cependant, on peut observer un changement dans l'ordre des trois dernières requêtes. En effet, leurs scripts contiennent des appels à la fonction `postman.setNextRequest(<nom-de-la-prochaine-requete>)` qui ne sont utiles que dans le cadre de l'automatisation des requêtes. Des `console.log()` ont également été placés dans les scripts afin de logguer ce qui y est demandé.

Appuyons maintenant sur le bouton bleu `Run Introduction ...` afin de lancer le Runner sur toute la collection et dans l'environnement sélectionné.

Les requêtes devraient alors se lancer une à une et leurs tests exécuté si elles en ont. Un résumé s'affichera à la fin du Run :

![résumé run](/images/chap.6/4-resume_run.png)

En consultant la console, on peut s'apercevoir que les trois derniers logs sont les suivants :

```json
Log depuis la requête 1 du chapitre 6 ==> Antépénultième requête en mode automatique
Calling postman.setNextRequest('3 - Avant-dernière requête du runner')
------------------------
Log depuis la requête 3 du chapitre 6  ==> Avant-dernière requête en mode automatique
Calling postman.setNextRequest('2 - Dernière requête du runner')
------------------------
Log depuis la requête 2 du chapitre 6 ==> Dernière requête du runner
Calling postman.setNextRequest(null)
```

Le script de test de la requête 1 a programmé la requête 3 pour être la requête suivante grâce à la ligne `postman.setNextRequest('3 - Avant-dernière requête du runner');`.

Le script de test de la requête 3 a programmé la requête 2 pour être la requête suivante grâce à la ligne `postman.setNextRequest('2 - Dernière requête du runner');`.

Le script de test de la requête 2 a programmé `null` pour être la requête suivante grâce à la ligne `postman.setNextRequest(null)`, ce qui a eu pour effet d'arrêter le runner.

> Note : grâce à la fonction `postman.setNextRequest(<nom-de-la-prochaine-requête>)` on peut donc boucler sur la même requête, si on veut la jouer plusieurs fois d'affilées avec des jeux de données différents par exemple. Une méthode simple est d'initier un compteur en variable d'environnement temporaire et de l'incrémenter à chaque passage dans le test.

### **Débugger grâce aux résultats du runner**

On s'aperçoit dans notre exemple qu'un test est en rouge : cela signifie bien entendu qu'il a échoué.
![requete échouée](/images/chap.6/6-failing_test.png)
Certaines données sont conservées et sont encore accessibles après la fin du run. Pour y accéder, il suffit de faire un clic gauche sur le nom de la requête. S'ouvre alors un popup permettant d'accéder au body de la requête, à l'URL, aux headers, etc.

![failing test 2](/images/chap.6/7-failing_test_2.png)
