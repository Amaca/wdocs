---
id: naming-bem
title: Naming e BEM
sidebar_label: Naming e BEM
---

Per rendere il codice ancora più leggibile, sarebbe necessario scrivere dei nomi di classi _"parlanti"_, cioè in grado di farci capire fin da subito di che cosa si tratta.

## Fasce, container, wrapper e item

Spesso i designer preparano dei layout divisibili in fasce, cioè linee di elementi con delle funzioni specifiche, ad esempio "fascia con slider", "fascia ultimi prodotti" ecc... 

Possiamo usare il tag html __section__ per definire una fascia. Solitamente viene seguita da un contenitore che definisce la larghezza del suo contenuto. Per dare un'indicazione evidente ai programmatori, è buona norma aggiungere dei commenti che sottolineano l'inizio e la fine della sezione.

E' utile usare degli ulteriori _div_ contenitori all'interno della sezione, che possiamo chiamare __.wrapper__ , così da raggruppare degli elementi facilmente (molto utile in caso di uso di flex).


Vediamo un esempio di fascia che mostra 2 articoli tra gli ultimi pubblicati:

```
<!-- Last posts -->
<section class="last-posts">
  <div class="container">
    <div class="wrapper">  

      <div class="item">
        <div class="img">
          <img src="#" alt="">
        </div>
        <div class="box">
          <div class="tit"><h1>Lorem ipsum dolor sit amet</h1></div>
          <div class="text">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</div>
        </div>
      </div>

      <div class="item">
        <div class="img">
          <img src="#" alt="">
        </div>
        <div class="box">
          <div class="tit"><h1>Lorem ipsum dolor sit amet</h1></div>
          <div class="text">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</div>
        </div>
      </div>     

    </div>
  </div>
</section>
<!-- /Last posts -->
```

In questo caso abbiamo creato una __section__ denominata _.last-posts_ con un _container_ che definisce la larghezza massima dei contenuti, un _wrapper_ e due elementi denominati _item_ con all'interno i moduli _.img_ e _.box_

Quindi:

>il consiglio principale sul nome degli elementi è di renderli corti, comprensibili e indipendenti dal contenuto, __trovando invece un nome legato alla sua funzione principale__.

## Coerenza e uniformità

Interrompiamo un attimo il naming per sottolineare un paio di note molto importanti.

>Va mantenuta coerenza e uniformità tra i vari file in sviluppo. Se definiamo una _section_ in un template, dovremmo mantenere quella struttura html il più possibile simile alle altre. 

Possiamo naturalmente modificare il suo interno, ma sempre con un certo criterio e con un'attenzione particolare alla visione globale del progetto. Non potremo quindi andare ad aggiungere dei contenitori sopra alla section così, senza motivo o cambiare completamente il codice interno. 

L'html andrebbe modificato grazie all'uso dei modificatori css. Questo perchè il programmatore non dovrà andare a riagganciare tutto l'html da capo, ma andrà soltanto ad inserire le classi di modifica dove è opportuno.

>In aggiunta, l'uso di librerie esterne, come ad esempio gli slider, devono essere limitati il più possibile e, se si decide di usarne uno, dovrà essere sfruttato quello senza andare ad aggiungerne continuamente di nuovi. 

## Riferimento a genitore su classi

Torniamo ora ai naming di classi. Se avessimo una lista di news, piuttosto che denominarle _.news_ riferendoci al contenuto dell'elento, potremmo chiamare il modulo _.listing_ e gli elementi al suo interno _.item_.

In questo modo potremo creare un modulo generico chiamato _listing_ utilizzabile in altre parti del progetto, e non legarci necessariamente alle news.


>Questo genere di approccio è utile ma a volte può risultare poco chiaro, perchè un _.item_ è un termine abbastanza generico e potrebbe essere utilizzato in altre occasioni, perdendone il controllo o generando confusione. 

Quindi a volte è comodo aggiungere dei riferimenti al modulo principale __sulle classi strettamente legate ad esso__.

>__Attenzione__: i moduli indipendenti come __.box__ o __.img__ rimangono invece con la loro classe originale, così da poter usare le loro caratteristiche definite fuori dal modulo _.listing_


```
<!-- Listing -->
<section class="listing">
  <div class="container">
    <div class="listing-wrapper">  

      <div class="listing-item">
        <div class="img">
          <img src="#" alt="">
        </div>
        <div class="box">
          <div class="tit"><h1>Lorem ipsum dolor sit amet</h1></div>
          <div class="text">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</div>
        </div>
      </div>

      <div class="listing-item">
        <div class="img">
          <img src="#" alt="">
        </div>
        <div class="box box-light">
          <div class="tit"><h1>Lorem ipsum dolor sit amet</h1></div>
          <div class="text">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</div>
        </div>
      </div>     

      ...
      ...

    </div>
  </div>
</section>
<!-- /Listing-->
```

