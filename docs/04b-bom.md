---
id: bom
title: Progetto Bom
sidebar_label: Progetto Bom
---

Il __BOM__ è un gestore di contenuti sviluppato e di proprietà di Websolute. E' molto potente, solido e personalizzabile. Per questo motivo viene spesso utilizzato per progetti di una certa complessità. E' sviluppato in *dotnet* e *aspnet* ed installato su ambienti windows. In questo caso, solitamente, usiamo TFS per il versionamento dei file. In alcuni progetti viene integrato anche con git.

Per integrare nel BOM il [progetto blank ](progetto-frontend) che ci è servito per sviluppare i primi montaggi statici, dobbiamo apportare alcune modifiche che vediamo di seguito.


La struttura rimane molto simile al boilerplate base. Vediamo più nel dettaglio cosa cambia.

---

## Alberatura

L'alberatura è pressochè identica. Avremo in src i sorgenti sass e js, mentre in dist tutti gli assets, i css e i js compilati. 

Per accedere e vedere con il browser i montaggi, basterà andare nell'url raggiungendo direttamente il file, che verrà risolto senza problemi (es: http://nomesito.it/dist/homepage.chtml)


```

project
│
└───dist
│   └───assets
│       └───img
│       └───fonts
│   └───css
|       └───vendor
│   └───js
|       └───vendor
|   └───partials
|       └───static-header.cshtml
|       └───static-footer.cshtml
|   └───static-homepage.cshtml
│   
└───src
│   └───js
|       └───vendor
│   └───scss
│         └───_modules
│         └───vendor
│                └───bootstrap
│                └───fontawesome
│                └───slick
|
|

```


Essendo l'ambiente *dotnet*, potremo utilizzare delle inclusioni di file come l'*head* o il *footer*, elementi comuni a tutti i template statici. 
Per questo abbiamo modificato l'estensione dei file da .html a .cshtml, cioè inin *dotnet*. Per una maggiore chiarezza, abbiamo deciso di usare la convenzione *static-nomepagina.php* per non confonderci con i file template del bom. 

All'interno della cartella __/dist__ troviamo i template principali con all'interno il codice di inclusione dei partial interessati, che troviamo nella __/dist/partials__ 

>NB: i __partials__ sono indipendenti e ad uso e consumo soltanto dei file presenti in __/dist__ e non dei layout del BOM.

```
MANCA LA FUNZIONE DI INCLUSIONE
```

>Questo offre un grande vantaggio poichè, se ad esempio dovessimo modificare il footer di tutti i montati statici, potremo farlo cambiando un solo file.

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
        './dist/css/*.css'
    ])
      .pipe(tfs.checkout())
});
```

```
gulp.task('checkout:js', function () {
    return gulp.src([
        './dist/js/*.js',
    ])
    .pipe(tfs.checkout())
});
```

## task checkout:all

__cosa fa__: fa il checkout di tutti i file css nella cartella dist per abilitare i permessi di scrittura.

```
gulp.task('checkout:all', function () {
    return gulp.src([
        './dist/css/*.css',
        './dist/css/**/.css',
        './dist/js/*.js',
        './dist/js/**/*.js',
    ])
    .pipe(tfs.checkout())
});
```

---

Per il resto rimane tutto invariato al boilerplate generico.