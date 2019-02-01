---
id: versioning
title: Integrazione progetto e versioning
sidebar_label: Integrazione progetto e versioning
---

Grazie al tema blank configurato e funzionante, possiamo creare i nostri template grafici con html, css e javascript. 

Una volta creati i primi layout, sarà necessario integrarli nelle piattaforme di sviluppo vere e proprie, unendo il lavoro dello sviluppatore front-end con quello degli sviluppatori back-end. Vediamo come.

## Cenni di versioning

Essendo team numerosi è necessario versionare i file più metodicamente possibile. Websolute utilizza Team Foundation Server (o TFS) di Microsoft per seguire l'intero ciclo di vita dei progetti.

>Team Foundation Server è il prodotto di Microsoft per la gestione del codice sorgente, il controllo dei progetti, il tracking delle funzionalità e dello stato dei bug e più in generale per gestire in maniera completa il ciclo di vita del software.

Per i progetti BOM riusciamo a versionare tutti i file direttamente con il controllo di versione di TFS, il __source control__. In altri progetti, spesso quelli basati su php come i progetti Wordpress, si tende ad usare TFS ma questa volta con il sistema di versionamento __git__. Presto ci sarà un approfondimento e linee guida backend che approfondiranno queste tematiche. 

In entrambi i casi, gli sviluppatori al lavoro sul progetto creeranno l'ambiente di sviluppo e vi forniranno tutti i dati di accesso e le indicazioni necessarie per scaricare i file in locale.  

## Integrazione dei file

Una volta scaricati, non dovremo far altro che posizionare all'interno del progetto vero e proprio i nostri file di montaggio statico preparati precedentemente. 

>Così facendo, oltre che iniziare a versionarli correttamente, inizieremo a renderli accessibili in primis agli sviluppatori, che dovranno usarli per comporre i template veri e propri agganciandoli al CMS scelto. 

Infatti, dopo averli integrati con il progetto principale, se ci saranno altri montaggi da sviluppare, verranno creati direttamente nell'ambiente di sviluppo, così da mantenerli sempre versionati, aggiornati e utilizzabili dai programmatori. 

>Il tema base creato e discusso in precedenza può essere installato in tutte le piattaforme che vogliamo, ma sarà necessario modificare alcune impostazioni a seconda del CMS utilizzato, come i riferimenti ai file e alcuni task del gulpfile. 

Abbiamo creato due guide, una per *Wordpress* e uno per *BOM*, i principali CMS usati in Websolute.
