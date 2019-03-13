# Sample RestAssured Framework

## Rest Assured

 [Rest Assured](http://rest-assured.io/) is one of the most powerful
libraries for testing RESTful API using Java language. This should be
the first-choice when you need to test a REST. All tests should be
written in the [BDD (Behavior Driven
Development)](https://en.wikipedia.org/wiki/Behavior-driven_development) format
and its framework syntax is very clean and easy to use. The framework
sends a network request to an application under test and verifies the
response based on the expectations.

The main features:

-   Specification reuse
-   Response validation
-   XPath verification
-   Behavior-driven development syntax

  

## Serenity BDD

 Serenity is an open source test automation framework (also known as
Thucydides) that helps you write well-structured functional tests, and
provides outstanding test reports. The main advantage of Serenity
reporting is that it not only provides raw test results, but also a
detailed specification of the tested feature. The Serenity framework is
used by many organizations due to a wide variety of features which are
available out of the box.

 Here is a short list of its main features:

-   Out-of-the-box integration with the most popular test frameworks
    (JUnit, [Cucumber](https://www.blazemeter.com/blog/api-testing-with-cucumber-bdd-configuration-tips?utm_source=blog&utm_medium=BM_blog&utm_campaign=restful-api-testing-using-serenity-and-rest-assured-a-guide),
    Rest-Assured, [Selenium](https://www.blazemeter.com/blog/how-automate-testing-using-selenium-webdriver-jenkins-and-allure?utm_source=blog&utm_medium=BM_blog&utm_campaign=restful-api-testing-using-serenity-and-rest-assured-a-guide) and
    many others)
-   Many built-in features (parallel execution, screenshots for UI
    tests, Data Driven testing)
-   Detailed reports
-   Integration with any build tool (maven, gradle, ant)

## Sample project - Qantas Mobile App Backend API:

<https://stash.qcpaws.qantas.com.au/projects/AMS04-A868/repos/mobileapiautomationsuite/browse>

<span class="underline">**How to automate new API ?**</span>

1.  Clone the automation project repository from the below mentioned
    project location.
2.  Create an appropriate package
    under [test.com](http://test.com/).qantas.api for the new api to be
    automated
3.  Create a new package setup' and new class  as shown below for
    setting the baseURI configuration by choosing the appropriate enum
    value for the new API URL.This base class  
    public class SetUp {  

            @ClassRule public static final BaseURIConfiguration res = new BaseURIConfiguration();

            @BeforeClass public static void baseSetUp() {

                //Assuming that there is only one EndPoint for each API if (res != null)
                    RestAssured.baseURI = res.getServiceMap().get(MobileAppsServices.BOOKINGS.getName()).get(0).getUrl();
            }

        }

      

4.  Create a package 'testbase' and a new class for the new API test
    base which will have the API test suite configuration and the health
    check for the new API.Please refer to the example below  

        public class BookingAggregatorTestBase extends SetUp {

            Health health = new Health();

            public static TestSuite prepareTestSuite(TestSuite suite) {
                suite.addTest(new JUnit4TestAdapter(PNRWithCarAndHotelBooking.class));
                suite.addTest(new JUnit4TestAdapter(PNRBooking.class));
                suite.addTest(new JUnit4TestAdapter(PNRWithNonQantasBooking.class));
                suite.addTest(new JUnit4TestAdapter(FrequentFlyerBooking.class));
                suite.addTest(new JUnit4TestAdapter(FrequentFlyerWithCarAndHotelBooking.class));
                suite.addTest(new JUnit4TestAdapter(FrequentFlyerMultipleBookings.class));
                suite.addTest(new JUnit4TestAdapter(DomesticHotelOffers.class));
                suite.addTest(new JUnit4TestAdapter(InternationalFlighttoAusHotelOffers.class));
                suite.addTest(new JUnit4TestAdapter(NoHotelOffers.class));
                return suite;
            }

            @Before public void performHealthCheck() {

                if (!health.isHealthCheckSuccessful(RestAssured.baseURI, ENDPOINT))
                    fail("Unable to run the test due to health check failure");
            }
        }

      
      

5.  create a package 'health' and configure the appropriate health check
    endpoint for the new API.Please refer to the example below. This
    endpoint will be used by the testbase class mentioned above  

        public interface EndPoint {

            public static final String ENDPOINT = "/health";
        }

6.  Create a package scenarios and create new classes for the various
    test scenarios as shown in the example below.Please make sure that
    the appropriate squad name is mentioned in the @withTag
    annotation.  
    Also include the Step definitions class created(mentioned in the
    below step) as the story so that it gives the context of the
    scenarios. 

        @RunWith(SerenityParameterizedRunner.class)
        @Story(RetrieveBookingsWithPNR.class)
        @WithTag("squad:Travel")
        public class DomesticHotelOffers extends BookingAggregatorTestBase {

            private final static Logger LOGGER = Logger.getLogger(DomesticHotelOffers.class.getName());
            private final TestDataModel testData;

            @Steps RetrieveBookingsWithPNR retrieveBookings;

            public DomesticHotelOffers(TestDataModel value) {
                this.testData = value;
            }

            @TestData public static Collection<Object[]> testData() {

                List<TestDataModel> testData = DataSetUp.getExcelData().get(CategoryTypes.NON_FREQUENT_FLYER.getName());
                Optional<List<TestDataModel>> testDataModelOptional = Optional.of(testData);
                testData = testDataModelOptional.map(t -> {
                    return t.stream().filter(x -> x.getJourneyType().equals("oneway")).collect(Collectors.toList());
                }).get();
                return TestDataFormat.getObjectArray(testData);
            }

            @Test @Title(value = "Scenario: Add trip for a PNR with eligibility for hotel offers")
            public void domesticHotelOffersTest() {

                String headerValue = retrieveBookings.validPNRwithFlightBooking(testData);
                BookingResponse response = retrieveBookings.getBookingPNRResponse(headerValue, RestAssured.baseURI);
                retrieveBookings.assertBookingPNRHotelOffersResponse(testData, response);

            }
        }

7.  Create a package 'steps' and new classes which will have all the
    step definitions to support the test scenarios.Please refer to the
    example below  
      

        public class RetrieveBookingsWithPNR {

            private final static Logger LOGGER = Logger.getLogger(RetrieveBookingsWithPNR.class.getName());

            @Step @Title("Given: A valid PNR with flight,car and hotel booking")
            public String validPNRwithCarAndHotelBooking(TestDataModel testDataModel) {
                return constructPNRHeader(testDataModel);
            }

        @Step@Title("When: Making a request for retreiving the booking details")
        public BookingResponse getBookingPNRResponse(String headerValue, String uri) {

            BookingResponse bookingResponse;
            Response response = given().accept(Constants.ACCEPT)
                    .header(Constants.HEADER_PNR_LAST_NAME, headerValue)
                    .when().get(uri)
                    .then()
                    .log()
                    .all()
                    .extract()
                    .response();
            ObjectMapper objectMapper = new ObjectMapper();
            if (response.getStatusCode() == 200) {
                LOGGER.log(Level.INFO, "Successful response for the PNR:SURNAME " + headerValue);
                try {
                    bookingResponse = objectMapper.readValue(response.body().asString(), BookingResponse.class);
                    return bookingResponse;
                } catch (IOException ie) {
                    LOGGER.log(Level.SEVERE, "Failed to generate the booking response");
                    return null;
                }
            } else {
                LOGGER.log(Level.INFO, "No Response received for the PNR:SURNAME " + headerValue);
                return null;
            }
        }

        @Step@Title("Then: Get an appropriate response withe flight booking details")
        public void assertBookingPNRFlightResponse(TestDataModel testDataModel, BookingResponse response) {

            commonAssertions(testDataModel, response);
        }

    }

8.  Include the new API suite configuration to the main RegressionSuite
    class under the suite package as shown in the example below  

        suite = BookingAggregatorTestBase.prepareTestSuite(suite);

9.  The test report will be generated by the 'mvn clean verify' command
    can be found in the below mentioned location   
    ../MobileAutomationSuite/target/site/serenity/index.html
