# Relational DB

-   [Why Test an RDBMS](#RelationalDB-WhyTestanRDBMS)
-   [What Should We Test](#RelationalDB-WhatShouldWeTest)
-   [When Should We Test](#RelationalDB-WhenShouldWeTest)
-   [How to Test](#RelationalDB-HowtoTest)
    -   [Database Sandboxes](#RelationalDB-DatabaseSandboxes)
    -   [Writing Database Tests](#RelationalDB-WritingDatabaseTests)
    -   [Setting up Database
        Tests](#RelationalDB-SettingupDatabaseTests)
    -   [Test tools selection ](#RelationalDB-Testtoolsselection)
    -   [Database Testing and Data
        Inspection](#RelationalDB-DatabaseTestingandDataInspection)

[Relational database management systems
(RDBMSs)](http://www.agiledata.org/essays/relationalDatabases.html) often
persist mission-critical data which is updated by many applications and
potentially thousands if not millions of end users. Furthermore, they
implement important functionality in the form of database methods
(stored procedures, stored functions, and/or triggers) and database
objects (e.g. Java or C\# instances). The best way to ensure the
continuing quality of these assets, at least from a technical point of
view, you should have a full regression test suite which you can run on
a regular basis.

Continuous regression testing based approach to database testing. Just
as agile software developers take this approach to their application
code, we should also do the same for our databases.

# Why Test an RDBMS

The current state of the art in many organisations is for data
professionals to control changes to the database schemas, for developers
to visually inspect the database during construction, and to perform
some form of formal testing during the test phase at the end of the
lifecycle. Unfortunately, none of these approaches prove effective.
Application developers will often go around data management group
because too difficult to work with, too slow in the way they work, or
sometimes they don't even know they should be working together. The end
result is that the teams don't follow the desired data quality
procedures and as a result quality suffers. 

There are some other reasons why you need to develop a comprehensive
testing strategy for your RDBMS.

1.  Data is an important corporate asset. 
2.  Mission-critical business functionality is implemented in RDBMSs. 
3.  Many functions in your application are implemented in DB in the form
    of stored procedures, triggers, ... 
4.  Testing provides the concrete feedback required to identify
    defects. 
5.  Support for evolutionary development.

# What Should We Test

Below figure indicates what should be considered to test when it comes
to relational databases. The diagram is drawn from the point of view of
a single database, the dashed lines indicate threat boundaries,
indicating that you need to consider threats both within the database
(clear box testing) and at the interface to the database (black box
testing). The table lists the issues which you should consider testing
for both internally within the database and at the interface to it. 

![](http://www.agiledata.org/images/databaseTesting.jpg)

<table>
<tbody>
<tr class="odd">
<td><strong>Black-Box Testing at the Interface</strong></td>
<td><strong>White/Clear-Box Testing Internally Within the Database</strong></td>
</tr>
<tr class="even">
<td><ul>
<li>O/R mappings (including the meta data)</li>
<li>Incoming data values</li>
<li>Outgoing data values (from queries, stored functions, views ...)</li>
</ul></td>
<td><ul>
<li>Scaffolding code (e.g. triggers or updatable views) which support refactoring</li>
<li>Typical unit tests for your stored procedures, functions, and triggers</li>
<li>Existence tests for database schema elements (tables, procedures, ...)</li>
<li>View definitions</li>
<li>Referential integrity (RI) rules</li>
<li>Default values for a column</li>
<li>Data invariants for a single column</li>
<li>Data invariants involving several columns</li>
</ul></td>
</tr>
</tbody>
</table>

# When Should We Test

Agile software developers take a test-first approach to development
where they write a test before you write just enough production code to
fulfil that test. The steps of test first development (TFD) are
overviewed in the UML activity diagram. The first step is to quickly add
a test, basically just enough code to fail. Next you run your tests,
often the complete test suite although for sake of speed you may decide
to run only a subset, to ensure that the new test does in fact fail. You
then update your functional code to make it pass the new tests. The
fourth step is to run your tests again. If they fail you need to update
your functional code and retest. Once the tests pass the next step is to
start over.

[![](http://www.agiledata.org/images/tddSteps.jpg)](http://www.agiledata.org/essays/tdd.html)

Test-driven development (TDD) is an evolutionary approach to development
which combines test-first development and refactoring. When an agile
software developer goes to implement a new feature, the first question
they ask themselves is "Is this the best design possible which enables
me to add this feature?" If the answer is yes, then they do the work to
add the feature. If the answer is no then they refactor the design to
make it the best possible then they continue with a TFD approach. This
strategy is applicable to developing both your application code and your
database schema, two things that you would work on in parallel.

When you first start following a TDD approach to development you quickly
discover that to make it successful you need to automate as much of the
process as possible? Do you really want to manually run the same build
script(s) and the same testing script(s) over and over again? Of course
not. So, agile developers have created OSS tools such as ANT, Maven,
and Cruise Control (to name a few) which enable them to automate these
tasks. More importantly, it enables them to automate their database
testing script into the build procedure itself.

[![](http://www.ambysoft.com/artwork/agileLifecycle.jpg)](http://www.ambysoft.com/essays/agileLifecycle.html)

# How to Test

## Database Sandboxes

A common best practice on agile teams is to ensure that developers have
their own "sandboxes" to work in. A sandbox is basically a technical
environment whose scope is well defined and respected. Below
figure depicts the various types of sandboxes which your team may choose
to work in. In each sandbox you'll have a copy of the database. In the
development sandbox you'll experiment, implement new functionality, and
refactor existing functionality, validate your changes through testing,
and then eventually you'll promote your work once you're happy with it
to the project integration sandbox. In this sandbox you will rebuild
your system and then run all the tests to ensure you haven't broken
anything (if so, then back to the development sandbox). Occasionally, at
least once an iteration/cycle, you'll deploy your work to the level
(demo and pre-production testing), and rerun your test suite (including
database tests) each time that you do so to ensure that your changes
integrate with the changes made by other developers. Every so often
(perhaps once every six to twelve months) into production. The primary
advantage of sandboxes are that they help to reduce the risk of
technical errors adversely affecting a larger group of people than is
absolutely necessary at the time.

![](http://www.agiledata.org/images/sandboxes.gif)

## Writing Database Tests

There's no magic when it comes to writing a database test, you write
them just like you would any other type of test. Database tests are
typically a three-step process:

1.  **Setup the test**. You need to put your database into a known state
    before running tests against it. There are several strategies for
    doing so.
2.  **Run the test**. Using a database regression testing tool, run your
    database tests just like you would run your application tests.
3.  **Check the results**. You'll need to be able to do "table dumps" to
    obtain the current values in the database so that you can compare
    them against the results which you expected.

## Setting up Database Tests

To successfully test your database you must first know the exact state
of the database, and the best way to do that is to simply put the
database in a known state before running your test suite. There are two
common strategies for doing this:

1.  **Fresh start**. A common practice is to rebuild the database,
    including both creation of the schema as well as loading of initial
    test data, for every major test run (e.g. testing that you do in
    your project integration or pre-production test sandboxes).
2.  **Data reinitialization**. For testing in developer sandboxes,
    something that you should do every time you rebuild the system, you
    may want to forgo dropping and rebuilding the database in favor of
    simply reinitializing the source data. You can do this either by
    erasing all existing data and then inserting the initial data vales
    back into the database, or you can simply run updates to reset the
    data values. The first approach is less risky and may even be faster
    for large amounts of data.

An important part of writing database tests is the creation of test
data. You have several strategies for doing so:

1.  **Have source test data**. You can maintain an external definition
    of the test data, perhaps in flat files, XML files, or a secondary
    set of tables. This data would be loaded in from the external source
    as needed.
2.  **Test data creation scripts**. You develop and maintain scripts,
    perhaps using data manipulation language (DML) SQL code or simply
    application source code (e.g. Java or C\#), which does the necessary
    deletions, insertions, and/or updates required to create the test
    data.
3.  **Self-contained test cases**. Each individual test case puts the
    database into a known state required for the test.

These approaches to creating test data can be used alone or in
combination. A significant advantage of writing creation scripts and
self-contained test cases is that it is much more likely that the
developers of that code will place it under configuration management
(CM) control. Although it is possible to put test data itself under CM
control, worst case you generate an export file that you check in, this
isn’t a common practice amongst traditional data professionals and
therefore may not occur as frequently as required. 

## Test tools selection 

<table>
<tbody>
<tr class="odd">
<td><strong>Category</strong></td>
<td><strong>Description</strong></td>
<td><strong>Examples</strong></td>
</tr>
<tr class="even">
<td>Data Privacy Tools</td>
<td>Data privacy, or more generally information privacy, is a critical issue for many organisations. Many organisations must safeguard data by law due to regulatory compliance concerns.</td>
<td><ul>
<li><a href="http://www-01.ibm.com/software/data/optim/protect-data-privacy/">IBM Optim Data Privacy</a> tools</li>
</ul></td>
</tr>
<tr class="odd">
<td>Testing tools for load testing</td>
<td>Tools simulate high usage loads on your database, enabling you to determine whether your system's architecture will stand up to your true production needs.</td>
<td><ul>
<li><a href="http://www.empirix.com/">Empirix</a></li>
<li><a href="http://www.mercury.com/us/solutions/application-delivery/">Mercury Interactive</a></li>
<li><a href="http://www.radview.com/">RadView</a></li>
<li><a href="http://www.webperformanceinc.com/">Web Performance</a></li>
</ul></td>
</tr>
<tr class="even">
<td>Test Data Generator</td>
<td>Developers need test data against which to validate their systems. Test data generators can be particularly useful when you need large amounts of data, perhaps for stress and load testing.</td>
<td><ul>
<li><a href="http://www.quest.com/datafactory/">Data Factory</a></li>
<li><a href="http://www.datatect.com/">Datatect</a></li>
<li><a href="http://www.sqledit.com/dg/">DTM Data Generator</a></li>
<li><a href="http://www.turbodata.ca/">Turbo Data</a></li>
</ul></td>
</tr>
<tr class="odd">
<td>Test Data Management</td>
<td>Your test data needs to be managed. It should be defined, either manually or automatically (or both), and then maintained under version control. You need to define expected results of tests and then automatically compare that with the actual results. You may even want to retain the results of previous test runs (perhaps due to regulatory compliance concerns).</td>
<td><ul>
<li><a href="http://www-01.ibm.com/software/data/optim/streamline-test-data-management/">IBM Optim Test Data Management</a> tools</li>
</ul></td>
</tr>
<tr class="even">
<td>Unit testing tools</td>
<td>Tools which enable you to regression test your database.</td>
<td><ul>
<li><a href="http://www.anydbtest.com/">AnyDbTest</a></li>
<li><a href="http://gojko.net/fitnesse/dbfit">DBFit</a></li>
<li><a href="http://www.dbunit.org/">DBUnit</a></li>
<li><a href="http://www.ndbunit.org/">NDbUnit</a></li>
<li><a href="http://sqlunit.sourceforge.net/">SQLUnit</a></li>
<li><a href="http://tsqlunit.sourceforge.net/">TSQLUnit</a> (for testing T-SQL in MS SQL Server)</li>
<li><a href="http://msdn.microsoft.com/vstudio/teamsystem/products/dbpro/">Visual Studio Team Edition for Database Professionals</a> includes testing capabilities</li>
<li><a href="http://weblogs.asp.net/rosherove/archive/2004/10/05/238201.aspx">XTUnit</a></li>
</ul></td>
</tr>
</tbody>
</table>

## Database Testing and Data Inspection

A common quality technique is to use data inspection tools to examine
existing data within a database. You might use something as simple as a
SQL-based query tool such as [DB Inspect](http://www.dbinspect.com/) to
select a subset of the data within a database to visually inspect the
results. For example, you may choose to view the unique values in a
column to determine what values are stored in it, or compare the row
count of a table with the count of the resulting rows from joining the
table with another one. If the two counts are the same then you don't
have an RI problem across the join.

The problem with data inspection is that it is often done manually and
on an irregular basis. When you make changes later, sometimes months or
years later, you need to redo your inspection efforts. This is costly,
time consuming, and error prone.

Data inspection is more of a debugging technique than it is a testing
technique. It is clearly an important technique, but it's not something
that will greatly contribute to your efforts to ensure data quality
within your organisation.

  

\*Orignal article refer
to <http://www.agiledata.org/essays/databaseTesting.html>
