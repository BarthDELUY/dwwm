# La notation objet en Javascript

## Introduction

À l'origine, les créateurs du langage Javascript ont inventé les variables pour pouvoir mémoriser des informations lors d'un script.

Ensuite, ils ont inventé les tableaux, pour pouvoir conserver plusieurs valeurs d'un seul coup.

Ce mécanisme, bien que très pratique, s'est vite avéré limité : quand je souhaite conserver les différentes caractéristiques d'un élément, ai-je mis le nom en première ou en deuxième position ?

Pour résoudre ce nouveau problème sont apparus les objets.


## Sommaire

  1. Définition d'un objet 🏫
  2. La notation JSON 🏫
  3. Créer son propre type de variable : les classes 🏫


## Les objets 🏫

Un objet est donc une variable de type complexe, au sein de laquelle je vais pouvoir donner un nom à chacune des valeurs qu'elle contient. Un objet est donc une variable, contenant d'autres variables :-)

Pour accéder à ces sous-variables, on va utiliser le point '.'. 

Vous vous rendez compte que vous utilisez donc des objets depuis plusieurs jours : quand vous écrivez elt.innerHTML, vous accédez à la sous-variable innerHTML de l'objet elt !

De même, si vous utilisez element.sous-element.value, vous accédez à la valeur du sous-élément contenu dans element.

## La notation JSON 🏫

[JSON](https://json.org) signifie **J**ava**s**cript **O**bject **N**otation.

Il s'agit d'une façon très simple de déclarer des objets en Javascript. Tellement simple, en fait, que cette notation a été reprise dans la quasi-totalité des langages, et s'est imposée de fait comme la manière façon de décrire des données qui transitent entre le back et le front.

Quelques exemples : 
  * Une personne : 

```js
let barth = {
    name: "DELUY",
    firstname: "Barth",
    job: "Formateur JS"
};
```

  * Un livre :

```js
let mybook = {
    title: "Le meilleur de JS en 14 pages",
    ISBN: "147B-2541-3985",
    author: barth,
    price: 12.99
};
```

Il est donc possible d'accéder au titre du livre par **mybook.title**, et au nom de son auteur par **mybook.author.name**, tout simplement !

##### Résumé de la syntaxe JSON 🏫

Un objet est déclaré entre accolades; ses sous-variables, que l'on va appeler attributs ou propriétés, sont composés d'un identifiant, suivi d'un deux-points, suivi de leur valeur.  
La valeur d'un attribut peut être de n'importe quel type : nombre, string, booléen, tableau, et même un autre objet !

Exemple complexe : 

```js

let restaurant = {
    name: "Aux petits lilas roses",
    address: {
        number: 1,
        street: "Allée des poireaux",
        zipcode: "69007",
        city: "Lyon"
    },
    employees: [
        {
            name: "GUSTEAU Rémi",
            job: "Chef"
        },
        {
            name: "BOUCHARD Gérard",
            job: "Server"
        }
    ],
    menus: [
        {
            name: "Menu du jour",
            price: 14.99
        },
        {
            name: "Menu du Chef",
            price: 18.99
        }
    ]
    
};

```

On a ici un objet qui contient 4 attributs :
  * name : le nom du restaurant
  * address : l'adresse du restaurant, qui est elle-même un objet
  * employees : la liste (donc *un tableau*) des employés (qui sont eux-mêmes des objets)
  * menus : la liste (donc *un tableau*) des menus du restaurant, qui sont eux-mêmes des objets

C'est du code informatique, et pourtant, ça reste très facile à lire !


## Créer ses propres types : les classes 🏫

La syntaxe JSON est parfaite pour décrire de petits objets, mais si j'ai besoin de plusieurs objets qui suivent la même structure, il faut que je fasse attention à ne pas me tromper. Pareil, si je souhaite leur ajouter un attribut, je dois l'ajouter partout...

Les classes vont nous permettre de définir la structure de nos futurs objets. Les variables qui utiliseront cette classe (on va parler d'*instances*) partageront cette structure commune.

Les classes vont également nous permettre d'encapsuler (de contenir) des fonctions utiles seulement à cette classe, ou des fonctionnalités qu'elle veut proposer au monde extérieur.

Tout comme les fonctions, les classes doivent être déclarées ; elles doivent également être déclarées *avant* d'être utilisées.

#### Déclaration d'une classe 🏫

```js
class Person {
    name;
    firstname;
    birthdate;
}
```

#### Utilisation de la classe 🏫

```js

let barth = new Person();

barth.name = "DELUY";
barth.firstname = "Barth";

console.log(barth);
```

#### Le mot-clé this

Dans une classe, pour accéder aux attributs, il n'est pas possible d'utiliser le nom de la variable (puis qu'elle n'existe pas encore, on est en train de déclarer la classe).  
Pour cela, les langages objets nous proposent le mot-clé **this**.

```js
class Person {
    name: "DELUY";
    firstname: "Barth";
    fullname: this.name + this.firstname;
}
```

#### Encapsuler une fonction dans une classe 🏫

Il n'est pas possible d'afficher directement un objet : si on essaie, on obtiendra "[Object] object".  
Il est intéressant que notre objet propose une fonction permettant de l'afficher, comme nous le souhaitons.

En POO, ce genre de fonctions est généralement appelée *toString()*.  
Du point de vue vocabulaire, une fonction encapsulée (contenue) dans une classe est appelée une *méthode* de la classe.

```js
class Person {
    name;
    firstname;
    toString() {
        return this.firstname + " " + this.name;
    }
}
```

Pour l'appeler :

```js
let barth = new Person();
barth.name = "DELUY";
barth.firstname = "Barth";
console.log(barth.toString());
```

#### Le constructeur 🏫

Le constructeur d'une classe est une méthode spéciale nommée "constructor()", appelée automatiquement dès qu'on utilise le mot-clé **new**.  
On l'utilise généralement pour lui passer les valeurs à stocker dans les attributs de la classe, au lieu de les configurer un par un :

```js
class Person {
    name;
    firstname;
    toString() {
        return this.firstname + " " + this.name;
    }
    constructor( name, firstname) {
        this.name = name;
        this.firstname = firstname;
    }
}