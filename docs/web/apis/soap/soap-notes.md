# SOAP Notes

<!-- SOAP is an acronym for Simple Object Access Protocol. -->

https://en.wikipedia.org/wiki/SOAP
https://blog.postman.com/soap-api-definition/
https://www.soapui.org/learn/api/soap-vs-rest-api/
https://www.postman.com/salesforce-developers/salesforce-developers/request/z5j7tgb/soap-login
https://www.techtarget.com/searchapparchitecture/definition/SOAP-Simple-Object-Access-Protocol

SOAP is a protocol for designing and developing web services. It allows programs running on different operating systems (like Windows, Linux, etc.) to communicate with each other over a network. SOAP APIs are known for their strict standards, security, and reliability.

Key Features of SOAP API
XML-Based: SOAP messages are formatted in XML, making them platform-independent and human-readable.

Protocol Independence: SOAP can work with various protocols like HTTP, SMTP, TCP, and more.

Extensibility: SOAP supports extensions for security, reliability, and other features.

Standardized: SOAP follows strict standards, making it highly reliable for enterprise-level applications.

Stateful Operations: SOAP can maintain stateful operations, unlike REST, which is stateless.

SOAP Message Structure
A SOAP message consists of the following parts:

Envelope: The root element that defines the start and end of the message.

Header (optional): Contains metadata like authentication or routing information.

Body: Contains the actual request or response data.

Fault (optional): Used to report errors during processing.

Example of a SOAP message:

```xml
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope">
  <soap:Header>
    <!-- Optional header information -->
  </soap:Header>
  <soap:Body>
    <m:GetUserDetails xmlns:m="https://example.com/user">
      <m:UserId>123</m:UserId>
    </m:GetUserDetails>
  </soap:Body>
</soap:Envelope>
```

Advantages of SOAP API
Security: Built-in support for WS-Security, making it ideal for sensitive data.

Reliability: Supports ACID (Atomicity, Consistency, Isolation, Durability) transactions.

Standardization: Strict standards ensure consistency across implementations.

Language and Platform Independence: Works across different programming languages and platforms.

Disadvantages of SOAP API
Complexity: More verbose and harder to implement compared to REST.

Performance: XML parsing can be slower than JSON (used in REST).

Less Flexibility: Strict standards can make it less flexible for simple use cases.

<!-- ## Characteristics -->

SOAP provides the Messaging Protocol layer of a web services protocol stack for web services.  
It is an XML-based protocol consisting of three parts:

- An envelope, which defines the message structure and how to process it
- A set of encoding rules for expressing instances of application-defined data-types
- A convention for representing procedure calls and responses

## What is SOAP?

SOAP is a messaging protocol specification,  
For exchanging structured information,  
In the implementation of web services in computer networks.

It uses XML Information Set for its message format,  
And relies on application layer protocols,  
Most often Hypertext Transfer Protocol (HTTP),  
Although some legacy systems communicate over Simple Mail Transfer Protocol (SMTP),  
For message negotiation and transmission.

Simple Object Access Protocol (SOAP) is a message specification for exchanging information between systems and applications.

When it comes to application programming interfaces (APIs), a SOAP API is developed in a more structured and formalized way.

Think of SOAP as being like the national postal service:

It provides a reliable and trusted way to send and receive messages between systems (and within enterprise applications).

It is older, established, and dependable—but it can be slower than competing architectural styles like REST.

## How Does it Work?

As an example of what SOAP procedures can do,  
An application can send a SOAP request to a server that has web services enabled,  
Such as a real-estate price database,  
With the parameters for a search.

The server then returns a SOAP response (an XML-formatted document),  
With the resulting data, e.g., prices, location, features.

Since the generated data comes in a standardized machine-parsable format,  
The requesting application can then integrate it directly.

## SOAP Characteristics

SOAP has 3 major characteristics:

1. Extensibility

   security and WS-Addressing are among the extensions under development.

1. Neutrality

   SOAP can operate over any protocol such as HTTP, SMTP, TCP, UDP.

1. Independence

   SOAP allows for any programming model.

## SOAP Architecture

The SOAP architecture consists of several layers of specifications for:

