# AWS Dynamo DB

**Overview**

DynamoDB allows users to create databases capable of storing and
retrieving any amount of data, and serving any amount of traffic. It
automatically distributes data and traffic over servers to dynamically
manage each customer's requests, and also maintains fast performance.

The two main advantages of DynamoDB are scalability and flexibility. It
does not force the use of a particular data source and structure,
allowing users to work with virtually anything, but in a uniform way.

Its design also supports a wide range of use from lighter tasks and
operations to demanding enterprise functionality. It also allows simple
use of multiple languages: Ruby, Java, Python, C\#, Erlang, PHP, and
Perl

  

**Sample project- Webchatbot-DynamoDB:**

<https://stash.qcpaws.qantas.com.au/projects/AMS04-A868/repos/vabothandler/browse>

The component bothandler talks to DynamoDB to save a few details.

In the view of Automation, We can develop a framework which will act as
a service and query this DB to verify the data. 

## Querying with Java

Queries in Java allow you to query tables and secondary indices. They
require specification of partition keys and equality conditions, with
the option to specify sort keys and conditions.

The general required steps for a query in Java include creating a
DynamoDB class instance, Table class instance for the target table, and
calling the query method of the Table instance to receive the query
object.

The response to the query contains an ItemCollection object providing
all the returned items.

The following example demonstrates detailed querying −

    DynamoDB dynamoDB = new DynamoDB ( new AmazonDynamoDBClient(new ProfileCredentialsProvider())); Table table = dynamoDB.getTable("Response"); QuerySpec spec = new QuerySpec() .withKeyConditionExpression("ID = :nn") .withValueMap(new ValueMap() .withString(":nn", "Product Line 1#P1 Thread 1")); ItemCollection<QueryOutcome> items = table.query(spec); Iterator<Item> iterator = items.iterator(); Item item = null; while (iterator.hasNext()) { item = iterator.next(); System.out.println(item.toJSONPretty()); }

The query method supports a wide variety of optional parameters. The
following example demonstrates how to utilize these parameters −

    Table table = dynamoDB.getTable("Response"); QuerySpec spec = new QuerySpec() .withKeyConditionExpression("ID = :nn and ResponseTM > :nn_responseTM") .withFilterExpression("Author = :nn_author") .withValueMap(new ValueMap() .withString(":nn", "Product Line 1#P1 Thread 1") .withString(":nn_responseTM", twoWeeksAgoStr) .withString(":nn_author", "Member 123")) .withConsistentRead(true); ItemCollection<QueryOutcome> items = table.query(spec); Iterator<Item> iterator = items.iterator(); while (iterator.hasNext()) { System.out.println(iterator.next().toJSONPretty()); }
