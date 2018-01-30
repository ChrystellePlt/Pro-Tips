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
htlm {
  font-size: 62,5%;
}
```

## Liens utiles
