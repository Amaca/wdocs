---
id: wordpress
title: Progetto Wordpress
sidebar_label: progetto Wordpress
---

Oltre al [BOM](bom), Websolute sviluppa molti siti web basati su [Wordpress](https://it.wordpress.org/), la nota piattaforma di blogging divenuta ormai un vero e proprio CMS grazie all'utilizzo di plug-in come [Advanced Custom Fields](https://www.advancedcustomfields.com/). 

Vogliamo quindi integrare il nostro boilerplate anche in un tema wordpress.

Il core di WP è scritto in php e i file sono versionati con GIT. 
Una volta scaricati i file di progetto configurati dagli sviluppatori, come prima cosa dobbiamo copiare i nostri file all'interno del tema WP all'interno di __/wp-content/themes/nometema__

---

Accedendo all'url direttamente da browser, la pagina non verrà risolta, diversamente da quanto succede sul BOM.

Dovremo quindi usare il motore di routing di WP per potervi accedere da url. Come?

1. Creare dei file .php all'interno della cartella __/dist__. 
2. Definire un __modello__ di wordpress con un semplice codice php all'interno di essi.
3. Aprire un nuovo documento dal back-end di WP, agganciare il nuovo modello e pubblicare il post.

Andiamo a vedere passo passo questo procedimento.

## 1. File php dentro /montaggi

Questa è l'alberatura del progetto:

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
|       └───static-header.php
|       └───static-footer.php
|   └───static-homepage.php
|   └───static-contact.php
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
```

All'interno di __/dist__ troviamo alcuni file esemplificativi come *static-homepage.php* e *static-contact.php*. Per una maggiore chiarezza, abbiamo deciso di usare la convenzione *static-nomepagina.php* per non confonderci con i file del core di wp. 

>NB: i template php in __/dist__ e in __partials__ non hanno niente a che vedere con i file del tema di wordpress come *header.php* o *footer.php*. Sono indipendenti e ad uso e consumo soltanto dei file presenti in __/dist__.

__Possiamo includere dei partials allo stesso modo del pacchetto BOM__, così da facilitare le modifiche, ma sfruttando delle funzioni php:

```
<?php
include 'partials/header.php';
?>
```

## 2. Definire modello WP

All'inizio dei file esemplificativi *static-homepage.php* dobbiamo inserire una dicitura di questo tipo:

```
<?php
/**
 * Template Name: Static Homepage
 */
?>    
```

Inserendo esattamente quella dicitura nei file, ma cambiando la dicitura "Static Homepage" con la convenzione "Static Nomepagina", attiveremo un nuovo modello di Wordpress.

## 3. Nuovo documento e scelta del modello

Ora che abbiamo il nostro modello attivo, dobbiamo:
* accedere al backend di WP 
* creare un nuovo documento di __tipo pagina__ 
* dare un nome al documento con convenzione "Static Nomepagina"
* scegliere il nuovo modello "Static Nomepagina" con la select dedicata
* pubblicare la pagina

A questo punto potremo accedere tranquillamente al nostro montaggio statico via url. 

>Il permalink viene indicato da WP una volta pubblicato, ma se avete seguito tutto per filo e per segno seguendo le convenzioni consigliate, dovrebbe essere http://nomesito.it/static-nomepagina 


---


