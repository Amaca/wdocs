---
id: moduli-modificatori
title: Moduli e modificatori
sidebar_label: Moduli e modificatori
---

Tenendo ben presenti i concetti di modularità, andiamo a vedere alcune convenzioni che dovremmo mantenere sempre durante lo sviluppo dei temi.

## Modulo BOX

Cerchiamo di capire quali sono i moduli che possiamo trovare in un layout generico. 

Solitamente riusciamo facilmente a definire almeno questi:

* Titoli
* Sottotitoli
* Etichette
* Liste
* Testi
* Immagini
* CTA

Tutti gli elementi sopracitati, possono essere divisi in piccoli moduli riutilizzabili in tutto il sito. Ad esempio potremmo definire un elemento denominato BOX che può contenere tutta una serie di elementi:

```
.box {

  .tit {
    stile del titolo
    ...
  }

  .subtit {
    stile del sottotitolo
    ...
  }

  .eyelet {
    stile delle etichette
    ...
  }

  .text {
    stile dei testi
    ...
  }

  .cta {
    stile delle cta
    ...
  }
}
```

>Questo elemento __.box__ è definibile modulo in quanto al suo interno ha degli elementi che si comporteranno sempre alla stessa maniera, a prescindere da dove verrà messo e riutilizzato nel sito. 

>Naturalmente abbiamo bisogno di cambiare il comportamento del .box a seconda del design, e potremo farlo con classi _"modificatore"_ o usando il modulo all'interno di un altro componente che va a variare le sue regole di default.

__Attenzione!__
La classe __.cta__ potrebbe essere una lista di bottoni, __che a loro volta sono definibili moduli__. 

Ad esempio:

```
<div class="box">
  <div class="tit">Benvenuto nel nostro sito</div>
  <div class="text">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</div>
  <div class="cta">
    <a href="#" class="btn btn-main">Vai al sito</a>
    <a href="#" class="btn btn-ghost">Vai allo store online</a>
    <a href="#" class="btn btn-inline">Torna indietro</a>
  </div>
</div>
```

Quindi, oltre ad aver definito il modulo .box, dovremo definire anche il .btn che avrà le sue varianti (nell'esempio *btn-main*, *btn-ghost* e *btn-inline*) e i suoi comportamenti.

>E' proprio questo il concetto di modularità: creare tanti elementi che possono essere iniettati all'interno di altri.

***

## Modificare un modulo

Partendo da questo esempio:

```
<div class="box">
  <div class="tit">Benvenuto nel nostro sito</div>
  <div class="text">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</div>
</div>
```

ipotizziamo che lo stile legato al modulo .box sia questo:

```
.box {
  background: grey;

  .tit {
    color: white;
    font-size: 20px;
    padding-bottom: 30px;
  }

  .text {
    color: white;
    font-size: 16px;
    padding-bottom: 30px;
  }
}
```

Abbiamo quindi definito lo stile di _default_ del modulo. Naturalmente non potremo utilizzarlo sempre allo stesso identico modo in tutto il sito.
Supponiamo di __voler cambiare i colori degli elementi__ del _.box_. Come?

Possiamo andare a creare delle varianti, principalmente in due modi:

1. creare un modificatore
2. cambiare le classi grazie al container genitore


## Crare un modificatore

Con modificatore intendiamo una classe che va inserita in linea nell'HTML per indicare una modifica del modulo.

Vediamo il SCSS:

```
.box {
  background: grey;

  .tit {
    color: white;
    font-size: 20px;
    padding-bottom: 30px;
  }

  .text {
    color: white;
    font-size: 16px;
    padding-bottom: 30px;
  }

  //classe modificatore che crea la variante del box default
  &.box-light {
    background: white;

    .tit {
      color: black;
    }

    .text {
      color: black;
    }
  }
}
```

Così facendo, da HTML dovremo soltanto andare ad inserire la classe modficatore sul box, andando a cambiare le regole del modulo a seconda di come è stato configurato. Questa regola sarà applicabile a tutti i box del sito.

```
<div class="box box-light">
  <div class="tit">Benvenuto nel nostro sito</div>
  <div class="text">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</div>
</div>
```

## Modifica dal container genitore

Le classi modificatori sono molto utili quando dobbiamo creare una regola che ci tornerà utile in tutto il sito. Cosa succede invece se abbiamo una modifica singola relativa soltanto ad una fascia specifica e che non riuseremo più?

In questo caso, conviene sovrascrivere le regole del modulo riferendosi al genitore in cui è contenuto.

Vediamo un esempio. Ipotizziamo di avere una sezione con un listing di news di questo tipo:

```
<section class="listing-news">
  <div class="container">

    <article class="news">
      <div class="box">
        <div class="tit">
          orem ipsum dolor sit amet
        </div>
        <div class="text">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit.
        <div>
        <div class="cta">
          <a href="#" class="btn btn-main">Leggi news</a>
        </div>
      </div>
    </article>

    ... 
    ...
    ...

  </div>
</section>
```

Se avessimo bisogno di una modifica del comportamento degli elementi di __.box__ e avremo questa modifica presumibilmente solo nel listing news, potremo variarlo direttamente nel modulo genitore __.listing-news__:

```
.listing-news {

  .news {

    .box {
      border: 1px solid grey;

      .tit {
        color: red;
        font-size: 22px;
      }

      .text {
        color: black;
        font-size: 18px;
      }
    }

  }

}
```

Così facendo le regole di default del modulo box saranno valide, ma verranno modificate dal modulo genitore __.listing-news__

>Il modulo __.box__ è applicabile praticamente a qualsiasi tipo di sito, chiaramente con le sue varianti di elementi e modificatori. 
Questo tipo di logica andrebbe applicata a tutti gli elementi del sito, dove possibile.

***

>Grazie alla definizione di moduli che ne contengono altri, con tutte le loro relative classi modificatori, potremo sviluppare un sito modulare, leggibile e comprensibile a tutti rapidamente. 

Andiamo a vedere ora i naming delle classi e l'eventuale utilizzo di BEM.