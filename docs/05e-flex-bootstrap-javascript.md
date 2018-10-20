---
id: flex-bootstrap-javascript
title: Flex, bootstrap e javascript
sidebar_label: Flex, bootstrap e javascript
---

## Frameworkless

Ultimamente la tendenza è di limitare l'inclusione di framework e librerie non più indispensabili grazie allo sviluppo di nuove tecnologie. 

Tra quelli costantemente in uso in Websolute, citiamo sicurante jQuery e Boostrap.

## Flex e bootstrap

Tendenzialmente il framework Bootstrap può essere ancora usato, ma ne consigliamo l'abbandono poichè ormai, grazie alle classi messe a disposizioni __flex__, ricreare certi comportamenti delle griglie è diventato molto semplice e veloce rispetto a qualche anno fa, facilitando e velocizzando lo sviluppo. 

Vi suggeriamo la chiara e semplice [guida flex](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) di Chris Coyier su CSS tricks.

Inoltre con l'arrivo delle [griglie CSS](https://css-tricks.com/snippets/css/complete-guide-grid/), abbiamo un'ulteriore strumento a supporto della crezione di layout, e di recente la [compatibilità griglie sui browser](https://caniuse.com/#search=grid) è buona.

Soprattutto non saremmo più condannati ad avere troppe classi inserite inline nell'html.

>Scrivendo poco codice, chiaro e "parlante", potremo modificare direttamente il CSS con i nostri moduli e modificatori. Il grado di personalizzazione sarà maggiore ma la comprensione e la leggibilità sarà migliore, soprattutto nel caso in cui usassimo BEM. 

Le stesse media query sono sempre più semplici da applicare anche grazie all'uso dei _mixin_ di cui abbiamo discusso nel capitolo precedente. Inoltre, grazie alle proprietà di flex e delle griglie, spesso non abbiamo più nemmeno bisogno di fare media query per gestire il responsive.

Lo stesso [bootstrap 4](https://getbootstrap.com/docs/4.0/getting-started/introduction/) non fa altro che sfruttare tutte le logiche di flex, ma a volte aumenta la complessità piuttosto che semplificare il lavoro. 

Tuttavia, qualora si decidesse di usare Bootstrap, raccomandiamo l'uso della versione 4.

## jQuery e Javascript

jQuery è senza dubbio una libreria javascript molto pratica e veloce, che ci da tanti strumenti per la manipolazione imperativa del DOM e tante altre features a cui ci siamo abituati negli anni. Molti plugin che utilizziamo inoltre, dipendono da jQuery obbligandone l'inclusione nei progetti. 

>Nonostante questo, le logiche e i metodi di sviluppo sono cambiate radicalmente con l'arrivo di tecnologie avanzate come node.js, i framework javascript come Angular o React (che modificano il DOM in maniera dichiarativa), ECMAScript 6, Typescript, i package manager e i task runner, e jQuery inizia a diventare molto meno necessaria. 

Non a caso ormai la maggior parte delle nuove librerie javascript sono scritte in _Vanilla js_, cioè javascript puro. 

Infatti oggi, con poche righe di javascript, possiamo fare tutto ciò che facciamo con jQuery senza difficoltà, e molto di più. 

Un sito utile è [youmightnotneedjquery.com](http://youmightnotneedjquery.com/) in cui possiamo cercare dei metodi di jquery che vengono "tradotti" in javascript.

Non dimentichiamoci poi che dover includere sempre delle librerie come jQuery, può portare a problemi di manutenzione sul lungo periodo nei casi in cui dovremo aggiornare dei componenti o le librerie stesse, creando incompatibilità e problematiche. Usando javascript puro, non avremo di questi problemi.

Inoltre è molto, molto più performante e lo conferma questo interessante [case history sulle performance](https://medium.com/@trombino.marco/you-might-not-need-jquery-a-2018-performance-case-study-aa6531d0b0c3). 

>Detto ciò, si consiglia di iniziare ad allontanarsi da jQuery ed iniziare ad usare vanilla js, anche in ottica di utilizzo di nuovi potenti strumenti come typescript e i nuovi metodi di ES6.


## Convenzioni Javascript

In ultimo, vediamo come strutturare il nostro codice javascript in modo lineare e chiaro.

Dentro la cartella del tema base _src/js/_ troviamo il file _main.js_ al cui interno andremo a mettere tutte le nostre funzioni javascript.

Potremo dedidere se avviarle al DOC ready o al caricamento della pagina. Per convenzione, andrebbero scritte le funzioni sopra al DOC ready e dividendo le une dalle altre con dei commenti ben evidenti.


```
/*--------------------------------------------------
Example
--------------------------------------------------*/
function example() {
  console.log('this is an example')
}


/*--------------------------------------------------
DOC READY
--------------------------------------------------*/
$(function () {

    example();

}); 
  
    
/*--------------------------------------------------
WIN LOAD
--------------------------------------------------*/ 
$(window).on('load', function () { 
}
```

Nella cartella _src/js/vendor/_ invece troviamo tutte le librerie esterne che includiamo senza doverle modificare. 

>NB: Se avessimo troppo codice in un singolo file, possiamo usarne diversi dal main.js ma sarà poi necessario modificare il gulpfile per la compilazione corretta.