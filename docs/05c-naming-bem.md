---
id: naming-bem
title: Naming e BEM
sidebar_label: Naming e BEM
---

Per rendere il codice ancora più leggibile, è necessario scrivere dei nomi di classi _"parlanti"_, cioè in grado di farci capire fin da subito di che cosa si tratta.

Questo aspetto è molto soggettivo, ma ci sentiamo di dare delle indicazioni così da capire se non altro le logiche che a nostro parere sono utili.

## Fasce, container, wrapper e item

Spesso i designer preparano dei layout divisibili in fasce, cioè linee di elementi con delle funzioni specifiche, ad esempio "fascia con slider", "fascia ultimi prodotti" ecc... 

Possiamo usare il tag html _section_ come indicazione di fascia. Solitamente viene seguita da un contenitore che definisce la larghezza del suo contenuto. Per dare un'indicazione evidente ai programmatori, è buona norma aggiungere dei commenti che sottolineano l'inizio e la fine della sezione.

E' utile usare degli ulteriori contenitori all'interno della sezione, che possiamo chiamare _.wrapper_ , così da raggruppare degli elementi facilmente (molto utile in caso di uso di flex).

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

In questo caso abbiamo creato una <section> denominata _.last-posts_ con un _container_ che definisce la larghezza massima dei contenuti, un _wrapper_ e due elementi denominati _item_ con all'interno i moduli _.img_ e _.box_

Quindi:

>il consiglio principale sul nome degli elementi è di renderli corti, comprensibili e indipendenti dal contenuto, __trovando invece un nome legato alla sua funzione principale__.


## Riferimento a genitore su classi

Se avessimo una lista di news, piuttosto che denominarle _.news_ cioè riferendoci al contenuto dell'elento, potremmo chiamarlo _.listing_ e gli elementi al suo interno _.item_.

In questo modo potremo creare un modulo generico chiamato _listing_ utilizzabile in altre parti del progetto, e non legarci necessariamente alle news.


Questo genere di approccio è utile ma a volte può risultare poco chiaro, perchè un _.item_ è un termine abbastanza generico e potrebbe essere utilizzato in altre occasioni, perdendone il controllo o generando confusione. Quindi a volte è comodo aggiungere dei riferimenti al modulo principale sulle classi strettamente legate ad esso:


```
<!-- Last posts -->
<section class="last-posts">
  <div class="container">
    <div class="last-posts-wrapper">  

      <div class="last-posts-item">
        <div class="img">
          <img src="#" alt="">
        </div>
        <div class="box">
          <div class="tit"><h1>Lorem ipsum dolor sit amet</h1></div>
          <div class="text">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</div>
        </div>
      </div>

      <div class="last-posts-item">
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

Ciò nonostante i moduli _box_ e _img_ rimangono invariati perchè per loro natura non sono legati strettamente al modulo _last-posts_

Questo tipo di approccio viene ancor più automatico grazie all'uso della metodologia BEM.

## Metodologia BEM

BEM (block element modifier) è un modo di scrivere CSS che aiuta molto nella stesura dei naming, dei moduli e dei loro modificatori.

Vi consigliamo vivamente la [Guida sui CSS modulari](https://spaceninja.com/2018/09/17/what-is-modular-css/) per capire la logica di BEM o la [Guida ufficiale](http://getbem.com/naming/)


Il caso precedente, scritto in BEM sarebbe:

```
<!-- Last posts -->
<section class="last-posts">
  <div class="container">
    <div class="last-posts__wrapper">  

      <div class="last-posts__item">
        <div class="img">
          <img src="#" alt="">
        </div>
        <div class="box">
          <div class="tit"><h1>Lorem ipsum dolor sit amet</h1></div>
          <div class="text">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</div>
        </div>
      </div>

      <div class="last-posts__item>
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
<!-- /Last posts -->
```

Facciamo quindi riferimento al modulo principale nelle classi con i due _underscore_ , mentre se aggiungiamo un modificatore come _box--light_ andranno inseriti i due trattini.


Qui alcuni esempi molto semplici per capire la logica grazie all'uso di una minifigure LEGO, che va a rappresentare il nostro modulo:

<img class="img" src="../img/05c-image-01.png" >

<img class="img" src="../img/05c-image-02.png" >

<img class="img" src="../img/05c-image-03.png" >

<img class="img" src="../img/05c-image-04.png" >


Un altro semplice esempio di uso BEM:

```
<button class="btn btn--big btn--orange">
  <span class="btn__price">$9.99</span>
  <span class="btn__text">Subscribe</span>
</button>
```

Procediamo a vedere altri strumenti utili per la modularità del css.