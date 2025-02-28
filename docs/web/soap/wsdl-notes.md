# WSDL Notes

https://en.wikipedia.org/wiki/Web_Services_Description_Language
https://www.w3schools.com/Xml/xml_wsdl.asp
https://www.w3.org/TR/wsdl.html
https://www.w3.org/TR/wsdl20/
https://www.w3.org/TR/wsdl/

## Web Services Description Language

The Web Services Description Language (WSDL),  
Is an XML-based interface description language,  
That is used for describing the functionality offered by a web service.

<!-- The acronym is also used for any specific WSDL description of a web service (also referred to as a WSDL file),
Which provides a machine-readable description of how the service can be called, what parameters it expects, and what data structures it returns.

Therefore, its purpose is roughly like a type signature in a programming language. -->

## Description

The WSDL describes services as collections of network endpoints, or ports.

The WSDL specification provides an XML format for documents for this purpose.

The abstract definitions of ports and messages are separated from their concrete use or instance, allowing the reuse of these definitions.

A port is defined by associating a network address with a reusable binding, and a collection of ports defines a service.

Messages are abstract descriptions of the data being exchanged,  
And port types are abstract collections of supported operations.

The concrete protocol and data format specifications for a particular port type constitutes a reusable binding,  
Where the operations and messages are then bound to a concrete network protocol and message format.

In this way, WSDL describes the public interface to the Web service.

WSDL is often used in combination with SOAP and an XML Schema to provide Web services over the Internet.

A client program connecting to a Web service can read the WSDL file to determine what operations are available on the server.

Any special data-types used are embedded in the WSDL file in the form of XML Schema.

The client can then use SOAP to actually call one of the operations listed in the WSDL file, using for example XML over HTTP.

## Building Blocks

- **Service**

  Contains a set of system functions that have been exposed to the Web-based protocols.

- **Port**

  Defines the address or connection point to a Web service.  
  It is typically represented by a simple HTTP URL string.

- **Binding**

  Specifies the interface and defines the SOAP binding style (RPC/Document) and transport (SOAP Protocol).  
  The binding section also defines the operations.

- **PortType**

  Defines a Web service, the operations that can be performed, and the messages that are used to perform the operation.

- **Operation**

  Defines the SOAP actions and the way the message is encoded, for example, "literal".  
  An operation is like a method or function call in a traditional programming language.

- **Message**

  Typically, a message corresponds to an operation.  
  The message contains the information needed to perform the operation.  
  Each message is made up of one or more logical parts.  
  Each part is associated with a message-typing attribute.  
  The message name attribute provides a unique name among all messages. The part name attribute provides a unique name among all the parts of the enclosing message. Parts are a description of the logical content of a message. In RPC binding, a binding may reference the name of a part in order to specify binding-specific information about the part. A part may represent a parameter in the message; the bindings define the actual meaning of the part. Messages were removed in WSDL 2.0, in which XML schema types for defining bodies of inputs, outputs and faults are referred to simply and directly.

- **Types**

  Describes the data. The XML Schema language (also known as XSD) is used (inline or referenced) for this purpose.

## Versions

The current version of the specification is 2.0;

Version 1.1 has not been endorsed by the W3C but version 2.0 is a W3C recommendation.

WSDL 1.2 was renamed WSDL 2.0 because of its substantial differences from WSDL 1.1.

By accepting binding to all the HTTP request methods (not only GET and POST as in version 1.1),

the WSDL 2.0 specification offers better support for RESTful web services, and is much simpler to implement.

| WSDL 1.1 Term | WSDL 2.0 Term |
| ------------- | ------------- |
| Service       | Service       |
| Port          | Endpoint      |
| Binding       | Binding       |
| PortType      | Interface     |
| Operation     | Operation     |
| Message       | —             |
| Types         | Types         |

:::note
The latest version of WSDL, which became a W3C recommendation in 2007, is WSDL 2.0.  
The meaning of the acronym has changed from version 1.1 where the "D" stood for "Definition".
:::
