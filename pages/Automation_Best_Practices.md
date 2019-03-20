# Automation Best Practices

Test Automation is an important testing activity during the software development lifecycle as it helps provide quick feedback to the team when a change in application code or logic is made. It also eases the burden of a human effort of repeated execution of regression tests resulting in more meaningful use of a QA Engineer's time towards exploratory testing.

Test Automation, when done right, can be very beneficial to the team. The ideas discussed below will help get the most value from a test automation process/activities and highlights pitfalls to avoid when starting the journey.

#### Manual vs Automated – Testing vs Checking

Avoid comparison between manual and automated testing. They are both needed as each serves a different purpose. Automated tests are a set of instructions written by a person to do a specific task. Every time an automated test is run, it will follow exactly the same steps as instructed and only check for things that are being asked to check.

On the other hand, during manual testing, tester’s brain is engaged and can spot other failures in the system. The test steps may not necessarily be the same every time, as the tester can alter the flows during the testing; this is especially true in case of exploratory testing.

#### Automate Regression Tests

One of the major reasons to automate a test is that you want to execute the test repeatedly on every new release. If the test is required to be executed only once, then the effort to automate the test can outweigh the benefits.

Regression tests are required to be executed repeatedly as the software under test evolves. This can be very time consuming and a boring task for QA to have to run regression tests every day. Regression tests are good candidates for test automation.

For example, here at Qantas, we have a release every week. We have more than 200 tests in the regression suite. Imagine the time and effort that would be needed to execute these tests manually. Also the chances of missing a test is high when executed manually. 

#### Design Tests Before Automating Them

A good test design helps in identifying the most probable automation candidates, which will increase the probability to find defects.

The danger in jumping straight to automation is that you’re only interested in making the script to work and usually only automate positive and happy flow scenarios rather than thinking about the other possible scenarios that can be tested.

Also, don’t reduce the scope of testing just to make the test work or pass.

#### Remove Uncertainty from Automated Tests

One of the key points of automated testing is the ability to give consistent results so that we can be certain that something has actually gone wrong when a test fails.

If an automated test passes in one run and fails in the next run, without any changes on the software under test, we cannot be certain if the failure is due to the application or due to other factors, such as test environment issues or problems in the test code itself.

When there are failures, we have to analyze the results to see what had gone wrong, and when we have lots of inconsistent or false positive results, it increases analysis time.

Don’t be afraid to remove unstable tests from regression packs; instead, aim for consistent clean results that you can rely on.

For example, there might be a scenario which is an edge case and the Engineer has automated it on Test Env. However this particular scenario might not be happening in staging or pre-prod. As a result this test passes on Test Env but consistently fails on Staging. It is better to remove such Tests.

#### Review Automated Tests for Validity

You will be alarmed by the sheer number of automated tests that are outdated, just don’t check for anything or are not checking the most important verifications!

This could be a symptom of jumping straight to automation without spending enough time beforehand planning on what needs to be done and designing good test scenarios.

Always have a colleague to review the automated tests for validity and sanity. Make sure tests are up to date.

#### Don’t Automate Unstable Functionality

As a new feature or functionality is being developed, many things can go wrong and even the feature may no longer be applicable because the business have changed their mind.

If you started automating tests as the feature was being developed, the tests need to be updated many times as the feature evolves and can be quite daunting trying to keep up with all the changes. And if the feature is no longer applicable, all that effort on test automation is wasted.

Therefore, it is always best to automate a feature once it has been stabilized and less subject to change.

#### Don’t Expect Magic From Test Automation

The primary reason for test automation is to free up QA time for interesting exploratory testing and to give confidence to the team that the application is still in good order as new changes are delivered.

Don’t expect automation to find lots of bugs. In fact, the number of bugs found by automation is always much less than manual and exploratory testing.

#### Don’t Rely Solely on Automation – Beware of False Positives

Automated regression tests can give a sense of confidence for the team because regression tests should still pass as new functionality is delivered.The team starts relying on the tests and having a good set of regression tests can act as a safety net.

However, note that not all tests are automated or can be automated, therefore always accompany automated tests with exploratory testing.

