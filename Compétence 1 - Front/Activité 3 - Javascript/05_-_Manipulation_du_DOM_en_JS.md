# Manipulation du DOM en Javascript

## Introduction

Le DOM est la représentation "programmatique" des balises HTML que le navigateur a trouvées sur la page.  
Javascript nous permet d'interagir avec lui, pour :
  * accéder aux éléments (par exemple, aux valeurs des champs de formulaires)
  * modifier les éléments (changer leur style, leurs attributs, etc)
  * ajouter des éléments (rajouter des lignes dans un tableau, ...)
  * supprimer des éléments (supprimer une ligne dans un tableau, ...)

On peut utiliser ici l'acronyme CRUD (pour **C**reate, **R**ead, **U**pdate, **D**elete).

## Sommaire ##

  1. [Accéder à un seul élément du DOM](#access-single-element)
  2. [Accéder à un ensemble d'éléments du DOM](#access-multiple-elements)
  3. Gérer les classes CSS d'un élément
  4. Gérer les attributs d'un élément
  5. Accéder à la valeur d'un champ de formulaire
  6. Modifier le contenu d'un élément
  7. Créer un nouvel élément
  8. Rattacher un nouvel élément au DOM
  9. Supprimer un élément du DOM

## 1. Accéder à un élément du DOM {#access-single-element}

### 1.1 Méthode générique 🏫

Pour accéder à un élément du DOM, on va utiliser la fonction `document.querySelector("mon sélecteur CSS")`. ([MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector))

"mon sélecteur CSS" correspond à un sélecteur CSS que vous utiliseriez dans un fichier .css pour définir du style (# pour l'id, . pour les classes, etc).

**⚠ ATTENTION ⚠**  La fonction document.querySelector() ne renvoie toujours que *null* (si aucun élément ne correspond au sélecteur CSS) ou UN élément. Si plusieurs éléments sont capturés par le sélecteur, elle renvoie uniquement le *premier* trouvé.

Exemples :

```html
<body>
    <p id="mon-paragraphe" class="discount">Mon premier paragraphe</p>
    <p id="mon-deuxieme-paragraphe" class="discount"><h2>Mon deuxième paragraphe</h2></p>
    <p id="mon-troisieme-paragraphe"><a href="#">Cliquez ici !</a></p>
</body>
```

```js
// Je récupère un paragraphe par son ID
let second_paragraphe = document.querySelector('#mon-deuxieme-paragraphe');

// Je récupère le premier élément qui a la classe "discount"
let first_discount = document.querySelector('.discount');

// Je récupère le premier a qui se trouve dans un p
let first_a = document.querySelector('p a');

// Je récupère le premier h2 du 2ème enfant de body
let first_h2_second_child = document.querySelector('body > *:nth-child(2) h2');
```

### 1.2 Méthode spécifique par ID ✨

Avant l'introduction du `document.querySelector()` en 2008, et le temps de son adoption par les navigateurs, il fallait utiliser la fonction `document.getElementById('mon id ici')` pour chercher un élément en particulier. Cela obligeait donc à mettre un ID sur tous les éléments que l'on souhaitait manipuler par JS.

**⚠ ATTENTION ⚠** Par rapport au querySelector qui attend un sélecteur CSS (et donc avec un '#' si on recherche par id), la méthode document.getElementById n'attend que l'id en paramètre.

Exemples : 

```html
<body>
    <p id="mon-paragraphe" class="discount">Mon premier paragraphe</p>
    <p id="mon-deuxieme-paragraphe" class="discount"><h2>Mon deuxième paragraphe</h2></p>
    <p id="mon-troisieme-paragraphe"><a href="#">Cliquez ici !</a></p>
</body>
```

```js
let first_p = document.getElementById('mon-paragraphe');

//⚠ ATTENTION ⚠ NE PAS UTILISER, SyntaxError
let second_p = document.getElementById('#mon-second-paragraphe');
// L'erreur ici est d'utiliser le #, il ne faut pas le mettre avec getElementById
```

## 2. Accéder à un ensemble d'éléments du DOM {#access-multiple-elements}

### 2.1 Méthode générique 🏫

La fonction document.querySelector() a une grande soeur, `document.querySelectorAll(...)` qui renvoie la liste complète des éléments respectant le filtre fourni en paramètres.

**⚠ ATTENTION ⚠**  La fonction document.querySelectorAll() renvoie **toujours** une liste. Cette liste est vide si querySelectorAll() n'a trouvé aucun élément, un seul élément si querySelectorAll() n'a trouvé qu'un seul élément (il faudra donc utiliser [0] à un moment ou à un autre pour accéder à cet élément), ou un tableau de plusieurs éléments.

🛈 INFORMATION 🛈 Utiliser querySelectorAll() en lui fournissant un id d'élément en paramètre est assez stupide, ça rajoute une couche de tableau alors que querySelector() est fait pour ça !

Exemples : 

```html
<body>
    <p id="mon-paragraphe" class="discount">Mon premier paragraphe</p>
    <p id="mon-deuxieme-paragraphe" class="discount"><h2>Mon deuxième paragraphe</h2></p>
    <p id="mon-troisieme-paragraphe"><a href="#">Cliquez ici !</a></p>
</body>
```

```js
// Je récupère tous les paragraphes de la page
let all_p = document.querySelectorAll('p');
console.log(all_p.length);

// Je récupère tous les paragraphes qui ont la classe CSS "discount"
let discount_p = document.querySelectorAll('p.discount');
console.log(discount_p);
```

### 2.2 Méthode spécifique par tag ✨

Pour une recherche par tag, on peut utiliser `document.getElementsByTagName('mon tag ici')`, qui est un synonyme de `document.querySelectorAll('mon_tag')`

Exemple : 

```js
// Je récupère tous les paragraphes
let all_p = document.getElementsByTagName('p');
```

### 2.3 Méthode spécifique par classe CSS ✨

Pour une recherche par classe, on peut utiliser `document.getElementsByClassName('ma_classe')`, qui est un synonyme de `document.querySelectorAll('.ma_classe')`

**⚠ ATTENTION ⚠** Par rapport au querySelectorAll qui attend un sélecteur CSS (et donc avec un '.' si on recherche par classe), la méthode document.getElementsByClassName() n'attend que le nom de la classe en paramètre.

Exemple : 

```js
// Je récupère tous les paragraphes
let all_p = document.getElementsByTagName('p');
```

### 2.4 Méthode spécifique par attribut "name" ✨

Pour une recherche par attribut "name", on peut utiliser `document.getElementsByName('le_nom')`, qui est un synonyme de `document.querySelectorAll('*[name=le_nom]')`

**⚠ ATTENTION ⚠** Par rapport au querySelectorAll qui attend un sélecteur CSS (et donc avec un '.' si on recherche par classe), la méthode document.getElementsByClassName() n'attend que le nom de la classe en paramètre.

Exemple : 

```html
<form>
    <input type="radio" value="bleu" name="color" id="color-bleu" />
    <label for="color-bleu">Bleu</label>
    <input type="radio" value="rouge" name="color" id="color-rouge" />
    <label for="color-rouge">Rouge</label>
    <input type="radio" value="jaune" name="color" id="color-jaune" />
    <label for="color-jaune">Jaune</label>
```

```js
// Je récupère tous les boutons radio sur la couleur
let all_color = document.getElementsByName('color');
```
