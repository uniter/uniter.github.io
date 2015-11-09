# Roadmap

In here, I will list what I will/want/should implement for these docs.

- [X] Intro page
    * FIXME: It could take some improvements. But it's a "draft" for now.
- [ ] Basic documentation of:
    * [X] What is Uniter and what does it do?
    * [ ] Getting started
        * [ ] Standalone
        * [X] Browserify (`phpify`)
        * [X] NodeJS
        * [ ] WebPack? / etc.
    * Benefits and disadvantages
    * Use cases
        * In the Browser...
        + In NodeJS...
        * In combination...
- [ ] Write example code.
    * [ ] "Run it!" function, to run Uniter straight off the page.
        * **NOTE** This will bundle the whole Runtime plus transpiler. Big JS file.
          I will use WebPack to handle that.
- [ ] Document the internal API
    * `Environment`
    * `Engine`
    * `phpToJS` / `phpToAST`
    * Uniter STL
    * Extending Uniter
- [ ] Advanced topics
    * Working with the AST
    * Use Sync or Async
    * Performance gains/losses
    * Optimal dependency tracking and injection
    * Minding the output filesize
    * Minding the environment
