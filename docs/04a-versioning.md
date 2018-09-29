---
id: versioning
title: Integrazione progetto e versioning
sidebar_label: Integrazione progetto e versioning
---

Grazie al tema blank configurato e funzionante, possiamo creare i nostri template grafici con html, css e javascript. 

Una volta creati i primi layout, sarà necessario integrarli nelle piattaforme di sviluppo vere e proprie, unendo il lavoro dello sviluppatore front-end con quello degli sviluppatori back-end. Vediamo come.

## Cenni di versioning

Essendo team numerosi è necessario versionare i file più metodicamente possibile. Websolute utilizza due tipologie di versionamento in base alla tipologia di progetto: 

* __git__ per progetti basati su *php*
* __tfs__ su quelli basati in *dotnet*.

In entrambi i casi, gli sviluppatori al lavoro sul progetto creeranno l'ambiente di sviluppo e vi forniranno tutti i dati di accesso e le indicazioni necessarie per scaricare i file in locale.  

## Integrazione dei file

Una volta scaricati i file, non dovremo far altro che posizionare all'interno del progetto vero e proprio i nostri file di montaggio statico preparati precedentemente. 

>Così facendo, oltre che iniziare a versionarli correttamente, inizieremo a renderli accessibili in primis agli sviluppatori, che dovranno usarli per comporre i template veri e propri agganciandoli al CMS scelto. 

Infatti, dopo averli integrati con il progetto principale, se ci saranno altri montaggi da sviluppare, verranno creati direttamente nell'ambiente di sviluppo, così da mantenerli sempre versionati, aggiornati e utilizzabili dai programmatori. 

>Il tema base creato e discusso in precedenza può essere installato in tutte le piattaforme che vogliamo, ma sarà necessario modificare alcune impostazioni a seconda del CMS utilizzato, come i riferimenti ai file e alcuni task del gulpfile. 

Per comodità, __abbiamo creato altri due temi base__, uno per *Wordpress* e uno per *BOM*, i principali CMS usati in Websolute.
