# Documentation

## Convention BEM
* B -> Block
* E -> Element
* M -> Modifier

```html

<!-- mainList = Block -->
<ul class="mainList mainList--xmas">
  <!-- __item = Element -->
  <li class="mainList__item">
    <!-- __itemLink = Element -->
    <a class="mainList__itemLink mainList__itemLink--isActive" href="/home">HOME</a>
  </li>
  <li class="mainList__item">
    <!-- __itemLink = Element -->
    <a class="mainList__itemLink" href="/about">About</a>
  </li>
  <li class="mainList__item">
    <!-- __itemLink = Element -->
    <a class="mainList__itemLink" href="/works">Works</a>
  </li>
</ul>
```

Exemple en SCSS

```css
.mainList {
  display: flex;
  justify-content: space-between;
  &--xmas {
    background: green;
  }
  &__item {
    list-style: none;
  }
  &__itemLink {
    color: red;
    &--isActive {
      color: white;
    }
  }
}
```

Exemple en CSS

```css
.mainList {

}

.mainList--xmas {

}

.mainList__item {

}

.mainList__itemLink {

}

.mainList__itemLink--isActive {

}
```

## Pseudo attributs

Les pseudos attributs `before` et `after` prermettent de créer des noeuds HTML en CSS.
Ils sont essentiellement utilisés pour ajouter des ornements, des décorations... On peut bien entendu faire des animations avec, les positionner par rapoport à leur parent (relative / absolute). **Ils doivent obligatoirement avoir un `content: ''`** afin de s'afficher.

```HTML
<section class="cover">
  <h1 class="cover__mainTitle">Présentation des pseudos-attributs</h1>
</section>
```

```CSS
.cover {
  background: #FDFDFD;
  padding: 20px;
  &__mainTitle {
    text-align: center;
    font-size: 24px;
    color: green;
    position: relative;
    &::before,
    &::after {
      content:'';
      display: block;
      width: 50px;
      height: 50px;
      background: green;
      top: 0;
      position: absolute;
    }
    &::before {
      left: 0;
    }
    &::after {
      right: 0;
    }
  }
}
```

## REM, EM, %, VW Sizing

### %

### EM

* Relative à la taille de son parent direct. A utiliser pour calculer les margins et paddings.

```CSS
.cover {
  font-size : 100%; /* 100% = 16px */
  &__mainTitle {
    /* 1em = 16px */
    font-size: .8em;
  }
}
```

### REM

* Le REM est basé sur la taille de la racine (soit la balise <html>) qui, par défaut a une valeur de 16px. Afin d'éviter tout calcul, il est nécessaire de l'écraser en donnant une base de 10px soit 62.5%.
* Le REM est intéressant à utiliser si les media-queries employées sont en rem également. Cela permettra de garder des proportions égales lorsqu'on va redimensionner la page.
* Ses proportions seront également gardées quand l'utilisateur zoomera dans la page.

```css
htlm {
  font-size: 62,5%;
}
.mainTitle {
  font-size : 1.6rem;
  width : 32rem;
}
```

### VW(idth) / VH(eight)

* Unités relatives à la taille de l'écran (peu importe le device)
* Attention au VH et à son contenur. 100 vh = 100vh quoi qu'il arrive.
* VW : très utile pour les interfaces fluides.

```css
html {
  font-size: 62,5%;
}
```

## Positionner un élément en CSS

La propriété *position* permet de spécifier le type de méthode de positionnement à appliquer à un élément. Elle accepte 5 valeurs : static, relative, absolute, fixed ou sticky.

* **Static :** Valeur par défaut. L'élément n'est positionné d'aucune manière spéciale. Un élément static est dit *non positionné* et un élément avec une propriété position ayant une valeur autre que static est dit *positionné*.

```CSS
.element {
  position: static;
  background-color: white;
  width: 500px;
}
```

* **Relative :** Relative se comporte de la même façon que static sauf si des propriétés supplémentaires lui sont ajoutées, comme par exemple : *top, right, bottom et left*.

```CSS
.element {
  position: relative;
  top: -20px;
  left: 20px;
  background-color: white;
  width: 200px;
}
```

* **Fixed :** Un élément positionné en fixed est positionné par rapport à la fenêtre du navigateur et restera toujours à la même place même si la page défile. De la même manière qu'avec un élément positionné en relative, il est possible d'utiliser les propriétés *top*, *right*, *bottom* et *left*.

``` CSS
.element {
  position: fixed;
  bottom: 0;
  right: 0;
  background-color: white;
  width: 200px;
}
```
* **Absolute :** Absolute se comporte comme fixed sauf que son positionnement est relatif à l'élément parent positionné le plus proche au lieu d'être relatif à la fenêtre du navigateur. Si un élément positionné en absolute n'à aucun élément parent positionné, il utilise le corps du document et se déplace avec le document au défilement de la page.