>Questo tipo di approccio viene ancor più automatico grazie all'uso della metodologia BEM, che consigliamo fortemente.

## Metodologia BEM

BEM (Block Element Modifier) è un modo di scrivere CSS che aiuta molto nella stesura dei naming, dei moduli e dei loro modificatori. In Websolute stiamo iniziando ad utilizzarlo e, a prescindere, aiuta a capire il concetto di componenti.

Vi consigliamo vivamente la [Guida sui CSS modulari](https://spaceninja.com/2018/09/17/what-is-modular-css/) per capire la logica di BEM o la [Guida ufficiale](http://getbem.com/naming/)

BEM definisce 3 tipologie da usare:

1) __Blocchi__: devono essere indipendenti e innestabili, quindi riutilizzabili in qualunque parte del progetto senza rompere niente. I blocchi inoltre sono ripetibili, quindi devono poter essere ripetuti nel layout senza problemi 
(esempio: .card)
2) __Elementi__: sono parti di un blocco che non possono essere usati all'infuori di esso. 
(esempio: .card__image)
3) __Modificatori__: classi che definiscono il comportamento dei blocchi e dei suoi elementi 
(esempio: .card--big)

Il caso precedente, scritto in BEM sarebbe:

```
<!-- Listing-->
<section class="listing">
  <div class="container">
    <div class="listing__wrapper">  

      <div class="listing__item">
        <div class="img">
          <img src="#" alt="">
        </div>
        <div class="box">
          <div class="tit"><h1>Lorem ipsum dolor sit amet</h1></div>
          <div class="text">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</div>
        </div>
      </div>

      <div class="listing__item">
        <div class="img">
          <img src="#" alt="">
        </div>
        <div class="box box--light">
          <div class="tit"><h1>Lorem ipsum dolor sit amet</h1></div>
          <div class="text">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</div>
        </div>
      </div>     

    </div>
  </div>
</section>
<!-- /Listing -->
```

>Facciamo quindi riferimento al modulo principale nelle classi con i due _underscore_ , mentre se aggiungiamo un modificatore come _box--light_ andranno inseriti i due trattini.


Qui alcuni esempi molto semplici per capire la logica grazie all'uso di una minifigure LEGO, che va a rappresentare il nostro modulo:

<img class="img" src="../assets/05c-image-01.png" />

<img class="img" src="../assets/05c-image-02.png" />

<img class="img" src="../assets/05c-image-03.png" />

<img class="img" src="../assets/05c-image-04.png" />


>BEM è molto pratico principalmente in lettura: con un veloce sguardo all'html siamo in grado di capire i moduli principali, i suoi elementi e i relativi modificatori.

Un semplice esempio di uso BEM:

```
<button class="btn btn--big btn--orange">
  <span class="btn__price">$9.99</span>
  <span class="btn__text">Subscribe</span>
</button>
```

Modificare il modulo listing e tutto ciò che è al suo interno a questo punto diventa facile e leggibile. 

A volte potremmo avere delle classi più lunghe del solito, ma rimane il fatto che è come se stessimo documentando l'html implicitamente, quindi ci sembra utile.

Se volessimo ad esempio sfruttare tutte le classi del listing, apportando però una sola classe modificatore che ne altera il comportamento, avremo:

```
<!-- Listing-->
<section class="listing listing--fullwidth">
  <div class="container">
    <div class="listing__wrapper">  

      <div class="listing__item">
        <div class="img">
          <img src="#" alt="">
        </div>
        <div class="box">
          <div class="tit"><h1>Lorem ipsum dolor sit amet</h1></div>
          <div class="text">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</div>
        </div>
      </div>

      <div class="listing__item>
        <div class="img">
          <img src="#" alt="">
        </div>
        <div class="box box--light">
          <div class="tit"><h1>Lorem ipsum dolor sit amet</h1></div>
          <div class="text">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</div>
        </div>
      </div>     

    </div>
  </div>
</section>
<!-- /Listing -->
```

Da css potremo modificare il comportamento originale del listing creando dei listing__item ad esempio di  _width: 100%;_ così da occupare una riga intera. 

>Facendo ciò, avremo sempre questo nuovo tipo di listing utilizzabile ovunque vogliamo, a prescindere dal contenuto. Grazie a BEM inoltre, capiremo con un solo sguardo che _.listing--fullwidth_ è un modificatore che va a modificare il comportamento di alcune classi del modulo originale _.listing_

Procediamo a vedere altri strumenti utili per la modularità del css.