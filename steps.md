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

*Comment s'y prendre pour obtenir un rendu assez rapidement prenant en compte chacune de ces contraintes ?*

### Acte 2
Tout d'abord, commencons par regarder un petit aperçu de ce que vous voulons obtenir. 
![](http://clement-galidie.fr/github/html-css/exercice-fil-ariane/fil-ariane-resultat.jpg)
Nous avons donc un « menu » composé de cinq liens. Il y a également deux formes triangulaires aux deux extrémités de chaque liens. 

Premièrement, nous allons poser la base : le code **HTML**.
```
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
**NB : ** j'utilise la syntaxe [BEM](https://bem.info/) (sans l'écriture de base que je ne trouve absolument pas pratique).