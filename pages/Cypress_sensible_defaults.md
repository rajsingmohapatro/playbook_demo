# Cypress sensible defaults

The following page will document sensible defaults when using Cypress for your UI automation framework.

### Using beforeEach() hook to set state of your application

Automation tests should be completely independent and isolated from one another to prevent flakiness and improve robustness of the framework. An example of an anti-pattern (i.e. bad practice) is when testing authenticated pages, to have one test login at the beginning of the test suite then have subsequent tests rely upon the initial success of that test. Should that test fail or any other subsequent test fail, it could potentially cause a domino effect of failures all because the state of the application was altered.

To prevent this it is best to set the state of the application, i.e. authenticate prior to each test executing using the `beforeEach()`, i.e. a sequence of commands run prior to the test running. 

Here is an example:

`beforeEach( function () {
    cy.loginViaAPI();
    cy.visit('/urlToTestPage')
})`

What this will do is prior to each test running:
* authenticate the user via the API, calling a custom function `loginViaAPI` that we've developed which simply makes a post request to the ID server and creates the authenticated session. We do not want to authenticate via the UI as it's slow and prone to more issues.
* We then 'visit' the page that we are trying to test directly. As we are now authenticated and the cookie set, there is no need to navigate through the home page.

The above will ensure each test is launched in a new state and that there are no interdependencies between one another.


### Using forEach() for iterating through test data



### Structuring test files so they aren't large



### Structuring test data files so they aren't large



### Including descriptions in test data files 



### How to use and setup Stub



### How to call test data files and share across many test cases 



### Setup different environment configuration files to execute across different environments (e.g. Dev / Stg / Prod)



### Reporting test results 



### Structuring and importing selectors from an external file and categorising them (e.g. tabs, buttons, input field etc...)



### iFrame


