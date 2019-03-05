# Test Reporting

Because Cypress is built on top of Mocha, that means any reporter built
for Mocha can be used with Cypress.

Cypress comes with two most common third party reporters for Mocha.
These are built into Cypress and can be used without installing
anything. 

-   [`teamcity`](https://github.com/cypress-io/mocha-teamcity-reporter)
-   `junit`

Also, Cypress supports creating custom reporters or using any kind of
3rd party reporters. 

## Local Reporters

Say you have the following directory structure:

``` bash
> my-project
  > cypress
  > src
  > reporters
    - custom.js
```

### To specify the path to your custom reporter:

``` xml
// cypress.json

{
  "reporter": "reporters/custom.js"
}
```

    The path above is relative to where your cypress.json is located.

  

Most famous reporter built on mocha is mochawesome reporter that can be
configured to create simple and user-friendly html reports. 

To install mochawesome reporter. 

``` js
// cypress.json

{
  "reporter": "mochawesome"
}
```

    Command line

``` bash
$ cypress run --reporter mochawesome
```

    You need to install any peer dependencies the reporter requires, even if they’re bundled with Cypress. 

    For example, mochawesome requires mocha as a peer dependency. You will need to install mocha as a dev dependency of your own project for it to work.

# Reporter Options

Some reporters accept options that customize their behavior. These can
be specified in your `cypress.json` or via the command line:

cypress.json

``` js
{
  "reporter": "junit",
  "reporterOptions": {
    "mochaFile": "results/my-test-output.xml",
    "toConsole": true
  }
}
```

### Command line

``` bash
$ cypress run --reporter junit --reporter-options "mochaFile=results/my-test-output.xml,toConsole=true"
```

Reporter options differ depending on the reporter (and may not be
supported at all). Refer to the documentation for the reporter you are
using for details on which options are supported.

  

Here is a sample Mochawesome report been generated. 

![Mochawesome
Screenshot](https://adamgruber.github.io/mochawesome/img/mochawesome-screen.png){height="400"}
