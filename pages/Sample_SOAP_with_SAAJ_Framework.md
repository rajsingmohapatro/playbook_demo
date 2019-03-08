# Sample SOAP with SAAJ Framework

**Overview:**

**SOAP with Attachments API for Java (SAAJ)** is mainly used for dealing
directly with SOAP Request/Response messages which happens behind the
scenes in any Web Service API. It allows the developers to directly send
and receive soap messages instead of using JAX-WS.

SAAJ messages follow SOAP standards, which prescribe the format for
messages and also specify some things that are required, optional, or
not allowed. With the SAAJ API, you can create XML messages that conform
to the SOAP 1.1 or 1.2 specification and to the WS-I Basic Profile 1.1
specification simply by making Java API calls.

  

**Sample Project with SAAJ- PNR Generation **

<https://stash.qcpaws.qantas.com.au/projects/AMS04-A868/repos/automationtestdata/browse>

In this project, SAAJ is used to send and receive message to QSOA. Its a
data driven framework wherein each iterations are carried over against
rows of Excel Test Data.

  

**How to use:**

**Creating a Message**

The first step is to create a message using a MessageFactory object. The
SAAJ API provides a default implementation of the MessageFactory class,
thus making it easy to get an instance. The following code fragment
illustrates getting an instance of the default message factory and then
using it to create a message.

  
MessageFactory factory = MessageFactory.newInstance();  
SOAPMessage message = factory.createMessage();

**Accessing Elements of a Message**

  

The next step in creating a message is to access its parts so that
content can be added. There are two ways to do this.
The SOAPMessage object message, created in the preceding code fragment,
is the place to start.

The first way to access the parts of the message is to work your way
through the structure of the message. The message contains
a SOAPPart object, so you use the getSOAPPart method of message to
retrieve it:

    SOAPPart soapPart = message.getSOAPPart();

Next you can use the getEnvelope method of soapPart to retrieve
the SOAPEnvelope object that it contains.

    SOAPEnvelope envelope = soapPart.getEnvelope();

You can now use the getHeader and getBody methods of envelope to
retrieve its empty SOAPHeader and SOAPBody objects.

    SOAPHeader header = envelope.getHeader();
    SOAPBody body = envelope.getBody();

The second way to access the parts of the message is to retrieve the
message header and body directly, without retrieving
the SOAPPart or SOAPEnvelope. To do so, use
the getSOAPHeader and getSOAPBody methods of SOAPMessage:

    SOAPHeader header = message.getSOAPHeader();
    SOAPBody body = message.getSOAPBody();

  

**Adding Content to the Body**

The SOAPBody object contains either content or a fault. To add content
to the body, you normally create one or more SOAPBodyElement objects to
hold the content. You can also add subelements to
the SOAPBodyElementobjects by using the addChildElement method. For each
element or child element, you add content by using
the addTextNode method.

When you create any new element, you also need to create an
associated javax.xml.namespace.QName object so that it is uniquely
identified.

The SOAPFactory class also lets you create XML elements when you are not
creating an entire message or do not have access to a
complete SOAPMessage object. For example, JAX-RPC implementations often
work with XML fragments rather than complete SOAPMessage objects.
Consequently, they do not have access to a SOAPEnvelope object, and this
makes using a SOAPFactory object to create Name objects very useful. In
addition to a method for creating Name objects, the SOAPFactory class
provides methods for creating Detail objects and SOAP fragments. You
will find an explanation of Detail objects in [Overview of SOAP
Faults](https://docs.oracle.com/javaee/5/tutorial/doc/bnbhr.html#bnbio) and [Creating
and Populating
a SOAPFault Object](https://docs.oracle.com/javaee/5/tutorial/doc/bnbhr.html#bnbip).

The following code fragment retrieves
the SOAPBody object body from message, constructs a QName object for the
element to be added, and adds a new SOAPBodyElement object to body.

    SOAPBody body = message.getSOAPBody();
    QName bodyName = new QName("http://wombat.ztrade.com", "GetLastTradePrice", "m");
    SOAPBodyElement bodyElement = body.addBodyElement(bodyName);

At this point, body contains a SOAPBodyElement object identified by
the QName object bodyName, but there is still no content in bodyElement.
Assuming that you want to get a quote for the stock of Sun Microsystems,
Inc., you need to create a child element for the symbol using
the addChildElement method. Then you need to give it the stock symbol
using the addTextNode method. The QName object for the
new SOAPElement object symbol is initialized with only a local name
because child elements inherit the prefix and URI from the parent
element.

    QName name = new QName("symbol");
    SOAPElement symbol = bodyElement.addChildElement(name);
    symbol.addTextNode("SUNW");

You might recall that the headers and content in a SOAPPart object must
be in XML format. The SAAJ API takes care of this for you, building the
appropriate XML constructs automatically when you call methods such
asaddBodyElement, addChildElement, and addTextNode. Note that you can
call the method addTextNode only on an element such as bodyElement or
any child elements that are added to it. You cannot call addTextNodeon
a SOAPHeader or SOAPBody object because they contain elements and not
text.

The content that you have just added to your SOAPBody object will look
like the following when it is sent over the wire:

    <SOAP-ENV:Envelope
     xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
      <SOAP-ENV:Body>
        <m:GetLastTradePrice xmlns:m="http://wombat.ztrade.com">
          <symbol>SUNW</symbol>
        </m:GetLastTradePrice>
      </SOAP-ENV:Body>
    </SOAP-ENV:Envelope>

  

  
