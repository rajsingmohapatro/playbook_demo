# Web Services / APIs

### What is API testing?

Application Programming Interface (API) is a specification that acts as
an interface for software components. While most functional testing
involves testing a user interface like a web page or a .NET form, *API
testing* involves bypassing a user interface and communicating directly
with an application by making calls to its APIs.

API testing allows the user to test headless technologies
like [JMS](https://en.wikipedia.org/wiki/Java_Message_Service), HTTP
Databases, and Web Services.

### Headless Testing

Most headless testing consists of bypassing the GUI and sending a
request directly to an application’s backend or service and receiving a
response back while validating the response to ensure things are working
as one expects them

[![API Testing
Approach](https://www.joecolantonio.com/wp-content/uploads/2018/11/APITestingApproach.png){.alignnone
.size-full .wp-image-4097 .lazyloaded width="419"
height="141"}](https://www.joecolantonio.com/api-testing/apitestingapproach/)

The above example is often referred to as the client/server
relationship. A client makes a request by asking for a resource, and the
request goes out to find the server that will fulfill the request. The
server locates the desired resource and then sends a response back to
the client.

### Why is API Testing Important?

With Agile development becoming the standard in most organizations, the
ways in which we develop software and automate tests have changed
dramatically.

Pre-Agile, most of the time spent on automation was done against a
graphical user interface (GUI). This is the piece that tools like
Selenium and  UFT/QTP handle.

But if you’ve been doing automation for any length of time you know how
time-consuming, fragile and hard-to-maintain these types of tests are.

Entire books have been written on how organizations have invested large
sums of money into creating custom functional GUI test automation
frameworks, only to become frustrated with their reliability over time;
to the point where people stop using it and the software becomes
shelf-ware.

Also, GUI tests that go against a user interface tend to take a long
time to run. For certain Agile practices like continuous builds, when
new code is checked in, the amount of time it takes to receive feedback
from a GUI regression suite of tests is unacceptable.

### API Fast Feedback

In those cases, quicker feedback is needed.

The sooner bugs are found the better since a developer instantly knows
the code changes they made have broken the build and need to be looked
at. In test-driven processes, users need a large percentage of test sets
to run fast and frequently and must be able to integrate them into the
development lifecycle.

GUI testing is still very important; it’s the only test type that truly
tests how a user will experience an application during production.
Certain defects can only be caught by GUI tests. In other words, while
it’s crucial, GUI should not be the only type of automation a user
focuses on, nor should it be the largest piece of the total amount of
automated tests that one creates.

Some good questions to ask when automating an API / web service:

-   Does the service respond with the correct values?
-   Does the behaviour match the end user’s intended requirements?
-   How quickly does the service send a response to the user?
-   Can the service handle expected and unexpected user loads?
-   Can the service handle invalid values and exceptions caused by bad
    data?

  

  
