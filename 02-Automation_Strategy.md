# Automation Strategy

Any Automation Strategy adhering to the principles of Test Automation
Pyramid should roughly be broken down as per below, which lists the
various types of Automated Tests and their ideal approx proportion
within any automated test pack.

<p float="left">
  <img src="images/119669963/119672045.png" width="450" />
  <img src="images/119669963/119671225.png" width="300" /> 
</p> 

### Automated Unit Tests: 

The key to a successful Test Automation Strategy starts with a comprehensive suite of Unit tests. Unit tests should be written by developers (Front End and Back End)  for any new feature that is developed. These Unit Tests form the foundation of a larger automation practice that spans all the way up to the System UI Tests. It is the responsibility of the developers to ensure that for every new component that is developed, a set of coherent and solid Unit Tests are written to prove that the code works as intended, handles errors and exceptions and meets the requirements. 

To support this, best practices such as [Test Driven Development (TDD)](https://en.wikipedia.org/wikiTest-driven_development) utilising the [x-unit frameworks](https://en.wikipedia.org/wiki/List_of_unit_testing_frameworks) and techniques such as [peer reviews](https://dev.to/codemouse92/10-principles-of-a-good-code-review-2eg) and tools for [code coverage](https://www.codacy.com/blog/what-your-mother-didnt-tell-you-about-code-coverage/) and [static analysis](https://en.wikipedia.org/wiki/List_of_tools_for_static_code_analysis) should also be utilised.

Among the various types of automated tests from within the Test Automation Pyramid, Unit Tests provide the most Return On Investment(ROI) to the team as they are very quick to run, easy to maintain and modify (as there are no dependencies). Errors detected in code as a result of running unit tests are quickly fed back to the developer. In theory, the suite of automated unit tests should not take longer than 5 minutes to run. 

### Automated Integration Tests: 

While Unit Tests are based around testing the functions within a class, Integration Tests form the next level up from Unit Tests to test the classes that collectively makeup the component to deliver a piece of functionality. These tests also include how components interact with resources or sub-systems (e.g file systems, databases) and are executed only when the Unit Tests have successfully run and passed.

Integration Tests are naturally run at API layer without the intervention of the user interface; hence tests would be able to verify functionality of a sub-system (or entire system in some cases) in a pure form and because the tests talk directly to the components, they are fast to execute and will be part of the build.

With integration tests different categories such as component, integration and API can be a bit difficult to classify. For some people integration testing is a very broad activity that tests through a lot of different parts of your entire system. For other's it's a rather narrow thing, only testing the integration with one external part at a time. Some call them integration tests, some refer to them as component tests, some prefer the term service test. Even others will argue, that all of these three terms are totally different things. There's no right or wrong. The software development community simply hasn't managed to settle on well-defined terms around integration testing.

### **Automated API Tests: **

API Functional tests involve testing the business functionality / logic of an application without having to use the User Interface. In order to do so, the services behind the application should exposed through an API (REST or Soap). Although every effort should be made in testing API end points in isolated parts of the system down to unit test level or covered through basic contract tests, a suite of automated API functional tests which test the logic and functionality of the service behind the application, without having to access the interface of the app is highly recommended. As a general recommendation, automated tests in the Integration / Service layer (including Component, Integration and API) of the Test Automation Pyramid should not take more than 20 minutes to run.

  

### **Automated GUI / E2E Tests:**

On the very top of Test Automation Pyramid lies the automated GUI or end-to-end(E2E) tests. There should be as few end-to-end tests as possible.  Although it is typically attractive to automate all the manual test cases in test pack at this layer, these type of tests have a tendency to be brittle and hence costly to maintain. They do however serve a useful purpose as smoke tests for the deployment of the solution, and can provide an early indication of major issues with the customer facing aspect of the app, that may not be wholly apparent at a lower level of testing. Key critical functionality and user flows with maximum traffic are usually good candidates to be automated in this layer.

A common problem is that teams conflate the concepts of End to End(E2E) tests, UI tests, and customer facing tests. These are all orthogonal characteristics. Modern single page application frameworks e.g react often come with their own tools and helpers that allow to thoroughly test these interactions in a pretty low-level (unit test) fashion. In pure frontend implementation using javascript, regular testing tools like Cypress can also be utilised. With a more traditional, server-side rendered application, Selenium-based tests are recommended choice.

  

### Manual Session Based Testing: 

Even the most diligent test automation efforts are not perfect. Sometimes certain edge cases are missed in automated tests and on other occasions it's nearly impossible to detect a particular bug by writing a unit test. Certain quality issues don't even become apparent within automated tests (i.e design or usability). Despite the best intentions with regards to test automation, manual session based testing of some sorts is still a good idea.

### *Avoiding Duplication:*

*In any automation strategy, it is important that automated tests at various layers of the Test Automation Pyramid and distributed in an even manner. The recommended Automated Test Coverage split is 70/20/10 between Unit, Integration and UI layer. While some overlap is unavoidable, techniques such as the [Three Amigo framework](https://techblog.constantcontact.com/software-development/three-amigos-to-the-rescue/) can help with identifying and eliminating automated test duplication.*
