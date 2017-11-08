
Makefiles
=========

**:warning: This project is no longer being maintained. It has been superceded by [rowanmanning/make](https://github.com/rowanmanning/make) :warning:**

Makefiles for use in various open source projects. Each Makefile provides a bunch of useful tasks which can be included in the Makefiles of your own projects. Heavily inspired by [n-makefile].

[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](#license)


Table of Contents
-----------------

  * [Node.js](#nodejs)
  * [License](#license)


Node.js
-------

The [Node.js] project Makefile is in [`Makefile.node`](Makefile.node). To use it, run the following in your project directory:

```sh
curl -s https://raw.githubusercontent.com/rowanmanning/makefiles/master/Makefile.node > Makefile.node
```

Now create a `Makefile` in the same directory and add the following to the top:

```make
include Makefile.node
```

This allows you to extend the provided tasks without worrying about your changes being overwritten when you update. Update to the latest version of `Makefile.node`:

```sh
make update-makefile
```

### Included tasks

  * `all`: Run the `install` and `ci` tasks.

  * `ci`: Run the `verify` and `test` tasks.

  * `clean`: Cleans the working directory. Relies on `git`.

  * `install`: Runs `npm install` but only if `package.json` has changed more recently than the `node_modules` folder. This speeds up installing to be instant if nothing needs doing. This task also prunes extra dependencies.

  * `verify`: Run the `verify-javascript` and `verify-spaces` tasks.

  * `verify-javascript`: Run the `verify-eslint`, `verify-jshint`, and `verify-jscs` tasks.

  * `verify-eslint`: If an `.eslintrc` file is present in the project root, run [ESLint] against the code.

  * `verify-jscs`: If a `.jscsrc` file is present in the project root, run [JSCS] against the code.

  * `verify-jshint`: If a `.jshintrc` file is present in the project root, run [JSHint] against the code.

  * `verify-spaces`: If an `.editorconfig` file is present in the project root and the [`lintspaces-cli`][lintspaces-cli] module is installed, run [Lintspaces] against the code.

  * `verify-coverage`: If a `coverage/lcov-report` folder is present in the project root and the [`nyc`][nyc] or [`istanbul`][istanbul] module is installed, check that coverage is above `90%`. This is configurable by specifying `export EXPECTED_COVERAGE := <value>` in your dependant Makefile.

  * `test`: Run the `test-unit-coverage`, `verify-coverage`, and `test-integration` tasks.

  * `test-unit`: If a `test/unit` folder is present in the project root, run [Mocha] recursively on it.

  * `test-unit-coverage`: If a `test/unit` folder is present in the project root and the [`nyc`][nyc] or [`istanbul`][istanbul] module is installed, run [Mocha] recursively on it with coverage reporting. If `instanbul` is _not_ present, fall back to `make test-unit`.

  * `test-integration`: If a `test/integration` folder is present in the project root, run [Mocha] non-recursively on it.

  * `update-makefile`: Update to the latest version of this Makefile.

### Helpers

  * The `TASK_DONE` output helper allows you to quickly output a green check-marked notice after a task has completed successfully. Just add it to your own tasks like this:

    ```make
    mytask:
        @do something
        @$(TASK_DONE)
    ```

  * The folder `./node_modules/.bin` is added to the `PATH` environment variable so that you don't need to explicitly reference it in calls to further commands.


License
-------

Makefiles is licensed under the [MIT] license.  
Copyright &copy; 2016, Rowan Manning



[eslint]: http://eslint.org/
[jscs]: http://jscs.info/
[jshint]: http://jshint.com/
[lintspaces]: https://github.com/schorfES/node-lintspaces
[mit]: LICENSE
[n-makefile]: https://github.com/Financial-Times/n-makefile
[node.js]: https://nodejs.org/
[lintspaces-cli]: https://github.com/evanshortiss/lintspaces-cli
[istanbul]: https://github.com/gotwarlost/istanbul
[mocha]: https://mochajs.org/
[nyc]: https://github.com/istanbuljs/nyc
