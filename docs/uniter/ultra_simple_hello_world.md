Ultra simple hello world
========================

> NB: This technique is not recommended for production apps -
> you'll want [a Webpack-based setup](./webpack_hello_world.html) for that.
>
> (_it does work great for putting together something like a single-file proof-of-concept though._) 

In this example we're going to create a simple HTML page with some text and two buttons,
then attach a click listener to each button that changes the text displayed -
but we're going to do it using _only_ PHP, no JavaScript will be written at all.

You should not use this mode in production - it results in the PHP being transpiled to JavaScript
on the fly when the page is loaded, which will be slower. However, it's great for throwing together
a quick proof of concept when you need to test something fast.

Step 1
------
Create your HTML page `index.html`:

```html
<html>
    <head>
        <title>Ultra simple hello world - demo</title>
    </head>
    <body>
        <h1>Ultra simple hello world - demo</h1>
        
        <h2>Change the text below by clicking a button!</h2>

        <p id="myMessage">Click a button to change me!</p>

        <button type="button" id="helloButton">Hello!</button>
        <button type="button" id="worldButton">World!</button>
        
        <script type="text/x-uniter-php">
            $messageBox = $document->getElementById('myMessage');
        
            $document->getElementById('helloButton')->addEventListener('click', function () use ($messageBox) {
                $messageBox->textContent = 'You clicked Hello!';
            });
        
            $document->getElementById('worldButton')->addEventListener('click', function () use ($messageBox) {
                $messageBox->textContent = 'You clicked World!';
            });
        </script>

        <script src="https://asmblah.github.io/uniter/dist/uniter.js"></script>
    </body>
</html>
```

[See it in action here.](./ultra_simple_hello_world_demo.html)

Step 2
------
Open it in a browser - and that's it!

- Clicking on `Hello!` should change the message displayed to `You clicked Hello!`
- Clicking on `World!` should change the message displayed to `You clicked World!`

How does it work?
-----------------
This approach embeds all the components of Uniter needed to parse, transpile and execute
the PHP code you embed on the page in those special `<script>` tags. This makes it super easy to set up,
but it does mean your bundle cannot take advantage of the Ahead-Of-Time transpile and will be bloated
with those components (the parser/transpiler would never normally make it to the browser-side).