- Message format
- Message Exchange Patterns (MEP)
- Underlying transport protocol bindings
- Message processing models
- Protocol extensibility

<!-- SOAP evolved as a successor of XML-RPC,
Though it borrows its transport and interaction neutrality from Web Service Addressing,
And the envelope/header/body from elsewhere (probably from WDDX). -->

## SOAP History

SOAP was designed as an object-access protocol,  
And released as XML-RPC in June 1998 as part of Frontier 5.1.

It was created by Dave Winer, Don Box, Bob Atkinson, and Mohsen Al-Ghosein.  
And it was created for Microsoft, where Atkinson and Al-Ghosein were working.

The specification was not made available until it was submitted to IETF 13 September 1999.  
According to Don Box, this was due to politics within Microsoft.  
Because of Microsoft's hesitation, Dave Winer shipped XML-RPC in 1998.  
The submitted Internet Draft did not reach RFC status and is therefore not considered a "web standard" as such.

Version 1.1 of the specification was published as a W3C Note on 8 May 2000.  
Since version 1.1 did not reach W3C Recommendation status, it can not be considered a "web standard" either.

Version 1.2 of the specification however, became a W3C recommendation on June 24, 2003.  
SOAP originally stood for "Simple Object Access Protocol" but version 1.2 of the standard dropped this acronym.

The SOAP specification was maintained by the XML Protocol Working Group of the World Wide Web Consortium until the group was closed 10 July 2009.

After SOAP was first introduced,  
It became the underlying layer of a more complex set of web services,  
Based on WSDL, XSD and UDDI.

These different services (especially UDDI) have proved to be of far less interest,  
But an appreciation of them gives a complete understanding of the expected role of SOAP,  
Compared to how web services have actually evolved.

## SOAP Terminology

SOAP specification can be broadly defined to be consisting of the following 3 conceptual components:

### Protocol Concepts

- SOAP

  This is a set of rules formalizing and governing the format and processing rules,  
  For information exchanged between a SOAP sender and a SOAP receiver.

- SOAP Nodes

  These are physical/logical machines with processing units,  
  Which are used to transmit/forward, receive and process SOAP messages.  
  These are analogous to nodes in a network.

- SOAP Roles

  Over the path of a SOAP message, all nodes assume a specific role.  
  The role of the node defines the action that the node performs on the message it receives.  
  For example, a role "none" means that no node will process the SOAP header in any way and simply transmit the message along its path.

- SOAP Protocol Binding

  A SOAP message needs to work in conjunction with other protocols to be transferred over a network.  
  For example, a SOAP message could use TCP as a lower layer protocol to transfer messages.  
  These bindings are defined in the SOAP protocol binding framework.

- SOAP Features

  SOAP provides a messaging framework only.  
  However, it can be extended to add features such as reliability, security etc.  
  There are rules to be followed when adding features to the SOAP framework.

- SOAP Module

  A collection of specifications regarding the semantics of SOAP header to describe any new features being extended upon SOAP.  
  A module needs to realize zero or more features.  
  SOAP requires modules to adhere to prescribed rules.

### Data Encapsulation Concepts

- SOAP Message

  Represents the information being exchanged between 2 SOAP nodes.

- SOAP Envelope

  It is the enclosing element of an XML message identifying it as a SOAP message.

- SOAP header block

  A SOAP header can contain more than one of these blocks,  
  Each being a discrete computational block within the header.

  In general, the SOAP role information is used to target nodes on the path.

  A header block is said to be targeted at a SOAP node if the SOAP role for the header block is the name of a role in which the SOAP node operates.

  (ex: A SOAP header block with role attribute as ultimateReceiver is targeted only at the destination node which has this role.  
  A header with a role attribute as next is targeted at each intermediary as well as the destination node.)

- SOAP header

  A collection of one or more header blocks targeted at each SOAP receiver.

- SOAP body

  Contains the body of the message intended for the SOAP receiver.

  The interpretation and processing of SOAP body is defined by header blocks.

- SOAP fault

  In case a SOAP node fails to process a SOAP message, it adds the fault information to the SOAP fault element.

  This element is contained within the SOAP body as a child element.

