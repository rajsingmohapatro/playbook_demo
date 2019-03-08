# Mongo DB

## **Overview**

MongoDB is an open-source document database and leading NoSQL database.
MongoDB is written in C++. This tutorial will give you great
understanding on MongoDB concepts needed to create and deploy a highly
scalable and performance-oriented database

MongoDB is a cross-platform, document oriented database that provides,
high performance, high availability, and easy scalability. MongoDB works
on concept of collection and document.

From an Automation perspective, MongoDB is a great source to save the
testdata. Also, You can use a Java-MongoClient for any automated
verification of MongoDB.

## **Sample Project:**

**<https://github.com/boaglio/mongodb-java-examples>**

## **How to use MongoClient ?**

## **Prerequisites**

-   A running MongoDB on localhost using the default port for
    MongoDB `27017`

-   MongoDB Driver. 

## **Make a Connection**

Use [`MongoClient()`](http://mongodb.github.io/mongo-java-driver/3.4/javadoc?com/mongodb/MongoClient.html) to
make a connection to a running MongoDB instance.

The `MongoClient` instance represents a pool of connections to the
database; you will only need one instance of class `MongoClient` even
with multiple threads.

### Connect to a Single MongoDB instance

The following example shows five ways to connect to the
database `mydb` on the local machine. If the database does not exist,
MongoDB will create it for you.

To connect to a single MongoDB instance:

-   You can instantiate a MongoClient object without any parameters to
    connect to a MongoDB instance running on localhost on port `27017`:

<!-- -->

    MongoClient mongoClient = new MongoClient();

-   You can explicitly specify the hostname to connect to a MongoDB
    instance running on the specified host on port `27017`:

<!-- -->

    MongoClient mongoClient = new MongoClient( "localhost" );

-   You can explicitly specify the hostname and the port:

<!-- -->

    MongoClient mongoClient = new MongoClient( "localhost" , 27017 );

-   You can specify
    the [`MongoClientURI`](http://mongodb.github.io/mongo-java-driver/3.4/javadoc?/com/mongodb/MongoClientURI.html) connection
    string:

<!-- -->

     MongoClientURI connectionString = new MongoClientURI("mongodb://localhost:27017");
     MongoClient mongoClient = new MongoClient(connectionString);

The connection string mostly follows [RFC
3986](http://tools.ietf.org/html/rfc3986), with the exception of the
domain name. For MongoDB, it is possible to list multiple domain names
separated by a comma. For more information on the connection string,
see [connection
string](http://docs.mongodb.org/manual/reference/connection-string).

## Access a Database

Once you have a `MongoClient` instance connected to a MongoDB
deployment, use
the [`MongoClient.getDatabase()`](http://mongodb.github.io/mongo-java-driver/3.4/javadoc?com/mongodb/MongoClient.html#getDatabase-java.lang.String-) method
to access a database.

Specify the name of the database to the `getDatabase()` method. If a
database does not exist, MongoDB creates the database when you first
store data for that database.

The following example accesses the `mydb` database:

     MongoDatabase database = mongoClient.getDatabase("mydb");

`MongoDatabase` instances are immutable.

## Access a Collection

Once you have a `MongoDatabase` instance, use
its [`getCollection()`](http://mongodb.github.io/mongo-java-driver/3.4/javadoc?com/mongodb/client/MongoDatabase.html#getCollection-java.lang.String-) method
to access a collection.

Specify the name of the collection to the `getCollection()` method. If a
collection does not exist, MongoDB creates the collection when you first
store data for that collection.

For example, using the `database` instance, the following statement
accesses the collection named `test`in the `mydb` database:

    MongoCollection<Document> collection = database.getCollection("test");

`MongoCollection` instances are immutable.

## Create a Document

To create the document using the Java driver, use
the [`Document`](http://mongodb.github.io/mongo-java-driver/3.4/javadoc?org/bson/Document.html) class.

For example, consider the following JSON document:

      {
       "name" : "MongoDB",
       "type" : "database",
       "count" : 1,
       "versions": [ "v3.2", "v3.0", "v2.6" ],
       "info" : { x : 203, y : 102 }
      }

To create the document using the Java driver, instantiate
a `Document` object with a field and value, and use
its [`append()`](http://mongodb.github.io/mongo-java-driver/3.4/javadoc?org/bson/Document.html#append) method
to include additional fields and values to the document object. The
value can be another `Document` object to specify an embedded document:

     Document doc = new Document("name", "MongoDB")
                    .append("type", "database")
                    .append("count", 1)
                    .append("versions", Arrays.asList("v3.2", "v3.0", "v2.6"))
                    .append("info", new Document("x", 203).append("y", 102));

## Insert a Document

Once you have the `MongoCollection` object, you can insert documents
into the collection.

### Insert One Document

To insert a single document into the collection, you can use the
collection’s [`insertOne()`](http://mongodb.github.io/mongo-java-driver/3.4/javadoc?com/mongodb/client/MongoCollection.html#insertOne-TDocument-) method.

    collection.insertOne(doc);

  

##### NOTE

If no top-level `_id` field is specified in the document, MongoDB
automatically adds the `_id` field to the inserted document.

  

### Insert Multiple Documents

To add multiple documents, you can use the
collection’s [`insertMany()`](http://mongodb.github.io/mongo-java-driver/3.4/javadoc?com/mongodb/client/MongoCollection.html#insertMany-java.util.List-) method
method which takes a list of documents to insert.

The following example will add multiple documents of the form:

    { "i" : value }

Create the documents in a loop and add to the `documents` list:

    List<Document> documents = new ArrayList<Document>();
    for (int i = 0; i < 100; i++) {
        documents.add(new Document("i", i));
    }

To insert these documents to the collection, pass the list of documents
to
the [`insertMany()`](http://mongodb.github.io/mongo-java-driver/3.4/javadoc?com/mongodb/client/MongoCollection.html#insertMany-java.util.List-) method.

    collection.insertMany(documents);

## Query the Collection

To query the collection, you can use the
collection’s [`find()`](http://mongodb.github.io/mongo-java-driver/3.4/javadoc?com/mongodb/client/MongoCollection.html#find--) method.
You can call the method without any arguments to query all documents in
a collection or pass a filter to query for documents that match the
filter criteria.

The [`find()`](http://mongodb.github.io/mongo-java-driver/3.4/javadoc?com/mongodb/client/MongoCollection.html#find--) method
returns
a [`FindIterable()`](http://mongodb.github.io/mongo-java-driver/3.4/javadoc?com/mongodb/client/FindIterable.html) instance
that provides a fluent interface for chaining other methods.

### Find the First Document in a Collection

To return the first document in the collection, use
the [`find()`](http://mongodb.github.io/mongo-java-driver/3.4/javadoc?com/mongodb/client/MongoCollection.html#find--) method
without any parameters and chain to `find()` method
the [`first()`](http://mongodb.github.io/mongo-java-driver/3.4/javadoc?com/mongodb/client/MongoIterable.html#first--) method.

If the collection is empty, the operation returns null.

  

The following example prints the first document found in the collection.

    Document myDoc = collection.find().first();
    System.out.println(myDoc.toJson());

  
