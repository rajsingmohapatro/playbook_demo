# Branching, Merging & Code Reviews

We use the [GitHub Flow](https://guides.github.com/introduction/flow/)
workflow for branching.

### In summary:

-   Create a branch off master anytime you are starting some new work.
-   Give the branch a useful name, referencing the JIRA ticket for that
    piece of work.
-   Commit regularly with meaning full messages. You can do this via
    command line or use a GUI based tool such as
    [Sourcetree](https://www.sourcetreeapp.com/).
-   When you are finished your work and want to merge it to master first
    create a pull request.

More detail available
[here](https://confluence.qantas.com.au/display/QQE/Automation+Test+Approach).

### Pull requests:

Always create a pull request for any changes you have made. This is so
other team members are made aware of the changes made, and an
opportunity to review and discuss improvements that could be made.

We make sure to never pushed straight to master.

As per QCP guidelines, all repositories require a minimum of 2 reviewers
and a passing build on bamboo.

### Some tips on how to create a good pull request:

-   Add a useful description.
-   Try and keep it small. The smaller the PR, the quicker it will be
    merged.
-   Make sure your changes/new tests don't break any existing tests.
-   Verify if the changes align to the framework architecture.
-   Include everyone as reviewers who need to know about the changes.
-   We write code in a consistent style. For example, some Java
    frameworks may follow [Google's style
    guide](https://google.github.io/styleguide/javaguide.html). Style
    guides can be automatically applied through your IDE.

### Some tips on how to review a pull request:

-   Try to make it a priority if possible.
-   We try and suggest solutions instead of just pointing out the area
    of improvement. Create a PR into the original PR.
-   We avoid Technical harassment (we are all on the same team).
-   Nobody has veto power.
-   Some things to look for -
    <https://automationpanda.com/2017/05/08/10-gotchas-for-automation-code-reviews/>.

The branch can be deleted when it is merged and you have no more changes
to make.
