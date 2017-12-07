Ultra simple hello world - demo
===============================

This is a live demo of the tutorial code described on [the ultra simple hello world tutorial page](../uniter/ultra_simple_hello_world.html).  

---

## Change the text below by clicking a button!

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

<!--<script src="https://asmblah.github.io/uniter/dist/uniter.js"></script>-->
<script src="http://localhost:5000/dist/uniter.js"></script>
