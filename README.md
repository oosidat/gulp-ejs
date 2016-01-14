# gulp-ejs

*This is a fork of [Rogério Vicente's gulp-ejs](https://github.com/rogeriopvl/gulp-ejs) plugin, modified to have different default behaviour regarding file extensions.*

> ejs plugin for [gulp](https://github.com/wearefractal/gulp)

## Usage

First, install `gulp-ejs` as a development dependency:

```shell
npm install --save-dev gulp-ejs
```

Then, add it to your `gulpfile.js`:

```javascript
var ejs = require("gulp-ejs");

gulp.src("./templates/*.ejs")
	.pipe(ejs({
		msg: "Hello Gulp!"
	}))
	.pipe(gulp.dest("./dist"));
```
If you want to use `gulp-ejs` in a watch/livereload task, you may want to avoid gulp exiting on error when, for instance, a partial file is `ENOENT`.
Here's an example on how to make it work:

```javascript
var ejs = require('gulp-ejs');
var gutil = require('gulp-util');

gulp.src('./templates/*.ejs')
	.pipe(ejs({
		msg: 'Hello Gulp!'
	}).on('error', gutil.log))
	.pipe(gulp.dest('./dist'));
```
This will make gulp log the error and continue normal execution.

## API

### ejs(options, settings)

#### options
Type: `hash`
Default: `{}`

A hash object where each key corresponds to a variable in your template. Also you can set ejs options in this hash.

For more info on `ejs` options, check the [project's documentation](https://github.com/visionmedia/ejs).

**Note:** As of `v1.2.0`, `file.data` is supported as a way of passing data into ejs. See [this](https://github.com/colynb/gulp-data#note-to-gulp-plugin-authors).

#### settings
Type: `hash`
Default: `{}`

A hash object to configure the plugin.

##### settings.ext
Type: `String`
Default: `undefined`

Defines the file extension that will be appended to the filename.

###### Example

**Not specifying extension:**

```javascript
var ejs = require("gulp-ejs");

gulp.src("./templates/hello.myrandomextension")
	.pipe(ejs())
	.pipe(gulp.dest("./dist"));
```

will produce file: `dist/hello.myrandomextension`

**Specifying extension:**

```javascript
var ejs = require("gulp-ejs");

gulp.src("./templates/hello.myrandomextension")
	.pipe(ejs({}, { ext: '.html'}))
	.pipe(gulp.dest("./dist"));
```

will produce file: `dist/hello.html`


## License

[MIT License](http://en.wikipedia.org/wiki/MIT_License)
