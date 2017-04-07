# api documentation for  [jshint-stylish (v2.2.1)](https://github.com/sindresorhus/jshint-stylish#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-jshint-stylish.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-jshint-stylish) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-jshint-stylish.svg)](https://travis-ci.org/npmdoc/node-npmdoc-jshint-stylish)
#### Stylish reporter for JSHint

[![NPM](https://nodei.co/npm/jshint-stylish.png?downloads=true)](https://www.npmjs.com/package/jshint-stylish)

[![apidoc](https://npmdoc.github.io/node-npmdoc-jshint-stylish/build/screenCapture.buildNpmdoc.browser.%2Fhome%2Ftravis%2Fbuild%2Fnpmdoc%2Fnode-npmdoc-jshint-stylish%2Ftmp%2Fbuild%2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-jshint-stylish/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-jshint-stylish/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-jshint-stylish/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Sindre Sorhus",
        "email": "sindresorhus@gmail.com",
        "url": "sindresorhus.com"
    },
    "bugs": {
        "url": "https://github.com/sindresorhus/jshint-stylish/issues"
    },
    "dependencies": {
        "beeper": "^1.1.0",
        "chalk": "^1.0.0",
        "log-symbols": "^1.0.0",
        "plur": "^2.1.0",
        "string-length": "^1.0.0",
        "text-table": "^0.2.0"
    },
    "description": "Stylish reporter for JSHint",
    "devDependencies": {
        "jshint": "^2",
        "mocha": "*",
        "xo": "*"
    },
    "directories": {},
    "dist": {
        "shasum": "242082a2c035ae03fd81044e0570cc4208cf6e61",
        "tarball": "https://registry.npmjs.org/jshint-stylish/-/jshint-stylish-2.2.1.tgz"
    },
    "engines": {
        "node": ">=0.10.0"
    },
    "files": [
        "index.js"
    ],
    "gitHead": "586e78216381545e3d55f8b04bd986f54bf6658d",
    "homepage": "https://github.com/sindresorhus/jshint-stylish#readme",
    "keywords": [
        "jshint",
        "reporter",
        "formatter",
        "format",
        "lint",
        "validate",
        "stylish",
        "elegant",
        "pretty"
    ],
    "license": "MIT",
    "maintainers": [
        {
            "name": "sindresorhus",
            "email": "sindresorhus@gmail.com"
        }
    ],
    "name": "jshint-stylish",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/sindresorhus/jshint-stylish.git"
    },
    "scripts": {
        "test": "xo && mocha"
    },
    "version": "2.2.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module jshint-stylish](#apidoc.module.jshint-stylish)
1.  [function <span class="apidocSignatureSpan">jshint-stylish.</span>reporter (result, config, options)](#apidoc.element.jshint-stylish.reporter)



# <a name="apidoc.module.jshint-stylish"></a>[module jshint-stylish](#apidoc.module.jshint-stylish)

#### <a name="apidoc.element.jshint-stylish.reporter"></a>[function <span class="apidocSignatureSpan">jshint-stylish.</span>reporter (result, config, options)](#apidoc.element.jshint-stylish.reporter)
- description and source-code
```javascript
reporter = function (result, config, options) {
		var total = result.length;
		var ret = '';
		var headers = [];
		var prevfile;
		var errorCount = 0;
		var warningCount = 0;

		options = options || {};

		ret += table(result.map(function (el, i) {
			var err = el.error;
			// E: Error, W: Warning, I: Info
			var isError = err.code && err.code[0] === 'E';

			var line = [
				'',
				chalk.gray('line ' + err.line),
				chalk.gray('col ' + err.character),
				isError ? chalk.red(err.reason) : chalk.blue(err.reason)
			];

			if (el.file !== prevfile) {
				headers[i] = el.file;
			}

			if (options.verbose) {
				line.push(chalk.gray('(' + err.code + ')'));
			}

			if (isError) {
				errorCount++;
			} else {
				warningCount++;
			}

			prevfile = el.file;

			return line;
		}), {
			stringLength: stringLength
		}).split('\n').map(function (el, i) {
			return headers[i] ? '\n' + chalk.underline(headers[i]) + '\n' + el : el;
		}).join('\n') + '\n\n';

		if (total > 0) {
			if (errorCount > 0) {
				ret += '  ' + logSymbols.error + '  ' + errorCount + ' ' + plur('error', errorCount) + (warningCount > 0 ? '\n' : '');
			}

			ret += '  ' + logSymbols.warning + '  ' + warningCount + ' ' + plur('warning', total);

			if (options.beep) {
				beeper();
			}
		} else {
			ret += '  ' + logSymbols.success + ' No problems';
			ret = '\n' + ret.trim();
		}

		console.log(ret + '\n');
	}
```
- example usage
```shell
...

### [gulp-jshint](https://github.com/spalger/gulp-jshint)

'''js
gulp.task('default', () =>
	gulp.src(['file.js'])
		.pipe(jshint('.jshintrc'))
		.pipe(jshint.reporter('jshint-stylish'))
);
'''

### [grunt-contrib-jshint](https://github.com/gruntjs/grunt-contrib-jshint)

'''js
grunt.initConfig({
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