### Message Sender And Receiver Concepts

- SOAP sender

  The node that transmits a SOAP message.

- SOAP receiver

  The node receiving a SOAP message.

  (Could be an intermediary or the destination node).

- SOAP message path

  The path consisting of all the nodes that the SOAP message traversed to reach the destination node.

- Initial SOAP sender

  This is the node which originated the SOAP message to be transmitted.

  This is the root of the SOAP message path.

- SOAP intermediary

  All the nodes in between the SOAP originator and the intended SOAP destination.

  It processes the SOAP header blocks targeted at it and acts to forward a SOAP message towards an ultimate SOAP receiver.

- Ultimate SOAP receiver

  The destination receiver of the SOAP message.

  This node is responsible for processing the message body and any header blocks targeted at it.

## Specification

The SOAP specification defines the messaging framework,  
Which consists of:

- **The SOAP processing model**

  Defining the rules for processing a SOAP message

- **The SOAP extensibility model**

  Defining the concepts of SOAP features and SOAP modules

- **The SOAP underlying protocol binding framework**

  Describing the rules for defining a binding to an underlying protocol that can be used for exchanging SOAP messages between SOAP nodes

- **The SOAP message construct**

  Defining the structure of a SOAP message

## SOAP Building Blocks

A SOAP message is an ordinary XML document containing the following elements:

| Element  | Description                                                                   | Required |
| -------- | ----------------------------------------------------------------------------- | -------- |
| Envelope | Identifies the XML document as a SOAP message.                                | Yes      |
| Header   | Contains header information.                                                  | No       |
| Body     | Contains call and response information.                                       | Yes      |
| Fault    | Provides information about errors that occurred while processing the message. | No       |

## Transport methods

Both SMTP and HTTP are valid application layer protocols used as transport for SOAP,  
But HTTP has gained wider acceptance as it works well with today's internet infrastructure;  
Specifically, HTTP works well with network firewalls.

## A background of SOAP APIs

SOAP was a standard that emerged in the late 1990s to give businesses the ability to move data around between corporate networks.

It was introduced just as the web was maturing, and while it does use HTTP primarily as a transport for the messages being passed around, its architectural patterns are not as closely aligned with HTTP as REST;

SOAP can also employ other protocols.

While REST is more of a style, SOAP gives you much more guidance on the structure of the request and response, as well as the message content and how it will be encoded.

Simply put, using SOAP when designing APIs focuses on the message, whereas using REST when designing APIs focuses on defining them as resources.

SOAP uses XML as the data format for messages being sent and received by an API client, and it provides four distinct dimensions to the API protocol:

Envelope: Defining the structure of the message.
Encoding: Rules for expressing the type of data.
Requests: How each SOAP API request is structured.
Responses: How each SOAP API response is structured.

Benefits of using SOAP APIs
Even though SOAP has very strict implementation guidelines, it is also known for its extensibility. Like other approaches to delivering APIs, SOAP uses HTTP for transport, but it can also leverage simple mail transport protocol (SMTP), transmission control protocol (TCP), and user data protocol (UDP) to pass messages back and forth. This allows for more flexibility when it comes to moving data, content, and media.

SOAP APIs also provide these other advantages when compared to REST APIs:

SOAP is language, transport, and even platform independent, whereas REST requires the use of HTTP.
SOAP is very secure, which makes it perfect for systems that handle sensitive data, such as financial services and online banking applications.
SOAP works well in distributed enterprise environments, instead of depending on direct point-to-point communication.
SOAP has built-in error handling features, which makes it easy to understand what happened when a request fails.

Conclusion
The SOAP protocol provides a much more solid foundation for APIs than the looser REST approach, but it can come with a cost. SOAP can make it slower to evolve and iterate APIs, and it can take longer to onboard new developers who aren’t familiar with SOAP’s older methods. Still, it’s a cost that is worthwhile for backbone applications and integrations that the enterprise depends upon. Remember that national postal service comparison? With its envelope, encoding, request, and response structure (as well as versatility with protocols like HTTP, TCP, UDP, and SMTP), SOAP remains a dependable way to define and operate APIs across the enterprise at scale.
