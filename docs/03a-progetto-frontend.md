---
id: progetto-frontend
title: Template blank e alberatura
sidebar_label: Template blank e alberatura
---
L'obiettivo di chi sviluppa un template grafico è fornire ai programmatori tutte le pagine disegnate dai Designer in HTML, CSS e JS già pronte per essere agganciate ai CMS. __Fornire i file e scrivere codice in modo chiaro, semplice e intuitivo aiuterà e velocizzerà gli sviluppatori a lavorare ai template__. 

>Per questo motivo è necessario seguire le successive indicazioni, così da poter creare dei pacchetti di file perfettamente lavorabili e comprensibili a tutti.

## Template base statico
Abbiamo creato un repository git con un __template blank__ (vuoto) utile per iniziare a lavorare ai montaggi front-end. In questo modo è possibile avere già configurata l'alberatura delle cartelle, dei *moduli sass* base, alcune delle librerie più usate, il *package.json* per installare i *moduli node* con *npm* e una lista di task nel *Gulpfile*.

E' possibile scaricarlo da qui:

<a href="https://github.com/Amaca/Gulp-starter-theme" class="btn">Scarica Gulp Starter Theme</a>

Una volta scaricato, basta scompattare lo zip all'interno di una cartella con il nome del nuovo progetto.

## Alberatura
Si è deciso di creare questo tipo di alberatura di cartelle:

```

project
│
└───assets
│   └───img
│   └───fonts
│
└───dist
│   └───css
|       └───vendor
│   └───js
|       └───vendor
│   
└───src
│   └───css
│   └───js
|       └───vendor
│   └───scss
│         └───_modules
│         └───vendor
│                └───bootstrap
│                └───fontawesome
│                └───slick

```

dove:

>__/src__ sta per *source* ed all'interno ci sono tutti i file sorgente, non compilati e non minimizzati. Non è necessario caricare questa cartella in produzione.

>__/dist__ sta per *distribution* ed all'interno ci sono i file compilati, minimizzati o compressi. Questa cartella va pubblicata in produzione.

>__/assets__ cartella per immagini, font,  video e tutti gli assets del sito.  

## Inclusione librerie e consegna sorgenti

Nel file *index.html* vengono inseriti i riferimenti soltanto ai file compilati dentro /dist. Notiamo anche che:

> per ridurre le chiamate HTTP si preferisce includere le librerie direttamente dentro le cartelle di progetto (vedi cartelle /vendor), invece di usare le CDN pubbliche.

>__Attenzione__: l'inclusione dei file va fatta esattamente così come viene indicato dal template base e vanno consegnati sempre progetti sia con i sorgenti non compilati, sia i file di distribuzione compilati ed, eventualmente, minimizzati. 

Ricevere o fornire soltanto file compilati e minimizzati __creerà sicuramente diverse difficoltà ai programmatori o a chi fa maintenance__, perciò è necessario preparare tutti gli strumenti che ci permettono di velocizzare questi interventi.
