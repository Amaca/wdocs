---
id: gulpfile-task
title: I task del gulpfile.js
sidebar_label: I task del gulpfile.js
---

Apriamo il file gulpfile.js e analizziamo i task al suo interno. I task sono procedure automatizzate che si attivano quando decidiamo noi. 

## gulp

Il task principale, quello di default, si attiva come anticipato con:

```
gulp
```

Questo è definito alla fine del gulpfile.js e attiva diversi task:

```
gulp.task('default', [
    //build and minify
    'minify',
    //vendor
    'sass:vendor',
    'js:vendor',
    //watch
    'sass:watch',
    'css:watch',
    'js:watch',
    //VARIOUS
    'webserver'
]);
```

Andiamo a vedere i task principali:

## task sass

__cosa fa__: prende il main.scss (il sass principale che importa tutti i moduli secondari) dalla cartella /src/scss , lo compila e crea il /dist/main.css applicandogli gli [autoprefixer](https://www.npmjs.com/package/gulp-autoprefixer), la [sourcemap](https://www.npmjs.com/package/gulp-sourcemaps) e un'header definita nel gulpfile stesso

```
gulp.task('sass', function () {
    console.log('COMPILING SASS');
    return gulp.src(
        './src/scss/main.scss'
    )
    .pipe(plumber(function (error) {
        console.log('sass error: compile plumber', error);
    }))
    .pipe(header(head))
    .pipe(sourcemaps.init())
    .pipe(sass().on('error', sass.logError))
    .pipe(autoprefixer({
        browsers: ['last 2 versions', 'Explorer >= 11', 'Android >= 4.1', 'Safari >= 7', 'iOS >= 7'],
        cascade: false
    }))
    .pipe(sourcemaps.write())
    .pipe(rename({ dirname: '' }))
    .pipe(gulp.dest('./dist/css/'))
   
});
```

## task sass:vendor

__cosa fa__: compila tutti i file scss nella cartella src/scss/vendor/ e li mette in dist/css/vendor

```
gulp.task('sass:vendor', function () {
    console.log('COMPILING SASS VENDOR');
    return gulp.src(
        './src/scss/vendor/**/*.scss'
    )
    .pipe(plumber(function (error) {
        console.log('sass error: compile plumber', error);
    }))
    .pipe(sourcemaps.init())
    .pipe(sass().on('error', sass.logError))
    .pipe(autoprefixer({
        browsers: ['last 2 versions', 'Explorer >= 11', 'Android >= 4.1', 'Safari >= 7', 'iOS >= 7'],
        cascade: false
    }))
    .pipe(sourcemaps.write())
    .pipe(rename({ dirname: '' }))
    .pipe(gulp.dest('./dist/css/vendor'))

});
```

## task sass:watch

__cosa fa__: rimane in ascolto in attesa di modifiche su tutti i file .scss presenti nella cartella /src/scss e nei sui figli e attiva il task *sass* al cambiamento

```
gulp.task('sass:watch', function () {
    var watcher = gulp.watch('./src/scss/**/*.scss', ['sass']); 
    watcher.on('change', function (e) {
        console.log('watcher.on.change type: ' + e.type + ' path: ' + e.path);
    });
    return watcher;
});
```

## task css

__cosa fa__: copia tutti i file .css da src/css a dist/css

```
gulp.task('css', function () {
    return gulp.src('./src/css/**/*.css')
        .pipe(gulp.dest('./dist/css/'));
});
```

## task css watch

__cosa fa__: rimane in ascolto in attesa di modifiche su tutti i file .css presenti nella cartella /src/css e attiva il task *css:minify* al cambiamento

```
gulp.task('css:watch', function () {
    var watcher = gulp.watch('./src/css/**/*.css', ['css:minify']);
    watcher.on('change', function (e) {
        console.log('watcher.on.change type: ' + e.type + ' path: ' + e.path);
    });
    return watcher;
});
```

## task js

__cosa fa__: copia tutti i file javascript in src/dist esclusi i vendor e li mette in dist/js
```
gulp.task('js', function () {
    console.log('COMPILING JS');
    return gulp.src([
        './src/js/**/*.js',
        '!./src/js/vendor/**/*.js'
    ])
    .pipe(header(head))
    .pipe(plumber(function (error) {
        console.log('js error: compile plumber', error);
    }))
    .pipe(gulp.dest('./dist/js'))
});
```

## task js:vendor

__cosa fa__: compila tutti i file js presenti in src/js/vendor eccetto jquery e li mette in dist/js/vendor
```
gulp.task('js:vendor', function () {
    console.log('COMPILING VENDOR JS');
    return gulp.src(
        './src/js/vendor/**/*.js'
    )
    .pipe(plumber(function (error) {
        console.log('js error: compile plumber', error);
    }))
    .pipe(gulp.dest('./dist/js/vendor'))
});
```

## task js:watch

__cosa fa__: rimane in ascolto in attesa di modifiche sui file javascript in src/js/ esclusi i vendor
```
gulp.task('js:watch', function () {
    var watcher = gulp.watch([
        './src/js/**/*.js',
        '!./src/js/vendor/**/*.js'
    ], ['js:minify']);
    watcher.on('change', function (e) {
        console.log('watcher.on.change type: ' + e.type + ' path: ' + e.path);
    });
    return watcher;
});
```

## webserver
__cosa fa__: attiva un webserver locale sulla porta 40000 e apre il browser. Ad ogni modifica dei file, si attiva il livereload che aggiorna la pagina automaticamente.

```
gulp.task('webserver', function () {
    return gulp.src('./')
        .pipe(webserver({
            livereload: true,
            directoryListing: false,
            port: 40000,
            open: true
        }));
});
```

***

Oltre ai task precedenti che si attivano automaticamente con il comando *gulp* ne abbiamo altri "secondari" che non devono attivarsi sempre per motivi di prestazioni e velocità di compilazione, ma ugualmente molto utili. Essi sono gulp:minify e gulp:publish che entrambi attivano altri task che vediamo di seguito.

## gulp minify

Attiva una serie di task creati per minimizzare i file compilati. Si attiva da console in questo modo:

```
gulp minify
```

E attiva i seguenti task:

```
gulp.task('minify', [
    'css:minify',
    'css:vendor-minify',
    'js:minify',
    'js:vendor-minify'
]);
```

## task sass:minify

__a cosa serve__: prima attiva il task sass (quindi compila i sass e crea il main.css in dist), copia il file di stile compilato, lo minimizza e lo chiama dist/css/main.min.css

```
gulp.task('sass:minify', ['sass'], function () {
    console.log('MINIFYING SASS');
    return gulp.src(
        './dist/css/main.css'
    )
    .pipe(cssmin())
    .pipe(rename({ suffix: '.min' }))
    .pipe(gulp.dest('./dist/css'));
});
```

## task sass:vendor-minify

__a cosa serve__: prima attiva il task sass:vendor (quindi compila i file di stile dei vendor e li mette in dist), poi li copia, li minimizza e li mette in dist/css/vendor/**.min.css

```
gulp.task('sass:vendor-minify', ['sass:vendor'], function () {
    console.log('MINIFYING VENDOR SASS');
    return gulp.src(
        './dist/css/vendor/**/*.css'
    )
    // minify
    .pipe(cssmin())
    .pipe(concat('vendor.min.css'))
    .pipe(gulp.dest('./dist/css/vendor'));
});
```


## task css minify

__cosa fa__: unisce e minimizza tutti i file css presenti in dist/css escludendo i vendor. il file main.css viene messo per ultimo nel bundle.

```
gulp.task('css:minify', ['css', 'sass'], function () {
    console.log('MINIFYING CSS');
    return gulp.src([
        './dist/css/**/*.css',
        '!./dist/css/main.css',
        '!./dist/css/vendor/**/*.css',
        './dist/css/main.css'
    ])
    .pipe(cssmin())
    .pipe(concat('main.min.css'))
    .pipe(gulp.dest('./dist/css'));
});
```

## task css vendor minify

__cosa fa__: unisce e minimizza tutti i file css presenti in dist/css/vendor.

```
gulp.task('css:vendor-minify', ['sass:vendor'], function () {
    console.log('MINIFYING VENDOR CSS');
    return gulp.src(
        './dist/css/vendor/**/*.css'
    )
    // minify
    .pipe(cssmin())
    .pipe(concat('vendor.min.css'))
    .pipe(gulp.dest('./dist/css/vendor'));
});
```

## task js:minify

__a cosa serve__: prima attiva il task js (quindi copia tutti i file js da src/js a dist/js), li unisce escludendo i vendor, minimizza e chiama il nuovo file dist/js/main.min.js. il file main.js viene messo per ultimo nel bundle.
```
gulp.task('js:minify', ['js'], function () {
    console.log('MINIFY JS')
    return gulp.src([
        './src/js/**/*.js',
        '!./src/js/main.js',
        '!./src/js/vendor/**/*.js',
        './src/js/main.js'
    ])
    .pipe(concat('main.min.js'))
    .pipe(uglify().on('error', function (e) {
        console.log(e);
    }))
    .pipe(gulp.dest('./dist/js'))
})
```

## task js:vendor-minify

__a cosa serve__: prima attiva il task js:vendor (quindi compila i file js dei vendor e li mette in dist), poi li concatena in un solo file minimizzato che viene messo in dist/js/vendor/vendor.min.js
```
gulp.task('js:vendor-minify', ['js:vendor'], function () {
    console.log('MINIFY VENDOR JS')
    return gulp.src([
        './dist/js/vendor/!(jquery-)*.js'
    ])
    .pipe(uglify().on('error', function (e) {
        console.log(e);
    }))
    .pipe(concat('vendor.min.js'))
    .pipe(gulp.dest('./dist/js/vendor'));
})
```

***

## Note

* E' possibile modificare il gulpfile a seconda delle esigenze, ma indicativamente la base è questa. 
* I task che non vengono utilizzati possono essere commentati dai task principali *default* e *minify* così da velocizzare le operazioni.
* I task di minimizzazione possono essere messi in quelli di compilazione, così da minimizzarli ad ogni aggiornamento dei file.