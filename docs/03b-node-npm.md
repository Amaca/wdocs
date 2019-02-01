---
id: node-npm
title: Node e npm
sidebar_label: Node e npm
---

Sulla root del tema blank troviamo due file particolarmente importanti: il *package.json* e il *gulpfile.js*

Nel primo sono elencati i moduli *node* che verranno installati tramite il package manager *npm*, mentre nel secondo la lista dei task che ci permetteranno di compilare i sorgenti della cartella /src nella cartella /dist di produzione.

Giusto per sapere di cosa stiamo parlando, vediamo insieme brevemente le definizioni di node e npm.

## Node

>[Node.js](https://nodejs.org/) è un framework che viene usato per scrivere applicazioni in Javascript lato server. Il codice su Node.js viene fatto girare da V8, il motore JavaScript open source di Google, scritto in C ++ e utilizzato in Google Chrome. 
Si tratta di una soluzione lato server basata su un modello di I/O asincrono che opera sugli eventi. In buona sintesi, mentre Node.js sta elaborando una procedura, mentre aspetta che venga portata a termine può partire già con altre operazioni.

Nel nostro progetto base useremo node soltanto per installare dei pacchetti tramite il package manager *npm*. Ciò nonostante sarà necessario installare node nel vostro computer. Il pacchetto di installazione è scaricabile sul [sito ufficiale](https://nodejs.org/en/download/) ed è compatibile con tutti i sistemi operativi.

## npm

Una volta installato node.js, potremo usare npm. 

>[npm](https://docs.npmjs.com) è il package manager di default di node.js. Grazie ad esso, da linea di comando, è possibile installare dei moduli presenti nel database ufficiale pubblico chiamato *npm registry*

__Facciamo un esempio pratico.__ Se volessimo installare l'ultima versione di jQuery in una cartella, basterà aprire la console in essa e digitare:

```
npm install jquery
```

In pochi secondi npm creerà una cartella chiamata __/node_modules__ e scaricherà all'interno la libreria jQuery.  

## Altri package manager e bundler

Sebbene npm è quello attualmente più usato in Websolute, ci sono altri package manager:
* [Yarn](https://yarnpkg.com/lang/en/): permette un'installazione molto rapida dai pacchetti, gestisce solidamente le versioni delle librerie ed è compatibile con il tema blank websolute (vedi file *yarn.lock*)
* [Bower](https://bower.io/): l'uso di Bower è da evitare poichè gli stessi creatori ne hanno abbandonato lo sviluppo.
* [Webpack](https://webpack.js.org/) o [Browseriy](http://browserify.org/): sono dei module bundler o, in altre parole, dei strumenti di compilazione. Forniscono *loaders* e *plug-in* che consentono di preparare le dipendenze dei file statici per i progetti Web. Sono principalmente utilizzati per web app o progetti complessi.

>__Webpack__ è già usato in Websolute su alcuni progetti avanzati e, probabilmente, sarà presto necessario integrarlo nel tema blank rendendolo uno standard.

Non ci resta che scoprire come istallare i pacchetti del boilerplate.