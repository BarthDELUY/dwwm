# jQuery : Résumé des principales fonctionnalités

## 1. Sélection d'éléments

jQuery offre une manière simple et rapide de sélectionner des éléments du DOM en utilisant des sélecteurs CSS.

```javascript
$('selector');
```

La fonction **$** de jQuery est équivalent au document.querySelector() et au document.querySelectorAll() combinés : 

  * si elle ne trouve pas d'éléments, elle renvoie null
  * si elle trouve un seul élément, elle renvoie cet élément
  * si elle trouve plusieurs éléments, elle les renvoie tous dans un tableau