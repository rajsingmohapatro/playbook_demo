# Automation Principles

This section describes the principles for implementing test automation for any Qantas Product / Project teams regardless of what systems and services they own and utilise. While there would be some teams within Qantas that are starting/exploring test automation in their products/projects, there are some other teams that have been around for sometime and have already setup various types of test automation in their areas. The principles mentioned here are generalist in advice and can be tailored to suit individual project/product team needs.

In any Software Development Life Cycle methodology, automated testing is an important activity. To enable faster releases, test automation becomes ever more important due to the quick feedback response that it provides to the development teams about the health of the application. 

In order to get this quick feedback, a comprehensive suite of automated tests should be available, which are fast to run and test results should be consistent and reliable. Any manual testing required should be minimal.

The testing quadrant diagram is an industry standard guide for what needs to be considered when testing in most environments and lists the various types of tests that should be included.  It should be noted that this quadrant is a standard recommendation for reference only and is not
the "**silver bullet**" of what needs to be completed. While the principles remain the same, this quadrant needs to be considered and reviewed for different type of projects, projects and releases and the most appropriate mix selected dependent on the scope, impact and overall risk.

  

### Pyramid of Test Automation

For the purpose of achieving fast feedback, majority of the
verifications should be done as part of the development of new features. In other words development and testing should be a coherent activity, and quality should be “baked in” right from the start by ensuring that
what is being developed works and that it hasn’t broken existing functionality. The industry standard recommendations for split of Q1 and Q2 automated tests as per the Testing quadrant below, should roughly follow the concept of "Test Automation Pyramid" as described [here](https://martinfowler.com/bliki/TestPyramid.html). This can be interpreted as per the diagram below:

![](../images/113028109/119670956.png)

![](../images/113028109/119670957.png)

![](../images/113028109/119671994.png)