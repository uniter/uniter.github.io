Uniter
======

What is it?
-----------
- it's a way to run PHP code in the browser: no server is required.
- it's a way to run PHP code in Node.js
- it provides a command called `uniter` that you can run
  in the same way as you would run Zend™'s `php` command:
  
  `uniter -r 'echo "Hello from PHP!";'`.

How do I use it?
----------------

### A really simple browser-side PHP demo
[See the demo](./docs/uniter/ultra_simple_hello_world.html) for a great way to proof-of-concept your code.
We don't recommend using this method for production work: see the Webpack section below for a proper setup.

### How do I set it up with Webpack?
[See our Webpack PHP tutorial](./docs/uniter/webpack_hello_world.html) for a walkthrough of all the steps
you need to create your first browser bundle with PHP inside. 

Where can I ask questions?
--------------------------
Feel free to join us on [![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/asmblah/uniter?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)!

How is Uniter structured?
-------------------------
Uniter is fairly large, so it's split into several packages:

[`uniter`](./uniter) is the main Uniter library (this repository).
It pulls in all the required components (below) to take a string of PHP code, evaluate it and return the result
with a simple API.
> Repo: [https://github.com/asmblah/uniter](https://github.com/asmblah/uniter)

[`phptoast`](./phptoast) is the parser for Uniter. It takes PHP code as a string
and returns an AST comprised of plain JavaScript objects.
> Repo: [https://github.com/uniter/phptoast](https://github.com/uniter/phptoast)

[`phptojs`](./phptojs) is the transpiler. It takes an AST (such as the one returned by `phptoast`)
and translates it into JavaScript
that can then be executed.
> Repo: [https://github.com/uniter/phptojs](https://github.com/uniter/phptojs)

[`phpcore`](./phpcore) is the minimal runtime library required for code transpiled by `phptojs` to execute.
It contains some builtin PHP classes and functions, but only those that are required
(eg. the `Closure` class or `spl_autoload_register(...)` function).
> Repo: [https://github.com/uniter/phpcore](https://github.com/uniter/phpcore)

[`phpruntime`](./phpruntime) is the extended "full" runtime library.
After pulling in `phpcore`, it installs the remaining builtin classes and functions, such as `array_merge(...)`.
Only a small subset of PHP's standard library has been implemented so far - please open a GitHub issue
in the `phpruntime` repository if you would like to request something that is missing.
> Repo: [https://github.com/uniter/phpruntime](https://github.com/uniter/phpruntime)

[`phpcommon`](./phpcommon) contains various tools that are shared between the different
packages, such as the `PHPFatalError` class used by both the parser (`phptoast`) and runtime (`phpcore`).
> Repo: [https://github.com/uniter/phpcommon](https://github.com/uniter/phpcommon)

[`phpify`](./phpify) is a Browserify transform that can be used to require PHP modules
(and entire libraries) from JavaScript.
For an example of compiling a PHP library down to JavaScript,
see the [Uniter Symfony EventDispatcher demo](https://github.com/uniter/event-dispatcher-demo).
> Repo: [https://github.com/uniter/phpify](https://github.com/uniter/phpify)

[`dotphp`](./dotphp) allows for easily including PHP files from Node.js.
A `require(...)` extension may be installed by using the `/register` script or PHP files may simply be required
with the exported `.require(...)` method. Stderr and stdout are mapped to the process' stderr and stdout respectively,
and the filesystem/ `include/require/_once(...)` access is mapped to the real filesystem.
> Repo: [https://github.com/uniter/dotphp](https://github.com/uniter/dotphp)
