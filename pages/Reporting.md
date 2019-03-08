# Reporting

Test reports help us to communicate the current state of the application
that we are testing.

They help stakeholders make decisions for releases.

Test reports should be clear and detailed. Ideally they are in a [BDD
format](https://docs.cucumber.io/guides/bdd-tutorial/).  
Some useful information that should be included in the report includes:

-   Number of features/scenarios/tests run
-   Number passed
-   Number failed
-   Number pending
-   Duration
-   Environment

If a test fails, the stacktrace should be displayed in the report to
help with debugging.  
If using a remote testing tool like Browserstack or Device Farm, then a
link to the video for the failing test should be included.

When choosing a tool for test automation reporting look at the more
popular open source ones available.  
Try and avoid writing your own reporting tool.  
There's lots of [Cucumber
plugins](http://docs.cucumber.io/cucumber/reporting/) available or you
can use [Serenity BDD](index) which comes with some nice functionality
for reporting.

When running tests on CI, use email triggers to send links for test
reports.  
You can also use Slack for Bamboo build notifications.

  