```CSS
.element {
  position: absolute;
  top: 120px;
  right: 0;
  width: 200px;
  height: 300px;
}
```

* **Sticky :** Un élément sticky se positionne par rapport à la position du scroll de l'utilisateur. Il alterne entre position *relative* et *fixed*, cela dépend de la position du scroll. L'élément est positionné en relative jusqu'à ce qu'il atteigne une position donnée - là, il "s'accroche" à cette position (comme une position *fixed*).  

```CSS
.element {
  position: sticky;
  top: 0;
  padding: 5px;
  background-color: white;
}
```

## Cacher un élément en CSS

* **Display : none**

L'élément n'apparaîtra pas dans la page bien qu'il soit toujours possible d'interagir avec lui à travers le DOM. Aucune place ne lui sera alloué dans la page.

* **Visibility : hidden**

Visibility hidden rendra l'élément invisible mais l'espace qui lui est attribué lorsqu'il est visible sera gardé. Il n'est pas possible d'effectuer de transition sur une propriété visibility.

* **Opacity : 0** 

Une opacité réglée à 0 rendra invisible un élément mais il continuera d'occuper son espace dans la page. Il est possible d'appliquer des transitions sur cette propriété, et donc par exemple de faire apparaître un élément graduellement. 

## Garder un ratio 

Pour créer des éléments qui gardent le même ratio lorsque la fenêtre est redimensionnée : 
* Créer une *DIV* qui servira de container

```HTML
<div class="container"> 
</div>

```
* Donner une largeur *width* en pourcentage au container. Ajouter un attribut CSS *padding-top* au container et lui donner une valeur en pourcentage. Le container gardera ainsi toujours le même ratio. Ex : un carré restera toujours carré.

```CSS
.container {
    background-color: turquoise;
    width: 100%;
    padding-top: 100%; /* 1:1 Aspect Ratio */
}
```

## @Font-face

* Qu’est-ce que c’est ?

La règle @font-face permet de définir les polices d'écriture à utiliser pour afficher le texte de pages web. Les utilisateurs ne sont plus obligés de choisir uniquement des polices dites « web-safe » (installées sur les postes des utilisateurs), ils peuvent à la place fournir des polices non standards. La règle @font-face peut être utilisée au niveau global d'une feuille de style et également au sein d'un groupe lié à une règle conditionnelle. Attention, elle ne peut pas être utilisée au sein d’une propriété CSS.

* Comment l’utiliser ?

L’utilisation basique de la règle @font-face est simple, il suffit de définir le nom de la police puis de signifier la source dans laquelle elle se trouve, comme dans l’exemple suivant :

```CSS
@font-face {
  font-family: 'quadranta';
  src: url('quadranta.eot');
}
```

Pour l'utiliser, il suffit ensuite d'appliquer une propriété *font-family* à un élément et de lui spécifier le nom de la font-face :

```CSS
p {
font-family: 'quadranta', serif;
}
```


## Cheatsheets

* JavaScript : http://overapi.com/javascript

* React :  https://devhints.io/react

* Redux : https://github.com/linkmesrl/react-journey-2016/blob/master/resources/egghead-redux-cheat-sheet-3-2-1.pdf

* VueJS : https://vuejs-tips.github.io/cheatsheet/

* SCSS : https://devhints.io/sass

* GraphQL : https://raw.githubusercontent.com/sogko/graphql-shorthand-notation-cheat-sheet/master/graphql-shorthand-notation-cheat-sheet.png

*Liste complète dans cet article : https://medium.freecodecamp.org/modern-frontend-hacking-cheatsheets-df9c2566c72a*


## Liens utiles

### Flexbox

Un article complet pour comprendre le système des flexboxs et comment utiliser cette propriété CSS :

https://css-tricks.com/snippets/css/a-guide-to-flexbox/

### Grids

Un article complet pour comprendre comment fonctionnent les grids en CSS et apprendre à s'en servir :

https://medium.freecodecamp.org/learn-css-grid-in-5-minutes-f582e87b1228

Un cours gratuit et complet en vidéos pour devenir un grid master : 

https://medium.freecodecamp.org/heres-my-free-css-grid-course-merry-christmas-3826dd24f098

### CSS master

Un article remplis de pro tips pour tout ceux qui veulent masteriser le CSS :

https://medium.com/@peedutuisk/lesser-known-css-quirks-oddities-and-advanced-tips-css-is-awesome-8ee3d16295bb

### The THIS keyword in JavaScript 

Un bon article/vidéo pour clarifier le concept un peu complexe du THIS en JavaScript :

https://tylermcginnis.com/this-keyword-call-apply-bind-javascript/






