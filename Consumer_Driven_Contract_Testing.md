# Consumer Driven Contract Testing

A Contract/Pact is a file which contains collection of agreements
between a client (Consumer)  and an API (Provider) that describes the
interactions that can take place between them. Consumer Driven Contracts
is a pattern that drives the development of the Provider from its
Consumers point of view.

### **Where is it used:**

Consumer contract testing is very useful in below situations

-   In micro services based architectures where a large number of
    consumer APIs depend on a single provider API(usually core APIs) and
    each consumer interacts/consumes provider in a slightly different
    way.
-   Where Provider API goes through frequent code/request/response body
    schema changes. Having contract testing in this case prevents
    existing consumers from breaking due to undesirable changes in
    Provider API.  
-   In a situation where Provider and Consumer APIs being developed
    simultaneously and Consumer team wants to set its expectation with
    Provider at an early stage of development cycle.

**For example:**

-   Lets assume we have a Provider API which responds to Get request
    method with a body containing four fields.
-   Assume we have two dependent consumers Consumer 1 and Consumer 2
    where Consumer 1 is interested in first 2 fields but consumer 2 is
    interested in last two fields exposed by Provider as part of
    response body.
-   Assume as part of an enhancement, if a developer on provider side
    makes a change to field 2 from type float to integer or removes the
    field without being aware of consumer 1's expectation then in
    production it would immediately break Consumer 1.
-   To ensure Provider API changes doesn't break any Consumer, tests
    have to be run for each consumer involving individual consumer
    teams. Imagine when a core Provider API has dozens of Consumers
    interacting with it and each consuming its response in slightly
    different way things would get very complicated to accommodate even
    small changes on Provider sides. Too many team level interactions
    would be required to identify impacted Consumer lists and to
    facilitate test executions on consumer side.
-   But having consumer based contract testing can help minimize the
    effort to test each consumers expectations without involving
    Consumer teams every time Provider undergoes some change.

### **How it works:**

[Pact](https://docs.pact.io/) has been identified as the leading
contract testing framework within the industry. It supports a variety of
programming languages and has a thriving community. In our case pact-jvm
is used to implement pact testing.

![](attachments/119670027/119675070.png){height="250"}

  

  

![](attachments/119670027/119675071.png){height="250"}

  

**On Consumer Side:**

-   Each Consumer defines what interaction its going to have with
    provider(like get, put methods) and the request and response body
    parameters(both header and body fields) used in those request
    methods.
-    Consumer generates pact file(using pact-jvm-consumer framework)
    which captures (usually a json file) the details of the expected
    interactions consumer wants to have with provider.
-   Then the file is shared with provider(usually through a shared
    location).
-   **On Provider Side:**
-   Testcases to verify each consumer pactfile is created and made part
    of provider build pipeline(this job kicks in just after provider is
    succefully deployed to test environment)
-   pact-jvm-provider framework library is used to parse each json
    pactfile and hit provider endpoint with requests and parses the
    response to ensure the interaction meets corresponding consumer
    expectation.

### **When not to use:**

It should be noted that while consumer interactions with provider are
documented through content and format of requests and responses,
Contract Tests are not meant for the following:

-   Testing new or existing providers where the functionality is not
    being driven by the needs of the consumer (eg. public APIs)
-   Testing providers where the consumer and provider teams do not have
    good communication channels.
-   Performance and load testing.
-   Functional testing of the provider as this is covered through API
    Functional Tests.
-   Situations where you cannot load data into the provider without
    using the API that you're actually testing (eg. public APIs).
-   Testing "pass through" APIs, where the provider merely passes on the
    request contents to a downstream service without validating them. 

  

## Attachments:

![](images/icons/bullet_blue.gif){width="8" height="8"}
[pact.png](attachments/119670027/119674597.png) (image/png)  
![](images/icons/bullet_blue.gif){width="8" height="8"}
[PactStep1.png](attachments/119670027/119675070.png) (image/png)  
![](images/icons/bullet_blue.gif){width="8" height="8"}
[PactStep2.png](attachments/119670027/119675071.png) (image/png)  

## Comments:

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Rajsing Mohapatro - As discussed can you please add the PACT JVM example here, thanks.</p>
<div class="smallfont" data-align="left" style="color: #666666; width: 98%; margin-bottom: 10px;">
<img src="images/icons/contenttypes/comment_16.png" width="16" height="16" /> Posted by 208534 at Jan 11, 2019 10:10
</div></td>
</tr>
</tbody>
</table>
