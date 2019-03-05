# Simple XML Deserialiser

## Overview:

Simple is a high performance XML serialization and configuration
framework for Java. Its goal is to provide an XML framework that enables
rapid development of XML configuration and communication systems. This
framework aids the development of XML systems with minimal effort and
reduced errors. It offers full object serialization and deserialization,
maintaining each reference encountered. In essence it is similar to C\#
XML serialization for the Java platform, but offers additional features
for interception and manipulation

**Sample source code- Qantas Mobile App Mediation API:**

<https://stash.qcpaws.qantas.com.au/projects/AMS04-A868/repos/mobile-api/browse>

The attached source code is of a mediation layer that only consumes SOAP
API, deserialises using SimpleXML.

  

**How to use**

**Serialising a simple object**  
In order to serialise an object to XML a series of annotations must be
placed within that object. These annotations tell the persister how the
object should be serialized. For example take the class shown below.
Here there are three different annotations, one used to describe the
name of the root element, one that describes an XML message element, and
a final annotation for an id attribute.

@Root  
public class Example {

@Element  
private String text;

@Attribute  
private int index;

public Example() {  
super();  
}

public Example(String text, int index) {  
this.text = text;  
this.index = index;  
}

public String getMessage() {  
return text;  
}

public int getId() {  
return index;  
}  
}  
To serialize an instance of the above object a Persister is required.
The persister object is then given an instance of the annotated object
and an output result, which is a file in this example. Other output
formats are possible with the persister object.

Serializer serializer = new Persister();  
Example example = new Example("Example message", 123);  
File result = new File("example.xml");

serializer.write(example, result);  
Once the above code is executed the object instance will have been
transferred as an XML document to the specified file. The resulting XML
file will contain the contents shown below.

&lt;example index="123"&gt;  
&lt;text&gt;Example message&lt;/text&gt;  
&lt;/example&gt;  
As well as the capability of using the field an object name to acquire
the XML element and attribute names explicit naming is possible. Each
annotation contains a name attribute, which can be given a string
providing the name of the XML attribute or element. This ensures that
should the object have unusable field or method names they can be
overridden, also if your code is obfuscated explicit naming is the only
reliable way to serialize and deserialize objects consistently. An
example of the previous object with explicit naming is shown below.

@Root(name="root")  
public class Example {

@Element(name="message")  
private String text;

@Attribute(name="id")  
private int index;

public Example() {  
super();  
}

public Example(String text, int index) {  
this.text = text;  
this.index = index;  
}

public String getMessage() {  
return text;  
}

public int getId() {  
return index;  
}  
}  
For the above object the XML document constructed from an instance of
the object results in a different format. Here the XML element and
attribute names have been overridden with the annotation names. The
resulting output is shown below.

&lt;root id="123"&gt;  
&lt;message&gt;Example message&lt;/message&gt;  
&lt;/root&gt;

  
**Deserializing a simple object**  
Taking the above example object the XML deserialization process is
described in the code snippet shown below. As can be seen the
deserialization process is just as simple. The persister is given the
class representing the serialized object and the source of the XML
document. To deserialize the object the read method is used, which
produces an instance of the annotated object. Also, note that there is
no need to cast the return value from the read method as the method is
generic.

Serializer serializer = new Persister();  
File source = new File("example.xml");

Example example = serializer.read(Example.class, source);

  
