---
id: modularita
title: Modularità
sidebar_label: Modularità
---

Ora che abbiamo tutti gli strumenti e le informazioni per creare un progetto base, è il momento di andare ad analizzare le convenzioni che dovremmo utilizzare per la scrittura di HTML e CSS modulare, comprensibile e mantenibile.

A tal proposito, vi segnaliamo una guida decisamente chiara e utile del blogger *space ninja* [guida CSS modulare](https://spaceninja.com/2018/09/17/what-is-modular-css/). Servendoci di essa, introdurremo il concetto di __modularità__.

## Problematiche

Scrivere CSS su larga scala senza strutturare a dovere le classi, i naming e il relativo html con delle logiche ben definite, può diventare problematico in ottica di mantenibilità e comprensibilità, creando un probabile debito tecnico.

* __Comprensibilità:__

```
<div class="box profile pro-user">
  <img class="avatar image" />
  <p class="bio">...</p>
</div>
```
Alcune domande che posso pormi leggendo questo HTML:

>In che modo _box_ e _profile_ sono correlati tra loro? In che modo il _profilo_ e _avatar_ sono correlati tra loro o non lo sono? La classe _image_ e quella _bio_ si troveranno nella stessa parte del CSS? Puoi usare _avatar_ altrove?

* __Difficile riusabilità:__

Riusare il codice può essere sorprendentemente difficile. Ad esempio: c'è uno stile su una pagina che vuoi riutilizzarlo su un'altra, ma quando ci provi, scopri che è stato scritto in un modo che funziona solo sulla prima. 

L'autore riteneva che quello stile dovesse essere usato solo all'interno di un particolare elemento o che ereditasse determinate classi dalla pagina. Quindi fuori da quel contesto, non funziona e per evitare di rompere l'originale, duplichi il codice da un'altra parte e lavori su quello.

Ora hai due problemi: hai il codice originale e il codice duplicato. Hai raddoppiato il tuo onere di manutenzione.

* __Difficile da mantenere:__

Il problema principale è andare ad effettuare delle manutenzioni su CSS di larga scala. Rischiamo sempre di modificare una cosa e romperne altre, andando a far decadere tutte le logiche originali di stesura dei file di stile.


## Concetto di Modularità

Citando la guida:

> L'idea è di assicurarsi che la cosa che stai scrivendo non farà più di quello che è stato scritto.

Se avessimo un design di questo tipo:

<img class="img" src="../img/05a-image-01.gif" >

***

Andando ad analizzarlo vedremmo delle sezioni ben distinte, più o meno così:

<img class="img" src="../img/05a-image-02.jpg" >

***

Il che ha senso, ma facendo un passo indietro dovremmo iniziare a pensare alla pagina come un'__insieme di piccoli pezzetti riutilizzabili in più parti nel progetto__.

<img class="img" src="../img/05a-image-03.png" >

***

L'abilità dello sviluppatore front-end sarà quindi quella di studiare i layout ricevuti dal designer, individuare questo tipo di moduli riutilizzabili, crearli e far si che funzionino ovunque, apportando dei modificatori che ne cambiano il comportamento a seconda del design.

Ad esempio:

<img class="img" src="../img/05a-image-04.jpg" >

***

Un esempio ancora più concreto di componenti modulari è facebook. Vediamo uno stream classico con evidenziati i moduli css riutilizzati un po' dapertutto nel social network:

<img class="img" src="../img/05a-image-05.png" >

***

Quindi ottimizzando gli stili usati per questi pattern ripetuti, puoi risparmiare enormi quantità di codice. Ciò porta a prestazioni reali, risparmi sui costi di manutenzione e miglioramento della comprensibilità e lettura da parte dei tecnici.

>Queste logiche inoltre si avvicinano alle più recenti evoluzioni in ambito di design digitale come il __Design System__ o ai framework javascript come __Angular__ e __React__ con cui avremo sempre più a che fare.

A supporto di questa logica modulare, abbiamo diversi metodi e strumenti di lavoro, che andiamo subito ad analizzare.
