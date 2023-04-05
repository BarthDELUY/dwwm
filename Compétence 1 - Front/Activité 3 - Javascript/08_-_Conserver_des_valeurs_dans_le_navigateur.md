# Conserver des valeurs dans le navigateur

## Introduction

Lorsqu'un utilisateur navigue sur notre site/application, on souhaite parfois conserver des valeurs utilisables à plusieurs endroits de la page, voire sur plusieurs pages du site.

Lorsqu'on est sur la même page, on peut utiliser une très mauvaise pratique : les variables globales dans un script. Toutefois, c'est impossible à réaliser entre plusieurs pages, puisque les variables sont spécifiques à chaque page.

Il existe deux mécanismes qui vont nous permettre de nous passer des variables globales, que nous allons découvrir ensemble au cours de ce support.

## Sommaire

  1. Le localStorage
  2. Le sessionStorage


## 1. Le localStorage 🏫

#### 1.1 Présentation

Le local storage (ou stockage local en français) est un mécanisme de stockage de données dans le navigateur web d'un utilisateur. Il permet de stocker des informations sur l'ordinateur ou l'appareil mobile de l'utilisateur, de manière permanente ou temporaire, pour une utilisation ultérieure par une application web.  
Contrairement aux cookies, qui ont une taille limitée et sont envoyés au serveur avec chaque requête HTTP, le local storage permet de stocker de plus grandes quantités de données côté client et de les récupérer sans avoir à les envoyer au serveur. Cela peut permettre une meilleure performance de l'application, ainsi qu'une meilleure expérience utilisateur, en permettant par exemple de stocker des préférences de l'utilisateur ou des données de cache.  
Le local storage est une technologie largement utilisée dans le développement web moderne, en particulier pour les applications web progressives (PWA) et les sites web utilisant des frameworks JavaScript tels que React, Angular ou Vue.js.

Le localStorage est partagé entre tous les onglets du navigateurs qui affichent les pages d'un même site ; il est égaelemnt conservé sans limite de durée (on peut récupérer les valeurs même après redémarrage de l'ordinateur).


#### 1.2 Utilisation

#####  Pour mémoriser un élément

```js

localStorage.setItem('clé', valeur);
```
ATTENTION : la clé ET la valeur doivent être des chaînes de caractères : il faut bien penser à utiliser JSON.stringify() si on veut conserver des objets ou des tableaux.

Exemple : 
```js
let users = [ 'Maxime', 'Aurélien', 'Nabilla'];
localStorage.setItem('users', JSON.stringify(users));

```


##### Pour lire un élément

```js
let mavar = localStorage.getItem('clé');
```

ATTENTION : la clé est être une chaîne de caractères, et la valeur renvoyée également : il faut bien penser à utiliser JSON.parse() si on veut conserver des objets ou des tableaux.

Exemple : 

```js

let users = JSON.parse(localStorage.getItem('users'));
```


#####  Pour supprimer un élément
```js
localStorage.remove/Item('clé');
```

## 2. Le sessionStorage 🏫

#### 2.1 Présentation

Comme le localStorage, le sessionStorage permet de mémoriser des données dans une page.

Cependant, il a quelques différences avec le localStorage : 

  * Le sessionStorage est spécifique à l'onglet en cours : on ne peut pas partager des données entre deux onglets. La variable "sessionStorage" est "locale" à l'onglet.
  * comme le sessionStorage est local à l'onglet, il est vidé dès qu'on ferme l'onglet ou la page.

#### 2.2 Utilisation

#####  Pour mémoriser un élément

```js

sessionStorage.setItem('clé', valeur);
```
ATTENTION : la clé ET la valeur doivent être des chaînes de caractères : il faut bien penser à utiliser JSON.stringify() si on veut conserver des objets ou des tableaux.

Exemple : 
```js
let users = [ 'Maxime', 'Aurélien', 'Nabilla'];
sessionStorage.setItem('users', JSON.stringify(users));

```


##### Pour lire un élément

```js
let mavar = sessionStorage.getItem('clé');
```

ATTENTION : la clé est être une chaîne de caractères, et la valeur renvoyée également : il faut bien penser à utiliser JSON.parse() si on veut conserver des objets ou des tableaux.

Exemple : 

```js

let users = JSON.parse(sessionStorage.getItem('users'));
```


#####  Pour supprimer un élément
```js
sessionStorage.remove/Item('clé');
```