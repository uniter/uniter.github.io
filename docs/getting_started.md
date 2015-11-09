# Getting started with Uniter

You can use Uniter in more than one way:

- inside NodeJS, or
- inside the Browser.

## Uniter in the browser
In order to build your PHP code for the browser, you will be needing a build tool. Currently, there is a basic Browserify transform called `phpify`. It maps out all of your dependencies and loads them, plus the runtime, into one output bundle.

To install, we first need to have `browserify` installed:

```
npm -g install browserify
```

If you are on a UNXI system, such as Mac OS X or Linux, you may need to prefix the above command with `sudo`. But if you plan to use Browserify as a local program, you are advised to edit your `package.json` file:

```json
{
    "name": "your-project",
    "version": "0.0.0",
    "scripts": {
        "browserify": "browserify"
    }
}
```

Now, use this command instead:

```
npm install --save-dev browserify
```

And you are good to go with a local copy of browserify. A regular install of your package won't include it - if you want, change `--save-dev` to `-save`. In most cases, you won't need this.

Now, we need to install the actual transformer that will run your PHP code through Uniter:

```
npm install --save-dev phpify
```

Done. Now all you need to do is put together a basic little Uniter project. You can find a demo here: [Uniter/phpify-demo](https://github.com/uniter/phpify-demo) (Note: Yes, we are working on a WebPack compatible version. Don't get confused by the existence of `webpack.config.js` just yet.)

## Uniter in NodeJS
Using Uniter in NodeJS is super straight forward:

1. Install `uniter-node`: `npm install --save uniter-node`
2. In your main JS file, like `app.js`, register Uniter.
3. Require any PHP file like your usual JS files, they'll just work!

To register Uniter with NodeJS, all you have to do is something like this:

```javascript
require("uniter-node")();
```

And that's it.

```javascript
var PhpModule = require("./my_php_module.php");
// Or you can ommit the extension
var PhpModule2 = require("./module2"); // ./module2.php
```

Within Uniter PHP, you can export values just like you would expect:

```php
<?php
$module->exports->myString = "Hello, World!";
```
