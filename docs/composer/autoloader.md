Composer autoloader
===================

Uniter fully supports taking the dependencies you install with Composer
and transpiling them to JavaScript to run in the browser.
It does this by taking all the code in the following places...

- Composer output in the `vendor/composer/*` folder,
- Composer's `vendor/autoload.php` and
- any dependencies you wish to include under `vendor/*`

... transpiling all of it to JavaScript and including it in your JS bundle.

As an example, you can use Composer to install the Symfony EventDispatcher component
as you would normally, but then you can require Composer's autoloader and create an `EventDispatcher`
to dispatch or listen for events on the browser side.
> See the [EventDispatcher demo](https://github.com/uniter/event-dispatcher-demo) for a working example.
