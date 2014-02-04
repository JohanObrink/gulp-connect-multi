# [gulp](https://github.com/wearefractal/gulp)-connect

> Gulp plugin connect to server, LiveReload and opening browser

## Install

Install with [npm](https://npmjs.org/)

```
npm install --save-dev gulp-connect
```


## Example

### connect + livereload + open + stylus
```js
var
  gulp = require('gulp'),
  watch = require('gulp-watch'),
  stylus = require('gulp-stylus'),
  connect = require('gulp-connect');

gulp.task('connect', connect.server({
  root: __dirname + '/app',
  port: 1337,
  livereload: true,
  open: {
    browser: 'chrome' // if not working OS X browser: 'Google Chrome'
  }
}));

gulp.task('html', function () {
  gulp.src('./app/*.html')
    .pipe(watch())
    .pipe(connect.reload());
});

gulp.task('stylus', function () {
  gulp.src('./app/stylus/*.styl')
    .pipe(watch())
    .pipe(stylus())
    .pipe(gulp.dest('./app/css'))
    .pipe(connect.reload());
});

gulp.task('default', ['connect', 'html', 'stylus']);
```

**all option**

```js
gulp.task('connect', connect.server({
  root: __dirname + '/app',
  port: 1337,
  livereload:{
    port: 35729
  },
  open: {
    file: 'index.html',
    browser: 'firefox'
  },
  middleware: function(connect, o) {
    return [
      // ...
    ]
  }
}));
```


###coffee

    gulp --require coffee-script/register
    
```coffee
gulp = require("gulp")
watch = require("gulp-watch")
stylus = require("gulp-stylus")
connect = require("gulp-connect")

gulp.task "connect", connect.server(
  root: __dirname + "/app"
  port: 1337
  livereload: true
  open:
    browser: "chrome"
)

gulp.task "html", ->
  gulp
    .src("./app/*.html")
    .pipe(watch())
    .pipe(connect.reload())

gulp.task "stylus", ->
  gulp
    .src("./app/stylus/*.styl")
    .pipe(watch())
    .pipe(stylus())
    .pipe(gulp.dest("./app/css"))
    .pipe(connect.reload())

gulp.task "default", [
  "connect"
  "html"
  "stylus"
]
```


## API

#### options.root

Type: `String`  
Default: `app`

The root path

#### options.port

Type: `Number`  
Default: `3000`

The connect port

#### options.livereload

Type: `Object or Boolean`  
Default: `false`

#### options.livereload.port

Type: `Number`  
Default: `35729`


#### options.open

Type: `Object`  
Default: `{}`

#### options.open.file

Type: `String`  
Default: `index.html`

The open file

#### options.open.browser

Type: `String`  
Default: `chrome`

The type of browser


## License

MIT © Vladislav Derjavin <dev@vld.me>