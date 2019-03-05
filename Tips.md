# Tips

## **1.Take screenshot for debugging**

            **Capture screenshot on test fail** --  By default, 
screenshot is automatically taken on test failing, you can find it in
the test report right after the test details of the failed scenario.

            **Capture screenshot on scenario finish** -- To enable
taking screenshot for all scenarios regardless success or fail, you can
set the global variable 'take\_screenshot\_all' to 'true' in bamboo plan
variable / global.yml.

            **Capture screenshot inside a step** – To capture a
screenshot inside a step, you only need to add 1 line of code to
indicate the scope, page, widget or component. Web driver will focus on
the target on attach the screenshot into test report.

``` java
new ActionHelper(driver).capture(scenario);
new ActionHelper(driver).capture(scenario, element);
new ActionHelper(driver).capture(scenario, component);
```

## ** 2.Broken Links Scanner**

           BrokenLinkHelper is provided in [Sample
Cucumber-Selenium-Java
Framework](Sample_Cucumber-Selenium-Java_Framework) to enable scanning
broken links in a page or element. To use this function, navigate to a
page first, and then a line of code as below can scan all links. You can
also customise this BrokenLinkHelper regarding to threads, retries,
etc. 

``` java
new BrokenLinkHelper(driver).scan();  //Scan all links and return a list of broken links
new BrokenLinkHelper(driver).doAssert(); //Scan all links and throw out exception if any broken link found.
new BrokenLinkHelper(componentElement).scan(); //Scan all links inside an element and return a list of broken links
new BrokenLinkHelper(componentElement).doAssert(); //Scan all links inside an element and throw out exception if any broken link found.
```
