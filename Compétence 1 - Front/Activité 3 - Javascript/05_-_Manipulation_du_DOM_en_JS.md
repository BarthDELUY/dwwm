# Manipulation du DOM en Javascript

## Introduction

Le DOM est la représentation "programmatique" des balises HTML que le navigateur a trouvées sur la page.  
Javascript nous permet d'interagir avec lui, pour :
  * accéder aux éléments (par exemple, aux valeurs des champs de formulaires)
  * modifier les éléments (changer leur style, leurs attributs, etc)
  * ajouter des éléments (rajouter des lignes dans un tableau, ...)
  * supprimer des éléments (supprimer une ligne dans un tableau, ...)

On peut utiliser ici l'acronyme CRUD (pour **C**reate, **R**ead, **U**pdate, **D**elete).

## Sommaire

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


## 3. Gérer les classes CSS d'un élément 🏫

### 3.1 Récupérer la liste des classes d'un élément 🏫

Il existe deux façons d'accéder à la liste des classes d'un élément :

  * `document.querySelector(...).className` qui renvoie la liste des classes sous forme d'une string (on obtient exactement la valeur qu'il y a dans l'attribut class="..." de l'élément)
  * `document.querySelector(...).classList` qui renvoie un tableau contenant les classes

Il est beaucoup plus simple de traiter classList que l'attribut className, on va donc se concentrer sur celui-là à partir de maintenant.

### 3.2 Ajouter une classe à un élément 🏫

```js
// On récupère l'élément
let elt = document.querySelector('#mon-id');
// On lui ajoute la classe "discount"
elt.classList.add("discount");
```

### 3.3 Supprimer une classe d'un élément 🏫

```js
// On récupère l'élément
let elt = document.querySelector('#mon-id');
// On lui retire la classe "discount"
elt.classList.remove("discount");
```

### 3.4 Toggle une classe d'un élément 🏫

```js
// On récupère l'élément
let elt = document.querySelector('#mon-id');
// On lui bascule la classe "discount"
elt.classList.toggle("discount");
```

## 4. Gérer les attributs d'un élément 🏫

### 4.1 Récupérer la valeur d'un attribut d'un élément 🏫

```js
// On récupère l'élément (ici, un champ de formulaire de type "number")
let elt = document.querySelector('input[type=number]#age');
// On récupère la valeur de son attribut "min"
let min_value = elt.getAttribute('min');
```

### 4.2 Ajouter/modifier la valeur d'un attribut d'un élément 🏫

```js
// On récupère l'élément (ici, un champ de formulaire de type "number")
let elt = document.querySelector('input[type=number]#age');
// On modifie de son attribut "min"
elt.setAttribute('min', 4);
```

### 4.3 Supprimer un attribut d'un élément 🏫

```js
// On récupère l'élément (ici, un champ de formulaire de type "number")
let elt = document.querySelector('input[type=number]#age');
// On modifie de son attribut "min"
elt.removeAttribute('min', 4);
```

## 5. Accéder à la valeur d'un champ de formulaire 🏫

```js
// On récupère l'élément (ici, un champ de formulaire de type "number")
let elt = document.querySelector('input[type=number]#age');
// On récupère sa valeur
let ma_valeur = elt.value;
// On change sa valeur
elt.value = 18;
```

## 6. Modifier le contenu d'un élément 🏫

En Javascript, le contenu HTML d'un élément est disponible dans sa propriété 'innerHTML'.
Il suffit de la remplacer pour modifier son contenu : 

```html
<p id="mon_paragraphe">
    Bonjour, vous devez choisir un nombre entre <span id="valeur_min">0</span>
    et <span id="valeur_min">0</span>.
</p>
<p id="p2"></p>
```

```js
// On récupère l'élément
let elt = document.querySelector('#valeur_min');
// On peut récupérer son contenu HTML dans une variable si nécessaire
let old_html = elt.innerHTML;
// On remplace son contenu
elt.innerHTML = "5";

// On récupère le deuxième paragraphe : 
let p2 = document.querySelector('p2');
// On le remplit avec plusieurs éléments HTML
p2.innerHTML = '<h1>Titre</h1><span style="color: red">ATTENTION</span> La boîte va bientôt fermer !';
```

Chaque modification de l'innerHTML d'un élément entraine une relecture et une reconstruction du DOM : le code HTML sera interprété.

## 7. Créer un nouvel élément 🏫

```js
// On crée l'élément
let elt = document.createElement('p');
elt.innerHTML = '<h1>Titre</h1><span style="color: red">ATTENTION</span> La boîte va bientôt fermer !';
elt.classList.add("discount");
```

**⚠ ATTENTION ⚠**  L'élément que l'on vient de créer est pour l'instant isolé de la page ! Si on écrase la variable "elt", on perd cet élément.

## 8. Attacher un élément à la page

### 8.1 Insérer l'élément à la fin d'un élément parent (un container par exemple) 🏫
```html
<section id="mes-articles">
    <p id="mon_paragraphe">
        Bonjour, vous devez choisir un nombre entre <span id="valeur_min">0</span>
        et <span id="valeur_min">0</span>.
    </p>
    <p id="p2"></p>
</section>
```
```js
// On crée l'élément
let new_p = document.createElement('p');
new_p.setAttribute('id', 'mon-nouveau-paragraphe');
new_p.innerHTML = '<h1>Titre</h1><span style="color: red">ATTENTION</span> La boîte va bientôt fermer !';
new_p.classList.add("discount");

// On récupère son élément parent
let elt_parent = document.querySelector("#mes-articles");
// On le rattache à son élément parent, à la fin de l'élément
elt_parent.appendChild(new_p);

```

### 8.2 Insérer l'élément au début d'un élément parent (un container par exemple) 🏫
```html
<section id="mes-articles">
    <p id="mon_paragraphe">
        Bonjour, vous devez choisir un nombre entre <span id="valeur_min">0</span>
        et <span id="valeur_min">0</span>.
    </p>
    <p id="p2"></p>
</section>
```
```js
// On crée l'élément
let new_p = document.createElement('p');
new_p.setAttribute('id', 'mon-nouveau-paragraphe');
new_p.innerHTML = '<h1>Titre</h1><span style="color: red">ATTENTION</span> La boîte va bientôt fermer !';
new_p.classList.add("discount");

// On récupère son élément parent
let elt_parent = document.querySelector("#mes-articles");
// On le rattache à son élément parent, à la fin de l'élément
elt_parent.prependChild(new_p);

```

### 8.3 Insertion positionnée d'un nouvel élément ✨

Pour insérer un élément à un emplacement spécifiquer, il faudra utiliser soit `insertBefore()` [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/insertBefore), `insertAfter()` [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Node/insertAfter), ou `insertAdjacentElement()` [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentElement).

## 9. Supprimer un élément du DOM 🏫

Pour supprimer un élément du DOM, il faut : 
  * accéder à son élément parent
  * récupérer l'élément à supprimer
  * le supprimer de la liste des éléments enfants du parent

Exemple : 
```html
<section id="mes-articles">
    <p id="mon_paragraphe">
        Bonjour, vous devez choisir un nombre entre <span id="valeur_min">0</span>
        et <span id="valeur_min">0</span>.
    </p>
    <p id="p2" class="to-delete"></p>
</section>
```
```js

// On récupère son élément parent
let elt_parent = document.querySelector("#mes-articles");
// On va chercher l'élément à supprimer
let elt_todelete = document.querySelector(".to-delete");
// La fonction removeChild détache l'élément du DOM et le renvoie, pour ne pas le perdre au cas où
let deleted_elt = elt_parent.removeChild(elt_todelete);

```
