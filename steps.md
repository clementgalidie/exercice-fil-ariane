# Fiche 00X
## Créer un fil d'ariane accessible, maintenable et en full CSS.

Principes abordés : accessibilité, interopérabilité, maintenabilité, performance.

### Acte 1
Vous avez pour consigne de créer un fil d'ariane pour un site internet. Seulement, comme pour la plupart des projets que vous devez mener, vous êtes tributaire de certaines contraintes. Pour ce petit exercice, les voici :
* Votre code HTML doit être valide (et le CSS aussi si vous le pouvez).
* Vous ne devez pas utiliser une seule image.
* Vous ne devez pas utiliser de JavaScript.
* Il doit être possible d'utiliser votre fil d'ariane avec un clavier (navigatio via la touche **TAB** par exemple).
* Votre fil d'ariane doit fonctionner sur la plupart des navigateurs récents. Vis-à-vis d'Internet Explorer, il doit être fonctionnel sur :
    * Internet Explorer 8 ;
    * Internet Explorer 9 ;
    * Internet Explorer 10 ;
    * Internet Explorer 11.
* Vous devez mettre au point une version responsive (potable).

> Comment s'y prendre pour obtenir un rendu assez rapidement prenant en compte chacune de ces contraintes ?

### Acte 2
Tout d'abord, commencons par regarder un petit aperçu de ce que vous voulons obtenir. 
![](http://clement-galidie.fr/github/html-css/exercice-fil-ariane/fil-ariane-resultat.jpg)
Nous avons donc un « menu » composé de cinq liens. Il y a également deux formes triangulaires aux deux extrémités de chaque liens. 

Premièrement, nous allons poser la base : le code __HTML__.
```html
<!DOCTYPE html>
<html lang="fr" dir="ltr">
<head>
  <meta charset="UTF-8">
  <title>Fiche 00X - fil d'Ariane</title>
  <link rel="stylesheet" href="assets/css/styles.css">
</head>
<body>
    <div class="page">

      <nav class="page-nav" role="navigation">
        <ul class="menu">
            <li class="menu-item"><a href="" class="menu-link">item 1</a></li>
            <li class="menu-item"><a href="" class="menu-link">item 2</a></li>
            <li class="menu-item"><a href="" class="menu-link">item 3</a></li>
            <li class="menu-item"><a href="" class="menu-link">item 4</a></li>
            <li class="menu-item menu-item--last"><a href="" class="menu-link">item 5</a></li>
        </ul>
      </nav>
    </div>
</body>
</html>
```
__NB :__ j'utilise la syntaxe [BEM](https://bem.info/) (sans l'écriture de base que je ne trouve absolument pas pratique).

__Internet Explorer 8__ ne supportant pas les nouvelles balises introduites via __HTML5__, nous devons utiliser le script [HTML5 Shiv](https://github.com/aFarkas/html5shiv) pour pallier ce « souci ». Pour l'installer, suivez simplement les instructions du __README__ du lien ci-dessus. Je l'ai inséré comme ceci dans mon fichier __HTML__ : 
```html
<!--[if lt IE 9]>
  <script src="assets/js/html5shiv.min.js"></script>
<![endif]-->
```
Le commentaire conditionnel
```html
<!--[if lt IE 9]><![endif]-->
```
permet de ne cibler que les versions  __strictement inférieures à Internet Explorer 9__.

### Acte 3
Les styles __CSS__ !

Commençons par supprimer les marges, positionner nos `<li>` côtes-à-côtes, et styliser un minimum nos liens.

```css
body {margin: 0;}

.page {
  width: 60em;
  margin-right: auto;
  margin-left: auto;
}

.menu {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

.menu-item {
  display: inline-block;
  min-width: 9.375em;
  min-height: 2.5em;
  line-height: 2.5em;
  margin-right: 3em;
  background-color: #444;
}

.menu-item--last {margin-right: 0;}

.menu-link {
  position: relative;
  display: block;
  font-size: 1.2em;
  color: #fff;
  text-decoration: none;
  text-align: center;
}
```

__NB :__ à noter qu'il y a un « souci » de __white-space__ avec `inline-block`. Dans notre cas, je ne corrige pas ce « souci » car je trouve qu'il ne pose pas de souci étant donné que nous voulons que nos éléments – `<li>` – soient espacés. Cependant, je vous suggère de lire [cet article](http://www.alsacreations.com/astuce/lire/1432-display-inline-block-espaces-indesirables.html) par exemple.

### Acte 4
La création des flèches __(sans image)__ !

À l'aide des __pseudo-elements__ [:before](http://mzl.la/1yWu8iq) et [:after](http://mzl.la/1JvICZM), et de la [technique](http://css-tricks.com/snippets/css/css-triangle/) permettant de créer des triangles en __CSS__ (en jouant avec les bordures de nos éléments), nous pouvons créer nos flèches très facilement.

```css
.menu-link:before {
  content: "";
  position: absolute;
  left: 0;
  width: 0;
  height: 0;
  border-top: 20px solid transparent;
  border-left: 20px solid #fff;
  border-bottom: 20px solid transparent;
}

.menu-link:after {
  content: "";
  position: absolute;
  right: -1.053em;
  width: 0;
  height: 0;
  border-top: 20px solid transparent;
  border-bottom: 20px solid transparent;
  border-left: 20px solid #444;
}
```

__NB :__ Internet Explorer 8 ne supporte que la syntaxe CSS2 (`:before` et `:after`).

On n'oublie pas d'ajouter des effets visuels lors du __hover__ et aussi lors du __focus__ (pour ceux qui naviguent via un clavier).

```css
.menu-link:hover,
.menu-link:focus {
  background-color: #f90;
}

.menu-link:hover:after,
.menu-link:focus:after {
  border-left-color: #f90;
}
```

### Acte 5
Une petite version __responsive__.