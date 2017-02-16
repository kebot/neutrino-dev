# Neutrino Jest Preset [![NPM version][npm-image]][npm-url]

`neutrino-preset-jest` is a Neutrino preset that supports testing JavaScript projects with the Jest test runner.

## Features

- Zero upfront configuration necessary to start testing
- Babel compilation that compiles your tests using the same Babel options used by your source code
- Easily extensible to customize your testing as needed

## Requirements

- Node.js v6.9+
- Yarn or npm client
- Neutrino v4, Neutrino build preset

## Installation

`neutrino-preset-jest` can be installed via the Yarn or npm clients. Inside your project, make sure
`neutrino` and `neutrino-preset-jest` are development dependencies. You will also be using
another Neutrino preset for building your application source code.

#### Yarn

```bash
❯ yarn add --dev neutrino-preset-jest
```

#### npm

```bash
❯ npm install --save-dev neutrino-preset-mocha
```

## Project Layout

`neutrino-preset-jest` follows the standard [project layout](/project-layout.md) specified by Neutrino. This
means that by default all project test code should live in a directory named `test` in the root of the
project. Test files end in either `_test.js` or `.test.js`.

## Quickstart

After adding the Jest preset to your Neutrino-built project, add a new directory named `test` in the root of the
project, with a single JS file named `simple_test.js` in it.

```bash
❯ mkdir test && touch test/simple_test.js
```

Edit your `test/simple_test.js` file with the following:

```js
describe('simple', () => {
  it('should be sane', () => {
    expect(!false).toBe(true);
  });
});
```

Now edit your project's package.json to add commands for testing your application. In this example,
let's pretend this is a Node.js project:

```json
{
  "scripts": {
    "test": "neutrino test --presets neutrino-preset-node neutrino-preset-mocha"
  }
}
```

Run the tests, and view the results in your console:

#### Yarn

```bash
❯ yarn test

  simple
    ✓ should be sane


  1 passing (426ms)

✨  Done in 4.17s.
```

#### npm

```bash
❯ npm test

  simple
    ✓ should be sane


  1 passing (409ms)
```

To run tests against files from your source code, simply import them:

```js
import thingToTest from '../src/thing';
```

## Executing single tests

By default this preset will execute every test file located in your test directory ending in `_test.js`.
Use the command line [`files` parameters](/cli/README.md#neutrino-test) to execute individual tests.

## Customizing

To override the test configuration, start with the documentation on [customization](/customization/README.md).
`neutrino-preset-mocha` creates some conventions to make overriding the configuration easier once you are ready to make
changes.

### Rules

The following is a list of rules and their identifiers which can be overridden:

- `compile`: Compiles JS files from the `test` directory using Babel. Contains a single loader named `babel`.

### Simple customization

By following the [customization guide](/customization/simple.md) and knowing the rule, loader, and plugin IDs above,
you can override and augment the build directly from package.json.

### Advanced configuration

By following the [customization guide](/customization/advanced.md) and knowing the rule, and loader IDs above,
you can override and augment testing by creating a JS module which overrides the config.

You can modify Mocha settings by overriding the preset with any options Mocha accepts. This is stored in the
`neutrino.custom.mocha` object.

_Example: Switch the test reporter from the default `spec` to `nyan`:_

```js
module.exports = neutrino => {
  neutrino.custom.mocha.reporter = 'nyan';
};
```

```bash
❯ yarn test
yarn test v0.19.1
$ node_modules/neutrino/bin/neutrino test
 1   -__,------,
 0   -__|  /\_/\
 0   -_~|_( ^ .^)
     -_ ""  ""

  1 passing (362ms)

✨  Done in 3.28s.
```

## Contributing

This preset is part of the [neutrino-dev](https://github.com/mozilla-neutrino/neutrino-dev) repository, a monorepo
containing all resources for developing Neutrino and its core presets. Follow the
[contributing guide](/contributing/README.md) for details.

[npm-image]: https://badge.fury.io/js/neutrino-preset-jest.svg
[npm-url]: https://npmjs.org/package/neutrino-preset-jest