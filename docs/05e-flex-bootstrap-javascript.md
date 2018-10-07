---
id: flex-bootstrap-javascript
title: Flex, bootstrap e javascript
sidebar_label: Flex, bootstrap e javascript
---

## Flex e bootstrap

Ultimamente la tendenza è andare sempre di più a togliere framework e librerie non più necessarie grazie allo sviluppo di nuove tecnologie. Questo vale per jquery per javascript, come bootstrap per i css. 

Tendenzialmente il framework bootstrap può essere ancora usato, ma ne consigliamo l'abbandono poichè ormai, grazie alle classi _flex_, ricreare certi comportamenti delle griglie è diventato molto semplice e veloce rispetto a qualche anno fa, facilitando e velocizzando lo sviluppo. 

Soprattutto, non saremmo più condannati ad avere troppe classi inserite inline nell'html ma scrivenod poco html, chiaro e "parlante", potremo modificare direttamente il css con i nostri moduli personalizzati. 

Lo stesso bootstrap 4 non fa altro che sfruttare tutte le logiche di flex, ma a volte aumenta la complessità piuttosto che semplificare il lavoro.

Tuttavia, qualora si decidesse di usarlo, raccomandiamo l'uso dell'ultima versione 4, appunto.


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

>NB: Se avessimo bisogno di troppo codice per una singola pagina, possiamo usare dei file diversi da main.js ma sarà poi necessario modificare il gulpfile per la compilazione corretta.