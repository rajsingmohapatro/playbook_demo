# Maintenance & Improvements

Any test automation frameworks and suite require regular updating and
maintenance. The true ROI can only be realised in the the long run when
automated tests are regularly maintained, reviewed, modified and retired
to suit changing needs/scope of the product. If we don't continue to
review, improve and update test frameworks we run the risk they will
fall over.

It's important to come up with a strategy for handling tech debt and
continuously improving the framework. Tech debt should be negotiated
with your team and included in sprints as an ongoing activity. As a
general principle, 20% of your innovation time should include as much as
possible towards maintaining a healthy and robust automated test pack.
These test automation maintenance tasks should be identified, logged in
JIRA and included as part of sprint planning for the entire team to have
visibility on the maintenance work needed.

Some tips on making maintenance easier:

-   Try and fix tests before a release goes live, otherwise they may get
    left behind.
-   [Reuse code](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
    wherever possible, more code is not always a good thing.
-   Regularly check for updated libraries.
-   Collaborate with other teams to compare test frameworks.
-   Try and avoid creating large tests, only test one thing at a time.
    Smaller is better.
-   Decouple test data.
-   Use IDs for element locators. Work with developers on ensuring IDs
    are assigned to elements.
-   Use page object model for UI tests.
-   Add helper classes where it makes sense.
-   If the code isn't simple and clear add some comments.
-   Work closely with developers. Encourage them to run your tests.
