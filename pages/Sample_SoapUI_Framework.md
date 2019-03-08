# Sample SoapUI Framework

## **Overview**

SOAP UI is the leading open source cross-platform APITesting tool.
SOAPUI allows testers to execute automated functional, regression,
compliance, and load tests on different Web API. SOAPUI supports all the
standard protocols and technologies to test all kinds of API's. SOAPUI
interface is simple that enables both technical and non-technical users
to use seamlessly.

Important features of SOAPUI :

1) Functional Testing 

2) Security Testing

3) Load Testing

4) Supported Protocols/Technologies**:** SOAP, WSDL,HTTP,HTTPS,REST,
JDBC,JMS

  

**Sample project:**

<https://github.com/SmartBear/soapui-sample-projects>

How to perform automation test for web services using SoapUI?

Follow the steps to perform automation test for web services by creating
a new Soap Project:

1) Go to the File and then click on New Soap Project.

[](http://testingfreak.com/wp-content/uploads/2015/07/soap2.png)

[](http://testingfreak.com/wp-content/uploads/2015/07/soap3.png)

2) Enter Project Name . You can enter any name of your choice.

3) Enter Initial WSDL url –

http://www.webservicex.net/CurrencyConvertor.asmx?wsdl

WSDL is nothing but end point url which should be provided to test web
services.

[](http://testingfreak.com/wp-content/uploads/2015/07/soap4.png)

4) Click OK.

Once you click OK you will see a new project has been created in left
side, this project is to convert the currency of one country to another
country.

[](http://testingfreak.com/wp-content/uploads/2015/07/soap5.png)

5) Double click on Request1 will load the script.

[](http://testingfreak.com/wp-content/uploads/2015/07/soap6.png)

6) We have Request ready and now have to see the response after adding
the value to the request and trigger it.

7) Now I am going to test this service by adding the FromCurrency as USD
and ToCurrency as INR and trigger the request.

[](http://testingfreak.com/wp-content/uploads/2015/07/soap7.png)

You can run the script by clicking on green color arrow shown on the
top.

Now we can see the response here that currency has been converted and
fetched in the response, so this web service works. Similarly we can
test this web service by changing the request.

Now lets create different test cases with different values:

1) Click on (+) logo to add test case.

[](http://testingfreak.com/wp-content/uploads/2015/07/soap8.png)

[](http://testingfreak.com/wp-content/uploads/2015/07/soap9.png)

2) You can give any name of this test suite. If you won’t give any name
it will take default name as TestSuite1.

3) Click OK button will ask to enter Test Case name. You can enter any
name.

[](http://testingfreak.com/wp-content/uploads/2015/07/soap10.png)

4) Click OK button will open another pop up Add Request to TestCase-

[](http://testingfreak.com/wp-content/uploads/2015/07/soap11.png)

5) Click OK button again will create the test case.

[](http://testingfreak.com/wp-content/uploads/2015/07/soap12.png)

6) To run this test case simply click on green arrow shown on the top

It will take few seconds and your test will be completed. If your test
gets passed you will see it is green in color otherwise it will be red
in case test fails.

[](http://testingfreak.com/wp-content/uploads/2015/07/soap13.png)

Similarly you can create more than one test cases by adding different
values in the request.

How to add and validate Assertion in test cases:

1) Double click on ConversionRate-Request1.

2) Click on Adds an assertion to this item icon shown on the top.

[](http://testingfreak.com/wp-content/uploads/2015/07/soap14.png)

3) Click on XPath Match and then click on Add button.

[](http://testingfreak.com/wp-content/uploads/2015/07/soap15.png)

4) Declare XPath expression which you want to validate and provide the
Expected Result in the box.

[](http://testingfreak.com/wp-content/uploads/2015/07/soap16.png)

5) Click on Save button and run the script by clicking on arrow shown on
the top.

[](http://testingfreak.com/wp-content/uploads/2015/07/soap17.png)

Once you run the script you can see the result at the bottom with
validation passed or failed.

[](http://testingfreak.com/wp-content/uploads/2015/07/soap18.png)
