# Sample Cucumber-Selenium-Java Framework

-   [Introduction](#SampleCucumber-Selenium-JavaFramework-Introduction)
-   [What is the
    capability](#SampleCucumber-Selenium-JavaFramework-Whatisthecapability)
-   [Framework Versioning
    Strategy](#SampleCucumber-Selenium-JavaFramework-FrameworkVersioningStrategy)
-   [Your test project looks
    like](#SampleCucumber-Selenium-JavaFramework-Yourtestprojectlookslike)
-   [Framework
    Configurations](#SampleCucumber-Selenium-JavaFramework-FrameworkConfigurations)
-   [Object Models](#SampleCucumber-Selenium-JavaFramework-ObjectModels)
-   [Setup new test
    project](#SampleCucumber-Selenium-JavaFramework-Setupnewtestproject)
-   [Common Function
    Helpers](#SampleCucumber-Selenium-JavaFramework-CommonFunctionHelpers)
-   [Advanced
    Features](#SampleCucumber-Selenium-JavaFramework-AdvancedFeatures)

  

# **Introduction**

[Qantas web automation test framework
v2.0](https://stash.qcpaws.qantas.com.au/projects/AMS02-A974/repos/qwebauto/browse) is
extracted from q.com regression test, which is the largest and most
stable test suite in Qantas. This front-end test framework uses Java +
Cucumber-JVM based tool sets, aiming to offer great capabilities to
automate most front-end tests. By using this framework, a test suite can
be setup in minutes without from scratch.

This framework is more like an open-sourced project, each automation
tester once working on this framework, is not only a user but also a
contributor to this framework. Any concerns to this framework either
areas can be improved are open and welcome to discuss. 

# **What is the capability**

Note: Confluence preview would not show up all the contents of this
slide. Please download it to your local machine.

# **Framework Versioning Strategy**

Qantas web automation test framework is built in Java programming
language and it is released to Qantas internal Nexus server. The latest
version can be checked [on
Stash](https://stash.qcpaws.qantas.com.au/projects/AMS02-A974/repos/qwebauto/browse/pom.xml). 

-   **Version Scheme**: MajorVersion.MinorVersion.BuildNumber (e.g.
    2.1.12)
-   Version Change: For minor changes like bug fix not impacting
    dependent projects , there will be no change to major or minor
    version number. Every time build framework will release a new
    version with the same major and minor version and new build
    number. When new feature introduced or any change impacts existing
    test project, minor version should be updated. Dependent projects
    need to manually update the framework version, fix any potential
    incompatibilities.
-   Use Version Range in Project: In dependent projects, please use a
    version range to allow auto update. e.g. \[2.1.0,2.2.0). It will
    automatically check the latest version starting with 2.1 in Nexus
    during build.

**Maven Dependency**

``` xml
<dependency>
    <groupId>com.qantas</groupId>
    <artifactId>qantas-web-automation-framework</artifactId>
    <version>${framework.version}</version>
</dependency>


<repositories>
    <repository>
        <id>nexus-internal</id>
        <name>Qantas jars</name>
        <url>http://nexus.qcpaws.qantas.com.au/nexus/content/repositories/internal</url>
    </repository>
</repositories>
```

# **Your test project looks like**

As mentioned above, test framework is released as jar file in internal
Nexus server. In your project, you will see very little about the
framework. However, you need to follow the structure appropriately to
use this framework.

![](attachments/119670968/119670974.png){width="300"}

Framework can not do everything to set up a new test project. But it do
provide some suggestions to set up a test project with good structure.

-   **Java Package**: package number should starts with
    com.qantas.(project). In Qantas page objects are divided to 3 parts:
    page, widget and component. Then you need to follow standard
    cucumber approach to have steps and test runners.
-   **Test Cases**: As adviced by Cucumber, feature files are located
    under src/test/resoucres/features and grouped by feature name.
-   **Configuration**: This folder is must to have and used to configure
    test framework and your own settings.
-   **drivers**: Should follow the same structure to place your own test
    drivers depending on your browser version and operation system.
    Otherwise, browser initiation would fail because framwork can not
    find the right driver file.
-   **scripts**: If you prefer to use embeded build script to manage
    your build process. You can have this file and configure Bamboo to
    use it as build script.  
      

# **Framework Configurations**

Framework provides 4 type of configuration files to setup your test
project.

1.  **Global Configuration**: This config is used across all tests
    during the whole run. It indicates which environment used, which
    browser used, test report settings and so on.  
    <https://stash.qcpaws.qantas.com.au/projects/AMS02-A974/repos/qwebauto/browse/config/global.yml>  
    ![](attachments/119670968/119670979.png){height="250"}  
    **Note**: All global settings can be overwritten from CI to allow
    maximum customerised test run.   
    ![](attachments/119670968/119670978.png){height="250"}  
      
2.  **Test Data Configuration**: This file contains test data used for
    each environment. Data structure is env → feature → name:value. You
    can use ResourceManager.getTestDataConfig(String feature, String
    name) anywhere to easily retrieve your test data.   
    https://stash.qcpaws.qantas.com.au/projects/AMS02-A974/repos/qwebauto/browse/config/testdata.ymlNote:
    In case test data is only used for a specific feature, no potential
    to share with other tests or unlikely to change, it is better to
    hardcode it in your test step file instead of upscaling
    configuration file.   
      
    ![](attachments/119670968/119670977.png){height="250"}
3.  **Url Configuration**:  This file is pretty much similar to test
    data configuration. This file is separated to store url
    configurations only. It has 2 level configs env→
    name:value. ResourceManager.getUrlConfig(String name) used to
    retrive values from url configuration. Urls can be set in a flexible
    mode as below:  
    ![](attachments/119670968/119670976.png){height="250"}

    How it works? Url configuration offers two ways to set up url,
    absolute path and relative path.

    1.  Absolute Path: if a url value starts with 'http', getUrlConfig
        function will return this value straight away.

    2.  Relative Path: On the other hand, if a url value does not start
        with 'http', it automatically uses homepage http scheme and
        domain as prefix. For instance in upper setting, the
        register\_path value in test environment is
        actually <http://www.test.qantas.com/register>  
          

4.  **Remote Driver**: remote driver config file is used to store
    different selenium/appium driver capability details and mapping to a
    name key, which need be indicated in global setting.  
    ![](attachments/119670968/119670975.png){height="206"}  
    To use a remote driver, 3 configs in global file need to be set.
    Using remote driver, hub address and which capability to use. This
    setting can be used for BrowserStack integration or any other kind
    of remote driver integration.  
    is\_remote\_driver: "true"  
    selenium\_hub address:
    "https://callistoreplatfo1:8zL7NsqjqPDo2VgsBqRT@hub-cloud.browserstack.com/wd/hub"   
    remote\_driver: "win10\_chrome62"  

What are environments? In Qantas, usually we have 3 type of
environments: test, staging and production. We do manual test and
automation implementation in test environment, regression test and
release test in staging environment and regular regression test in
production. For pre-release(blue environment) testing, the 'env' value
should remain 'production' and 'is\_blue\_environment' should be true.

In this framework, environment value is indicated in global setting and
can be overwritten from CI. In test data and url configuration files,
environment name is used as the
key. ResourceManager.getTestDataConfig(String feature, String name) 
and ResourceManager.getUrlConfig(String name) method relies on
environment value in global setting to return value.

What is default environment? Sometimes we use same test data or url for
all environments. In this case you do not have to setup value for each
environment. Place the value under default environment and it will be
picked up if this value does not exist under indicated environment. 

**What is ResourceManager**? ResourceManager is a Java object instance
injected to dependency to store and share variables across steps. It is
not only providing static methods to retrieve configuration settings,
but also offering 

setTestData(String name, Object object), getTestData(String name),
hasTestData(String name) for use to store values within individual test.
In other words, configuration values are used across entire test run
while test data is automatically cleaned up after each scenario.

https://stash.qcpaws.qantas.com.au/projects/AMS02-A974/repos/qwebauto/browse/src/main/java/com/qantas/framework/config/ResourceManager.java

**How to set multiple execution threads**? Execution thread amount is
set in annotation of test runner, which means it is constant and cannt
be dynamically changed. Open RunCukesTest.java and locate
ExtendedCucumberOptions annotation and then you will see the setting.

  

# **Object Models**

Qantas Web Automation Test Framework provides 5 type of models so
far. https://stash.qcpaws.qantas.com.au/projects/AMS02-A974/repos/qwebauto/browse/src/main/java/com/qantas/framework/model

-   Page Model
-   Widget Model
-   Component Model
-   Steps Model
-   Cookie Model

It is your choice to use it or not. By extending project objects from
these models correspondingly, you can use pre-defined parent level
common methods to ease your coding and also you agree to implement those
interfaces as contract.

# **Setup new test project**

1.  **Create a new project folder on your local machine**
2.  **Navigate to project folder through Command / Terminal**
3.  **Use git command to clone framework project to local**  
    command: git
    clone https://\*\*\*\*\*\*@stash.qcpaws.qantas.com.au/scm/ams02-a974/qwebauto.git
4.  **Switch to example branch**  
    command: git checkout example
5.  **Remove git element from project**  
    Remove .git sub folder from your project. It is a hidden folder so
    please make sure it is visible before any action through no matter
    GUI or Commandline.
6.  **Customerise your own project**  
    Open pom.xml, change **artifactId **and **name **with your project
    info.  
    ![](attachments/119670968/119670970.png){width="400"}
7.  **Push to your project repository**  
    1.  Initialize project by running the following commands  

            git init
            git add --all
            git commit -m "Initial Commit" 

          

    2.  Push your files to the repository by running the following
        commands

            git remote add origin https://username@your.bitbucket.domain:7999/yourproject/repo.git 
            git push -u origin master

# **Common Function Helpers**

Framework provides a few helpers that contains common and advanced
methods used in your test implementation.

-   ActionHelper: Advanced functions in addition to standard selenium
    action.
-   WebElementHelper: Advanced functions in addition to standard
    selenium web element.
-   PageAssertionHelper: Assert a page with url, title or element
    presence.
-   URLHelper: Provide advanced functions to build a url or assert a
    url.
-   CalendarHelper: Provide Java-alike calendar functions not based on
    local machine time but Qantas Server Time.

# **Advanced Features**

-   Mock Proxy (Integration Test Extension): [Manipulating HTTP
    Request/Response](Manipulating_HTTP_Request_Response)
-   Automated Accessibility Testing: [Automated Accessibility
    Testing](Automated_Accessibility_Testing)

## Attachments:

![](images/icons/bullet_blue.gif){width="8" height="8"} [Qantas Web
Automation Test Framwork.pptx](attachments/119670968/119670969.pptx)
(application/vnd.openxmlformats-officedocument.presentationml.presentation)  
![](images/icons/bullet_blue.gif){width="8" height="8"}
[image2018-1-24\_15-6-1.png](attachments/119670968/119670970.png)
(image/png)  
![](images/icons/bullet_blue.gif){width="8" height="8"}
[image2018-1-24\_14-41-56.png](attachments/119670968/119670971.png)
(image/png)  
![](images/icons/bullet_blue.gif){width="8" height="8"}
[image2018-1-24\_14-24-51.png](attachments/119670968/119670972.png)
(image/png)  
![](images/icons/bullet_blue.gif){width="8" height="8"} [Introduction to
Qantas Web Automation Test Framwork
2.0.pptx](attachments/119670968/119670973.pptx)
(application/vnd.openxmlformats-officedocument.presentationml.presentation)  
![](images/icons/bullet_blue.gif){width="8" height="8"}
[image2018-1-24\_11-2-50.png](attachments/119670968/119670974.png)
(image/png)  
![](images/icons/bullet_blue.gif){width="8" height="8"}
[image2018-1-24\_10-28-47.png](attachments/119670968/119670975.png)
(image/png)  
![](images/icons/bullet_blue.gif){width="8" height="8"}
[image2018-1-24\_9-59-13.png](attachments/119670968/119670976.png)
(image/png)  
![](images/icons/bullet_blue.gif){width="8" height="8"}
[image2018-1-23\_16-52-42.png](attachments/119670968/119670977.png)
(image/png)  
![](images/icons/bullet_blue.gif){width="8" height="8"}
[image2018-1-23\_16-48-52.png](attachments/119670968/119670978.png)
(image/png)  
![](images/icons/bullet_blue.gif){width="8" height="8"}
[image2018-1-23\_16-46-38.png](attachments/119670968/119670979.png)
(image/png)  
