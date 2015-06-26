# Working With Gulp
[Gulp](http://gulpjs.com) is a JavaScript task runner, frequently used for building your site's JavaScript, CSS, and more. Because there is a [gulp-sass](https://github.com/dlmanning/gulp-sass) plugin that uses `node-sass`, we can integrate eyeglass by using its `require` to wrap the `node-sass` options.

```js
var gulp = require("gulp");
var sass = require("gulp-sass");

var eyeglass = require("eyeglass")({
  // ... node-sass options
    importer: function(uri, prev, done) {
        done(sass.NULL);
    }
});

// Disable import once with gulp until we
// figure out how to make them work together.
eyeglass.enableImportOnce = false

gulp.task("sass", function () {
  gulp.src("./sass/**/*.scss")
    .pipe(sass(eyeglass.sassOptions()).on("error", sass.logError))
    .pipe(gulp.dest("./css"));
});
```