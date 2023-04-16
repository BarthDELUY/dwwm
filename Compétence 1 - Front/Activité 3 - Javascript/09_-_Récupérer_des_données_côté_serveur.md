# Récupérer des données côté serveur

## Introduction

À l'origine, développer un site web consistait à développer un ensemble de pages reliées entre elles par des `<a>`, mais plus ou moins indépendantes.  
Le côté serveur s'occupait de la cohérence et de la session utilisateur, ainsi que de générer le code HTML à la volée : on parle de développement web monolithique.

Avec le développement du web haut débit et des technologies, les métiers de développeur front et développeur back se sont peu à peu éloignés, notamment avec l'invention de l'Ajax, puis de la HistoryAPI qui a entrainé l'apparition des SPA (*Single Page Application*). Le front et le back sont maintenant totalement indépendants l'un de l'autre, mais communiquent à chaque action de l'utilisateur: on parle désormais de "mode API". Le back va offrir des "endpoints" que le front va interroger pour interagir avec les données stockées côté serveur.

L'utilisateur va donc charger la totalité du squelette du front d'un seul coup, puis le garder en cache dans son navigateur.  
Javascript va ensuite s'occuper de charger seulement le contenu de la page depuis le back, au format JSON, et l'injecter dans la page.

Pour cela, il est nécessaire que Javascript propose un mécanisme permettant d'émettre des requêtes HTTP et de traiter le contenu de la réponse du serveur.

## Sommaire

  1. Ajax et XHR
  2. La fetch API
  3. Concept : comment traiter des données récupérées côté serveur ?

## 1. Ajax et XHR

#### Ajax

Ajax signifie *Asynchronous Javascript and XML*.  
Ce mécanisme, introduit à la fin des années 1990, permet d'envoyer une requête asynchrone côté serveur, et de traiter le résultat au moment où il arrive.

Initialement, il était prévu que le retour soit formaté en XML ; cependant, ce langage est trop verbeux et trop lourd par rapport aux données à transférer, et la plupart des librairies de l'époque se sont basées sur JSON, beaucoup plus léger et simple à comprendre.

#### XHR

Le mécanisme XHR était le mécanisme implémenté dans les navigateurs, pour émettre une requête vers le serveur, sans avoir à changer de page.

Problème : chaque navigateur implémentait son propre mécanisme, qui ne fonctionnait pas de la même façon.

Il était donc indispensable d'utiliser une librairie comme jQuery ou Prototype ou Script.aculo.us pour "gommer" ces différences et pouvoir travailler efficacement.

Le mécanisme XHR reposait sur des callbacks : à chaque changement d'état de la requête et de la réponse, on pouvait rattacher une fonction à exécuter, un peu comme les addEventListener.

## 2. La fetch API

Le W3C a donc proposé en 2015 un mécanisme uniforme, la [fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch), toujours en évolution aujourd'hui (la dernière release date du 23 mars 2023).

Ce mécanisme ne se base plus sur les callbacks, mais sur le mécanisme de la programmation asynchrone et des Promesses (dont la manipulation dépasse le cadre de la formation DWWM).

#### Exemple de Fetch

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <article id="cat-fact"></article>
    <script>
        // Au chargement de la page, on va chercher un cat fact random pour l'afficher
window.addEventListener('load', (e) => {
    let url = 'https://cat-fact.herokuapp.com/facts/random';
    fetch(url)
    .then((response) => { // Code appelé quand le navigateur reçoit la réponse
        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }
        return response.json();
    })
    .then((json) => document.querySelector('#cat-fact').innerHTML = json.text) // Code appelé si la réponse est OK
    .catch((err) => console.error(`Fetch problem: ${err.message}`));

});


    </script>
</body>
</html>
```

## 3. Concept : comment traiter des données récupérées côté serveur ?

Dans la "vie réelle" de votre application (c'est-à-dire la phase d'*exploitation* de l'application), les échanges entre client et serveur vont être constants : soumission d'un formulaire, changement de page dans un catalogue, tri de données (affichage par prix croissant, par nom, etc), les cas d'utilisation ne manquent pas.

Lorsque le front va récupérer des données côté serveur (requête GET), il va recevoir une réponse au format JSON, contenant les données demandées.

Il convient alors de procéder de façon logique pour les traiter.

Tout d'abord, il faut se demander : quel est le type d'information que je récupère depuis le back ?

  * est-ce un tableau (le json commence par un **[**) ? => il va falloir le parcourir pour récupérer les valeurs et les traiter une par une
  * est-ce un objet (le json commence par **{**) ? => il est possible d'accéder directement à ses propriétés, parfait !
  * est-ce une donnée primitive (number, string, boolean, etc) ? => il est possible de les traiter directement.

Dans tous les cas, le code de traitement doit se trouver soit dans une fonction (*et c'est le meilleur endroit*), soit dans la partie "// Code appelé si la réponse est OK" du paragraphe précédent.