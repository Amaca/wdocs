---
id: bom
title: Progetto Bom
sidebar_label: Progetto Bom
---

Il __BOM__ è un gestore di contenuti sviluppato e di proprietà di Websolute. E' molto potente, solido e personalizzabile. Per questo motivo viene spesso utilizzato per progetti di una certa complessità. E' sviluppato in *dotnet* e *aspnet* ed installato su ambienti windows. In questo caso usiamo TFS per il versionamento dei file. 

Come anticipato, abbiamo preparato un pacchetto base blank alternativo a quello visto nel capitolo [progetto base front-end](progetto-frontend) ed è scaricabile al seguente link:

<a href="#" class="btn" target="_blank">Scarica BOM Starter Theme</a>

Una volta scaricati i file del progetto BOM preparato dagli sviluppatori, basterà copiare i file del progetto base BOM nella root.

In realtà è lo stesso [progetto blank ](progetto-frontend) ma adattato all'ambiente del BOM, quindi le logiche, le path e i task del gulpfile rimangono per lo più le stesse. 

Vediamo più nel dettaglio cosa cambia.

---

## Alberatura

L'alberatura è pressochè identica se non fosse per la cartella __/montaggi__ in cui andremo a mettere i nostri file html statici e non più sulla root come nalle [progetto base generico ](progetto-frontend). 

Per accedere e vedere con il browser i montaggi, basterà andare nell'url raggiungendo direttamente il file, che verrà risolto senza problemi (es: http://nomesito.it/montaggi/homepage.chtml)

```

project
│
└───dist
│   └───css
|       └───vendor
│   └───fonts
│   └───img
│   └───js
|       └───vendor
│   
└───src
│   └───fonts
│   └───img
│   └───js
|       └───vendor
│   └───scss
│         └───_modules
│         └───vendor
│                └───bootstrap
│                └───fontawesome
│                └───slick
|
└───montaggi
|    └───partials
|
|

```

Essendo l'ambiente *dotnet*, potremo utilizzare delle inclusioni di file come l'*head* o il *footer*, elementi comuni a tutti i template statici. 
Per questo abbiamo dei file che sono in *dotnet* con estensione *cshtml*. 

All'interno della cartella __/montaggi__ troviamo i template principali con all'interno il codice di inclusione dei partial interessati, che troviamo nella __/montaggi/partial__ 

>Questo offre un grande vantaggio poichè, se ad esempio dovessimo modificare il footer di tutti i montati statici, potremo farlo cambiando un solo file.

>NB: i __partials__ sono indipendenti e ad uso e consumo soltanto dei file presenti in __/montaggi__.

Chiaramente i riferimenti dei template statici ai file all'interno di /dist sono stati modificati così da adattarci in maniera adeguata alla nuova alberatura.

---

## Gulpfile e TFS

I task del gulpfile sono esattamente gli stessi, escludendo quelli relativi al versionament TFS: 
si attivano alla compilazione dei sass e dei javascript per gestire i permessi di scrittura dei file. 

> Sono già stati configurati nei task del gulpfile. I task checkout:css e checkout:js si attivano con il comando iniziale *gulp*


## task checkout:css e checkout:js

__cosa fanno:__ ad ogni compilazione, i task di TFS faranno un checkout sbloccando i permessi di scrittura sui file compilati. 

```
gulp.task('checkout:css', function () {
  return gulp.src([
      './dist/css/main.css'
  ])
    .pipe(tfs.checkout())
});
```

```
gulp.task('checkout:js', function () {
    return gulp.src([
        './dist/js/main.js'
    ])
    .pipe(tfs.checkout())
});
```

## task checkout:all

__cosa fa__: fa il checkout di tutti i file css nella cartella dist per abilitare i permessi di scrittura.

```
gulp.task('checkout:all', function () {
  return gulp.src([
      './dist/css/*'
  ])
      .pipe(tfs.checkout());
});
```

## task checkout:publish

__cosa fa__: fa il checkout di tutti i file immagine e dei font della cartella dist per abilitare i permessi di scrittura.

```
gulp.task('checkout:publish', function () {
    return gulp.src([
        './dist/img/*',
        './dist/fonts/*'
    ])
    .pipe(tfs.checkout());
});
```

---

Per il resto rimane tutto invariato al tema generico.