FAQ
===

Q: Is it fast enough?
---------------------
A: As with any browser-side work you do, the profiler is your friend.
The value system (see [Q: How are floats vs. ints handled?](#q-how-are-floats-vs-ints-handled)) adds a fair amount of overhead,
so you may find that the equivalent code written in vanilla JS is faster than writing the same logic
in PHP and transpiling it down to JS with Uniter.

Q: How are floats vs. ints handled?
-----------------------------------
Due to nuances in value handling between JS and PHP, Uniter handles primitive value types
like strings and numbers specially. This means it can still distinguish between an integer and a float,
even though JavaScript only has one value type for both: Number.

Q: Why?
-------
A: The goal here isn't to try to replace JavaScript on the browser-side - that would be crazy.
Instead, we can take existing PHP code, transpile it down to JavaScript in much the same way
as we would with ES6->ES5 with Babel, and then run it in the browser.

This means you can take a package that already exists on Packagist (like a Symfony component),
install it with Composer and use it browser-side too.

> See [the Composer autoloader section](../composer/autoloader.html) for an explanation of how this works.
