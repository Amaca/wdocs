---
id: package-json-gulp
title: package.json e gulp.js
sidebar_label: package.json e gulp.js
---

Ora che sappiamo a cosa serve npm, possiamo procedere con l'installazione dei pacchetti del nostro tema base, così da poter utilizzare una serie di strumenti utili ai fini dello sviluppo. 

In particolare la __compilazione e minimizzazione del javascript e dei moduli sass__ che generano i file di stile.
Parleremo nel capitolo *produzione dei template e convenzioni* di questi vantaggi.

## package.json
Nella root del tema troviamo un file chiamato package.json:

```
{
  "name": "gulpstartup",
  "version": "1.0.0",
  "description": "Gulp Startup",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "es6-promise": "^4.0.5",
    "gulp": "^3.9.1",
    "gulp-autoprefixer": "^4.1.0",
    "gulp-concat": "^2.6.1",
    "gulp-cssmin": "^0.2.0",
    "gulp-header": "^2.0.1",
    "gulp-imagemin": "^4.1.0",
    "gulp-plumber": "^1.1.0",
    "gulp-rename": "^1.2.2",
    "gulp-sass": "^3.1.0",
    "gulp-sourcemaps": "^2.6.4",
    //"gulp-tfs": "0.0.9",
    "gulp-uglify": "^3.0.0",
    "gulp-webserver": "^0.9.1",
    "node-sass": "^4.7.2"
  }
}
```

Grazie a questo file indicheremo a npm i moduli che deve scaricare e mettere nella cartella /node_modules. I moduli sono indicati in devDependencies.

Possiamo quindi attivare npm da console che leggerà il package.json e scaricherà i pacchetti necessari automaticamente. Rechiamoci nella root del nostro progetto, apriamo la console di comando al suo interno e digitiamo:

```
npm install
```

Se avete installato node.js ed avete aperto la console nella path giusta, npm inizierà a scaricare tutti i moduli installati nel package.json.
Dopo alcuni minuti di installazione, vedremo la cartella /node_modules completa dei moduli richiesti.

## Gulp.js
Tra quelli scritti in devDependencies, ne troviamo alcuni con la dicitura gulp, che è un task runner.

> [Gulp.js](https://gulpjs.com/) è un toolkit JavaScript open-source di Fractal Innovations e la comunità open source di GitHub. È un esecutore di compiti costruito su Node.js e npm, utilizzato per l'automazione di attività ripetitive che richiedono tempo, coinvolte nello sviluppo del web come la minificazione, la concatenazione, il busting della cache, il test di unità, il linting, l’ottimizzazione ecc.


Per avviare i task del gulpfile, è necessario scrivere nella console:

```
npm gulp
```

Se è stato fatto tutto correttamente, si avvieranno una serie di task, tra cui quello del webserver locale sulla porta 40000 con tanto di watcher dei file sass e js.

Andiamo a vedere più nel dettaglio il gulpfile.