Sometimes a change in the software should fail a test; however, if all tests are passing that means the defect is missed and because there was no call to action, the defect went unnoticed.

#### Aim for Fast Feedback

Quick feedback is one of the objectives of automated tests because developers are keen to know if what they have developed works and hasn’t broken current functionality.

In order to get this quick feedback loop, the tests need to be automated at component or API layer without relying on the UI.

Tests run on UI are much slower and prone to error due to GUI changes. In other words, the functionality still works as expected but the tests fail due to changes in the UI. Therefore the tests can become unreliable.

#### Understand the Context

Tests can be automated at any layer, Unit, API, Service, GUI. Each layer serves a different purpose for testing.
Unit Tests ensure that the code works at the class level, that it compiles and the logic is as expected. Tests at this layer are more verification than validation.

API Tests or Integration Tests ensure a set of functions and classes can work together and data can be passed from one class to another.

GUI Tests on the other hand test user flows and journeys. Generally, we would not test for functionality from the UI. This should be done at lower layers.

The main purpose of UI tests is to ensure the whole system works as per some common user scenarios and use cases. Testing at this layer is more Validation rather than Verification

At UI level, we automate scenarios rather than stories.

Read more about Test Pyramid [here](https://www.agilecoachjournal.com/2014-01-28/the-agile-testing-pyramid).

#### Don’t Automate Every Test

100% Test Coverage is not possible since there can be millions of combinations. We always execute a subset of possible tests. The same principle applies to automated testing.

To create an automated script, it requires time and effort, and aiming for “Automating Every Test”, we require a lot of resource and time, which in many cases is not possible.

Instead, use a Risk-based approach to determine which tests should be automated. To get the most value out of automation, only automate the most important business cases and scenarios.

Also, a high number of automated tests adds maintenance cost and difficult to maintain.

Another note to bear in mind is that not all tests can be automated. Some tests are very complex in nature and require many downstream system checking and can be inconsistent. In these cases, it is best to leave these checks for manual testing.

#### Don’t Automate Chaos

In order to get the most out of your automated testing, a good QA process should be in place. If the QA process is chaotic and we add automated testing to that chaos, all we get is faster chaos.

Try to answer questions like, What to automate, When to automate, When to execute the automated tests, Who shall automate the tests, What tools should be used for test automation, etc…

#### Cross browser testing

![](attachments/119669972/119682705.jpg)

-   Cross browser testing is a process that ensures your website or application behaves as expected across multiple browsers.
-   Cross browser testing can be time consuming. Automated methods like unit testing, functional testing or visual regression do not capture cross browser bugs. So as of yet, it can only be done manually. Because every test starts from usage statistics, simplifying the statistics only makes sense. This means, taking into account only the meaningful platform/operating system/vendor/version combinations. For the most part, differences between versions, platforms and operating systems can be omitted.
-   Browser neutral bugs can waste time. These are stylistic bugs, incapable of being caught by automated methods, but that have nothing to do with a specific browser. Falsely assuming that a browser-neutral bug is browser specific can waste time.
-   A short list of techniques that can be used to catch them are:

    -   resizing the browser
    -   zooming in and out if applicable
    -   turning JavaScript off
    -   turning CSS off
    -   turning off both CSS and JavaScript
    -   using only a keyboard to interact with the
application.

Any browser can be used.

We at Qantas use browserstack for cross browser testing.

### Mobile testing

#### Good mobile testing practices

-   Ensure that you have access to all physical devices on which the application run (Not just emulators or simulators)
-   Consider the additional time and/or personnel needed to test all the application’s modules on all the devices.
-   Have an explicit list of devices on which QA will be performed. Basically this means that the company is committing to supporting certain devices and Operating Systems on which the application will perform as designed. The users will be informed that even though the application might work on other devices, the company will not be held responsible for unexpected issues. This is the approach taken by most leading vendors today, including for example, Skype.
-   Implement a mixed strategy when you have a scenario where you do not have all the possible devices and therefore cannot do exhaustive testing on each:  Use an emulator on the early stages of app development.  Keep adding real devices into the testing later down the development cycle. This way you can certify that all the requirements and goals are being covered.
