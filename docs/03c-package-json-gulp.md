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
  "name": "gulpstartup", // Cambiare con nome cliente
  "version": "1.0.0",
  "description": "Gulp Startup", // Cambiare con descrizione progetto
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
    "gulp-tfs": "0.0.9",
    "gulp-sass": "^3.1.0",
    "gulp-sourcemaps": "^2.6.4",
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

Inoltre verrà creato un __package-lock.json__, che viene autogenerato e serve per evitare doppie installazioni di moduli e inclusioni. Non avremo la necessità di modificarlo, tuttavia è necessario avere l'ultima versione di npm per renderlo leggibile. Nel paragrafo __Altri comandi utili__ qui sotto, spieghiamo come aggiornare npm. 

## Gulp.js
Tra i moduli che troviamo in devDependencies del package.json, ne troviamo alcuni con la dicitura gulp, che è un task runner.

> [Gulp.js](https://gulpjs.com/) è un toolkit JavaScript open-source di Fractal Innovations e la comunità open source di GitHub. È un esecutore di compiti costruito su Node.js e npm, utilizzato per l'automazione di attività ripetitive che richiedono tempo, coinvolte nello sviluppo del web come la minificazione, la concatenazione, il busting della cache, il test di unità, il linting, l’ottimizzazione ecc.
Nel caso in cui Gulp non sia stato ancora installato:

```
npm install gulp-cli -g
npm install gulp -D
```

Per avviare i task del gulpfile, è necessario scrivere nella console:

```
npm gulp
```

Se è stato fatto tutto correttamente, si avvieranno una serie di task, tra cui quello del webserver locale sulla porta 40000 con tanto di watcher dei file sass e js.

## Altri comandi utili

In questo caso abbiamo già inizializzato e configurato tutto quanto all'interno del nostro template blank. Tuttavia potreste trovarvi nella situazione di dover inizializzare un package.json tutto vostro, ed è possibile farlo con:

```
npm init
```

Questo attiverà un mini wizard che vi permetterà di creare il vostro personale package.json. 

----

Se voleste installare un pacchetto singolo ed aggiungerlo al vostro package.json in automatico, basta aggiungere la desinenza --save-dev:

```
npm install sass-module --save-dev
```

----

Potremmo avere la necessità di aggiornare i pacchetti del gulpfile, ed è possibile farlo in questo modo:

```
npm i -g npm-check-updates
ncu -u
npm install
```

----

Se volessimo aggiornare il package manager npm:

```
npm i -g npm-upgrade
```

----

Se invece avessimo aggiornato di recente node.js o npm (per vedere la versione installa basta scrivere node -v o npm -v) alcuni moduli potrebbero essere da ricompilare. 
In particolare ci è capitato spesso con il modulo node-sass e si sistema scrivendo:

```
npm rebuild node-sass
```

Per aggiornare un solo pacchetto all'ultima versione (sostituire node-sass con nome del pacchetto):

```
npm install node-sass@latest --save-dev
```



Viene comunque sempre indicato dalla console il modulo da ricompilare, basterà usare il comando cambiando il nome in questione.

----

>Quando riapriamo un progetto vecchio o facciamo questo tipo di aggiornamenti, una delle soluzioni è eliminare completamente la cartella __node_modules__ e rieseguire un _npm install_ così da inizializzare il tutto da zero.


Ora invece andiamo a vedere più nel dettaglio il gulpfile.
