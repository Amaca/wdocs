---
id: sass-mixin
title: Moduli sass e mixin
sidebar_label: Moduli sass e mixin
---

Grazie all'uso dei preprocessori css, possiamo utilizzare una serie di strumenti che ci aiutano a modulare ancora di più i nostri elementi.

Al momento websolute utilizza il preprecessore _scss_ , quindi è questo che consigliamo di usare (infatti è quello già configurato nei temi base discussi in precedenza)

## Moduli .sass

Nel nostro tema base i file sass sono importati da un file principale chiamato _src/scss/main.scss_ che con questa sintassi include gli altri moduli presenti nella cartella _modules_:

```
@import "_modules/variables";
@import "_modules/base";
@import "_modules/mixins";
@import "_modules/typography"; 
@import "_modules/buttons";
@import "_modules/header";
@import "_modules/footer"; 
```

>Ad ogni modulo che creiamo (come ad esempio il nostro _.box_ ) possiamo associargli un file _.sass_ in cui definire tutti gli elementi e i suoi modificatori.

In questo modo sarà molto facile, anche per uno frontender che non ha mai visto il codice, trovare il file legato al modulo che cerca.


## Variabili e Mixins

I preprocessori css ci mettono a disposizione le variabili, che possiamo definire nel modulo _src/scss/modules/variables.scss_

Allo stesso modo possiamo includere dei mixins, cioè delle vere e proprie funzioni per generare il css. 

Per includere mixins e variabili negli altri file, dopo averli creati e definiti basta scrivere in cima ai moduli:

```
@import 'variables';
@import 'mixins';
```

## Media Query

Senza dubbio tra i mixin più utili troviamo quelli delle media query. Ne abbiamo predisposte alcune con i più comuni breakpoint, permettendoci di usare una sintassi molto comoda e veloce per richiamare le media query. 

Vediamo intanto i mixin:


```
//--------------------------------------------------
//Media Query
//--------------------------------------------------
$xl-width: 1560px;
$lg-width: 1499px;
$md-width: 1199px;
$sm-width: 991px;
$xs-width: 767px;
$xxs-width: 575px;


@mixin xl {
  @media (max-width: #{$xl-width}) {
    @content;
  }
} 

@mixin lg {
  @media (max-width: #{$lg-width}) {
    @content;
  }
} 

@mixin md {
  @media (max-width: #{$md-width}) {
    @content;
  }
}

@mixin sm {
  @media (max-width: #{$sm-width}) {
    @content;
  }
}

@mixin xs {
  @media (max-width: #{$xs-width}) {
    @content;
  }
}
 
@mixin xxs {
  @media (max-width: #{$xxs-width}) {
    @content;
  }
}
```

Per utilizzare le media query, non dovremo far altro che scrivere:

```

.box {
  
  .text {
    font-size: 20px;

    @include sm { //media query su max width 991px
      font-size 16px
    }

    @include xs { //media query su max width 767px
      font-size 14px
    }
  }
}

```

Andiamo ora a vedere alcune convenzioni riguardo il javascript.