Webpack hello world
===================

In this example we're going to create a simple HTML page with some text and two buttons,
then attach a click listener to each button that changes the text displayed -
but we're going to do it using PHP that we'll pre-transpile to JavaScript using Webpack and the Uniter loader.

> If you're in a hurry, you can [check out the finished example here](https://github.io/uniter/webpack-hello-world).

Step 1
------
Install all the tools you're going to need:

```shell
npm install --save-dev phpify source-map-loader transform-loader babel-loader babel-core babel-preset-env webpack
```

Step 2
------
Add your PHPify config to `package.json`:

```json
{
    ...
    "phpify": {
        "phpToJS": {
            "sync": true
        }
    }
}
```

> The `sync` option enables the synchronous mode for Uniter. In most cases you'll want to stick to synchronous mode,
> but if you need to call something that may block like `usleep(...)`, you'll need to switch to async mode.
> See the [async vs sync mode]() section.

Step 3
------
Create your HTML page `index.html`:

```html
<!DOCTYPE html>
<html>
    <head>
        <title>My web page</title>
    </head>
    <body>
        <h1>My web page</h1>

        <p id="myMessage">Click a button to change me!</p>

        <button type="button" id="helloButton">Hello!</button>
        <button type="button" id="worldButton">World!</button>

        <script src="./dist/my_bundle.js"></script>
    </body>
</html>
```

Step 4
------
Create your PHP file that will return a closure to attach the buttons' behaviours, `binder.php`:

```php
<?php

print 'Hello from binder.php!';

return function ($document) {
    $messageBox = $document->getElementById('myMessage');
    
    $document->getElementById('helloButton')->addEventListener('click', function () use ($messageBox) {
        $messageBox->textContent = 'You clicked Hello!';
    });
    
    $document->getElementById('worldButton')->addEventListener('click', function () use ($messageBox) {
        $messageBox->textContent = 'You clicked World!';
    });
};
```

Step 5
------
Create your entrypoint JS file `my_app.js`:

```javascript
// Fetch the PHP module (but don't actually run it yet)
const binderModule = require('./binder.php')();

// Hook stdout and stderr up to the console
binderModule.getStdout().on('data', function (data) {
    console.info(data);
});
binderModule.getStderr().on('data', function (data) {
    console.warn(data);
});

// Run the PHP module, capture its result Closure
// and cast it to a JavaScript function we can call
const binder = binderModule.execute().getNative();

// Call the PHP closure function returned from binder.php, from JavaScript!
binder(document);
```

Step 6
------
Create your Webpack config file `webpack.config.js`:

```javascript
module.exports = {
    context: __dirname,
    entry: './my_app',
    module: {
        rules: [
            {
                // PHPify transpiles your PHP code to JavaScript,
                // so Webpack can include it in your JS bundle for you
                // and it can be run in the browser.
                test: /\.php$/,
                use: 'transform-loader?phpify'
            },
            {
                // PHPify is (at the moment) a Browserify transform and not
                // a Webpack loader, so we need to extract the source map
                // it generates and apply it to Webpack's for it to work properly.
                test: /\.php/,
                use: 'source-map-loader',
                enforce: 'post'
            },
            {
                // This is the standard Babel setup to enable ES5 support
                test: /\.js$/,
                exclude: /\bnode_modules\b/,
                use: {
                    loader: 'babel-loader?presets=env'
                }
            }
        ]
    },
    output: {
        path: __dirname + '/dist/',
        filename: 'my_bundle.js'
    }
};
```

Step 7
------

Build your bundle with Webpack:

```shell
node_modules/.bin/webpack --devtool source-map
```

You'll probably find it handy to add an NPM script for your webpack build command above.

There's one [in the complete demo repository for this example](https://github.com/uniter/webpack-hello-world/blob/master/package.json).

Step 8
------

Open `index.html` in a browser!
