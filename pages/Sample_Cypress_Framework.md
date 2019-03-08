# Sample Cypress Framework

# What is Cypress:

Cypress is a next generation front end testing tool built for the modern
web. We address the key pain points developers and QA engineers face
when testing modern applications.

It simplifies the process of: 

-   [Set up
    tests](https://docs.cypress.io/guides/overview/why-cypress.html#Setting-up-tests)
-   [Write
    tests](https://docs.cypress.io/guides/overview/why-cypress.html#Writing-tests)
-   [Run
    tests](https://docs.cypress.io/guides/overview/why-cypress.html#Running-tests)
-   [Debug
    Tests](https://docs.cypress.io/guides/overview/why-cypress.html#Debugging-tests)

Cypress is most often compared to Selenium; however Cypress is both
fundamentally and architecturally different. Cypress is not constrained
by the same restrictions as Selenium.

This enables you to write faster, easier and more reliable tests.

# Cypress Usage:

Users of Cypress are typically developers or QA engineers building web
applications using modern JavaScript frameworks.

Cypress enables you to write all types of tests:

-   End-to-end tests
-   Integration tests
-   Unit tests

Cypress can test anything that runs in a browser.

# Setting up Cypress:

There are no servers, drivers, or any other dependencies to install or
configure. All it requires is that you have **npm (Node Package
Manager)** installed on your machine and with a couple of steps you can
start using Cypress. 

1.  Check if you have node installed on your system;

    ``` bash
    $ node -v 
    v11.6.0
    $ npm -v
    6.5.0
    ```

    If you don't have node installed, please download it from
    [here.](https://nodejs.org/)

      

2.  If you do have npm then simply install cypress;

    ``` bash
    $ npm install cypress --save-dev
    ```

3.  Once you have cypress installed, you can now open up an editor of
    your choice, open up the folder where you installed cypress and
    start writing tests. 

# Understanding Cypress Structure:

  

# Folder Structure

After adding a new project, Cypress will automatically scaffold out a
suggested folder structure. By default it will create:

``` bash
/cypress
  /fixtures
    - example.json

  /integration
    /examples
      - actions.spec.js
      - aliasing.spec.js
      - assertions.spec.js
      - connectors.spec.js
      - cookies.spec.js
      - cypress_api.spec.js
      - files.spec.js
      - local_storage.spec.js
      - location.spec.js
      - misc.spec.js
      - navigation.spec.js
      - network_requests.spec.js
      - querying.spec.js
      - spies_stubs_clocks.spec.js
      - traversal.spec.js
      - utilities.spec.js
      - viewport.spec.js
      - waiting.spec.js
      - window.spec.js

  /plugins
    - index.js

  /support
    - commands.js
    - index.js
```

  

## Configuring Folder Structure

While Cypress allows to configure where your tests, fixtures, and
support files are located, if you’re starting your first project, It is
recommended to use use the above structure.

You can modify the folder configuration in your `cypress.json`.

## Fixture Files

Fixtures are used as external pieces of static data that can be used by
your tests.

You would typically use them with
the [`cy.fixture()`](https://docs.cypress.io/api/commands/fixture.html) command
and most often when you’re stubbing [Network
Requests](https://docs.cypress.io/guides/guides/network-requests.html).

## Test files

Test files may be written as:

-   `.js`
-   `.jsx`
-   `.coffee`
-   `.cjsx`

Cypress also supports `ES2015` out of the box. You can use
either `ES2015 modules` or `CommonJS modules`. This means you
can `import` or `require` both npm packages and local relative modules.

>  Example Recipe
>
>   
>
> Check out our recipe using [ES2015 and CommonJS
> modules](https://docs.cypress.io/examples/examples/recipes.html#Node-Modules).

To see an example of every command used in Cypress, open
the `example` folder within your `cypress/integration` folder.

To start writing tests for your app, simply create a new file
like `app_spec.js `within your `cypress/integration` folder. Refresh
your tests list in the Cypress Test Runner and your new file should have
appeared in the list.

## Plugin files

By default Cypress will automatically include the plugins
file `cypress/plugins/index.js` before every single spec file it runs.
This is done purely as a convenience mechanism so you don’t have to
import this file in every single one of your spec files.

## Support file

By default Cypress will automatically include the support
file `cypress/support/index.js`. This file runs before every single spec
file . This is done purely as a convenience mechanism so you don’t have
to import this file in every single one of your spec files.

The support file is a great place to put reusable behavior such as
Custom Commands or global overrides that you want applied and available
to all of your spec files.

You can define your behaviors in a `beforeEach` within any of
the `cypress/support` files:

    beforeEach(function () {
      cy.log('I run before every test in every spec file!!!!!!')
    })

![global
hooks](https://docs.cypress.io/img/guides/global-hooks.993be24d.png){height="250"}

>  Keep in mind, setting something in a global hook will render it less
> flexible for changes and for testing its behavior down the road.

From your support file you should also `import` or `require` other files
to keep things organized.

Cypress automatically seed you an example support file, which has
several commented out examples.

# Writing tests

Cypress is built on top
of [Mocha](https://docs.cypress.io/guides/references/bundled-tools.html#Mocha) and [Chai](https://docs.cypress.io/guides/references/bundled-tools.html#Chai).
We support both Chai’s `BDD` and `TDD` assertion styles. Tests you write
in Cypress will mostly adhere to this style.

If you’re familiar with writing tests in JavaScript, then writing tests
in Cypress will be a breeze.

## Test Structure

The test interface borrowed
from [Mocha](https://docs.cypress.io/guides/references/bundled-tools.html#Mocha) provides `describe()`, `context()`, `it()` and `specify()`.

`context()` is identical to `describe()` and `specify()` is identical
to `it()`, so choose whatever terminology works best for you.

``` js
function add (a, b) {
  return a + b
}

function subtract (a, b) {
  return a - b
}

function divide (a, b) {
  return a / b
}

function multiply (a, b) {
  return a * b
}
```

``` js
describe('Unit test our math functions', function() {
  context('math', function() {
    it('can add numbers', function() {
      expect(add(1, 2)).to.eq(3)
    })

    it('can subtract numbers', function() {
      expect(subtract(5, 12)).to.eq(-7)
    })

    specify('can divide numbers', function() {
      expect(divide(27, 9)).to.eq(3)
    })

    specify('can multiply numbers', function() {
      expect(multiply(5, 4)).to.eq(20)
    })
  })
})
```

## Hooks

Cypress also provides hooks (borrowed
from [Mocha](https://docs.cypress.io/guides/references/bundled-tools.html#Mocha)).

These are helpful to set conditions that you want to run before a set of
tests or before each test. They’re also helpful to clean up conditions
after a set of tests or after each test.

``` js
describe('Hooks', function() {
  before(function() {
    // runs once before all tests in the block
  })

  after(function() {
    // runs once after all tests in the block
  })

  beforeEach(function() {
    // runs before each test in the block
  })

  afterEach(function() {
    // runs after each test in the block
  })
})
```

  

    The order of hook and test execution is as follows:

-   All `before()` hooks run (once)
-   Any `beforeEach()` hooks run
-   Tests run
-   Any `afterEach()` hooks run
-   All `after()` hooks run (once)

>  Before writing `after()` or `afterEach()` hooks, please see
> cypress's [thoughts on the anti-pattern of cleaning up state
> with `after()` or `afterEach()`](https://docs.cypress.io/guides/references/best-practices.html#Using-after-or-afterEach-hooks).

## Excluding and Including Tests

To run a specified suite or test, simply append `.only` to the function.
All nested suites will also be executed. This gives us the ability to
run one test at a time and is the recommended way to write a test suite.

``` js
function fizzbuzz (num) {
  if (num % 3 === 0 && num % 5 === 0) {
    return 'fizzbuzz'
  }

  if (num % 3 === 0) {
    return 'fizz'
  }

  if (num % 5 === 0) {
    return 'buzz'
  }
}
```

``` js
describe('Unit Test FizzBuzz', function () {
  function numsExpectedToEq (arr, expected) {
    // loop through the array of nums and make
    // sure they equal what is expected
    arr.forEach((num) => {
      expect(fizzbuzz(num)).to.eq(expected)
    })
  }

  it.only('returns "fizz" when number is multiple of 3', function () {
    numsExpectedToEq([9, 12, 18], 'fizz')
  })

  it('returns "buzz" when number is multiple of 5', function () {
    numsExpectedToEq([10, 20, 25], 'buzz')
  })

  it('returns "fizzbuzz" when number is multiple of both 3 and 5', function () {
    numsExpectedToEq([15, 30, 60], 'fizzbuzz')
  })
})


To skip a specified suite or test, simply append .skip() to the function. All nested suites will also be skipped.
it.skip('returns "fizz" when number is multiple of 3', function () {
  numsExpectedToEq([9, 12, 18], 'fizz')
})
```

## Dynamically Generate Tests

You can dynamically generate tests using JavaScript.

``` js
describe('if your app uses jQuery', function () {
  ['mouseover', 'mouseout', 'mouseenter', 'mouseleave'].forEach((event) => {
    it('triggers event: ' + event, function () {
      // if your app uses jQuery, then we can trigger a jQuery
      // event that causes the event callback to fire
      cy
        .get('#with-jquery').invoke('trigger', event)
        .get('#messages').should('contain', 'the event ' + event + 'was fired')
    })
  })
})
```

    The code above will produce a suite with 4 tests:

    > if your app uses jQuery
      > triggers event: 'mouseover'
      > triggers event: 'mouseout'
      > triggers event: 'mouseenter'
      > triggers event: 'mouseleave'

## Assertion Styles

Cypress supports both BDD (`expect`/`should`) and TDD (`assert`) style
assertions. [Read more about
assertions.](https://docs.cypress.io/guides/references/assertions.html)

``` js
it('can add numbers', function() {
  expect(add(1, 2)).to.eq(3)
})

it('can subtract numbers', function() {
  assert.equal(subtract(5, 12), -7, 'these numbers are equal')
})
```

# Watching tests

When running in interactive mode
using [`cypress open`](https://docs.cypress.io/guides/guides/command-line.html#cypress-open) Cypress
watches the filesystem for changes to your spec files. Soon after adding
or updating a test Cypress will reload it and run all of the tests in
that spec file.

This makes for a productive development experience because you can add
and edit tests as you’re implementing a feature and the Cypress user
interface will always reflect the results of your latest edits.

> Remember to
> use [`.only`](https://docs.cypress.io/guides/core-concepts/writing-and-organizing-tests.html#Excluding-and-Including-Tests) to
> limit which tests are run: this can be especially useful when you’ve
> got a lot of tests in a single spec file that you’re constantly
> editing; consider also splitting your tests into smaller files each
> dealing with logically related behavior.

## What is watched?

Files

-   [`cypress.json`](https://docs.cypress.io/guides/references/configuration.html)
-   [`cypress.env.json`](https://docs.cypress.io/guides/guides/environment-variables.html)

Folders

-   `cypress/integration/`
-   `cypress/support/`
-   `cypress/plugins/`

The folder, the files within the folder, and all child folders and their
files (recursively) are watched.

> Those folder paths refer to the [default folder
> paths](https://docs.cypress.io/guides/references/configuration.html#Folders-Files).
> If you’ve configured Cypress to use different folder paths then the
> folders specific to your configuration will be watched.

## What isn’t watched?

Everything else; this includes, but isn’t limited to, the following:

-   Your application code
-   `node_modules`
-   `cypress/fixtures/`

If you’re developing using a modern JS-based web application stack then
you’ve likely got support for some form of hot module replacement which
is responsible for watching your application code—HTML, CSS, JS,
etc.—and transparently reloading your application in response to
changes.
