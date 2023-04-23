# Les modules en Javascript

## Introduction

Avec le temps, Javascript est passé de petites interactions avec l'utilisateur sur la page à des applications complètes en SPA, sans parler de NodeJS.

Il devenait de plus en plus complexe d'organiser correctement ses scripts, sans passer par des outils tiers comme require.js ou webpack.

ES6 a donc implémenté la notion de modules, similaires aux packages Java ou aux namespaces de PHP.

**Tous** les frameworks front reposent aujourd'hui sur ce concept de modules.

## Sommaire

  1. Notions théoriques 🏫
  2. Export 🏫
  3. Import 🏫

## 1. Notions théoriques 🏫

Les deux principales différences entre un module et un script classique sont :
  
  * la "portée" du contenu du module : par défaut, tout le code contenu dans un module est caché au reste du programme, tant que le développeur ne choisit pas explicitement de le rendre visible (et donc utilisable)
  * la façon dont le code va être inclus dans la page web

Un module est un fichier JS, pouvant comporter des variables, des fonctions, une classe, etc.

La recommandation actuelle est de lui donner l'extension .js, comme pour les fichiers javascript standards.

Un module utilisera toulours le *mode strict* de JS.

## 2. Export 🏫

Par défaut, tout le code contenu dans un module est invisible au reste du programme.

Le développeur choisit les éléments qu'il rend visible au reste de la page, en utilisant le mot-clé **export**.

Exemple : 

  * Fichier UserAccount.func.js

```js

function convertUserAccountsToHTML(userAccounts)
{
    let table = document.createElement("table");
    table.appendChild(getUserAccountsHeaders(userAccounts));
    let i = 0;
    let tbody = document.createElement("tbody");
    while (i < userAccounts.length) {
        tbody.appendChild(convertUserAccountToHTML(userAccounts[i]));
    }
    table.appendChild(tbody);
    return table;
}

function getUserAccountsHeaders(userAccounts)
{
    let thead = document.createElement("thead");
    /// Bloc de code
    ///
    ///
    return thead;
}

function convertUserAccountToHTML(userAccount)
{
    let tr = document.createElement("tr");
    /// Bloc de code
    ///
    ///
    return tr;
}

// Le reste du programme n'a pas besoin de connaître les fonctions "getUserAccountsHeaders" et "convertUserAccountToHTML"
// En tant que développeur, je choisis de ne rendre visible que la fonction "utile" de conversion :
export { convertUserAccountsToHTML };

```

Ce mécanisme permet de "cacher" le découpage interne du code : le programme ne connait que les fonctions qui lui sont effectivement utiles.

Attention, il n'est possible d'exporter que des éléments situés au niveau "global" (*top-level*) du module, c'est-à-dire situés en dehors de tout bloc de code (il n'est pas possible d'exporter une variable locale à une fonction, ou juste une méthode ou un attribut d'une classe).

## 3. Import 🏫

À l'inverse, pour pouvoir utiliser du code situé dans un module, il va falloir l'importer là où on va en avoir besoin grâce à l'instruction **import**.  
Les imports sont par convention déclarés en début de fichier, à la place *"use strict";*

Syntaxe : 

```js
// import { élément1, élément2, ... } from 'chemin';
// Le chemin DOIT commencer soit par un / (et désigne la racine du site), soit par un '.', soit par '..'
import { convertUserAccountsToHTML } from './modules/UserAccount.func.js';

```

Une fois l'import déclaré, l'élément importé (variable, constante, fonction, classe) devient accessible comme si il avait été déclaré dans le fichier en cours.

Attention : il n'est possible d'utiliser l'instruction **import** que dans un module : à partir du moment où vous commencez à utiliser des modules, tout votre code va devenir module :

```html

<script type="module" src="index.js"></script>

```


