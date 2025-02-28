# WSDL

## What is WSDL?

The Web Services Description Language (WSDL),  
Is an XML-based interface description language,  
That is used for describing the functionality offered by a web service.

## How Does WSDL Work?

WSDL is often used in combination with SOAP and an XML Schema to provide Web services over the Internet.

A client program connecting to a Web service can read the WSDL file,  
To determine what operations are available on the server.

Any special data-types used are embedded in the WSDL file in the form of XML Schema.

The client can then use SOAP to actually call one of the operations listed in the WSDL file,  
Using for example XML over HTTP.

## Versions

### WSDL 1.0

In the year 2000,  
WSDL 1.0 was developed by IBM, Microsoft, and Ariba;  
To describe Web Services for their SOAP toolkit.

It was built by combining two service description languages:  
NASSL (Network Application Service Specification Language) from IBM,  
And SDL (Service Description Language) from Microsoft.

### WSDL 1.1

WSDL 1.1, published in 2001, is the formalization of WSDL 1.0.  
No major changes were introduced between 1.0 and 1.1.

Version 1.1 has not been endorsed by the W3C but version 2.0 is a W3C recommendation.

### WSDL 1.2

In 2003 WSDL 1.2 was a working draft at W3C, but has become WSDL 2.0.

According to W3C:  
WSDL 1.2 is easier and more flexible for developers than the previous version.  
WSDL 1.2 attempts to remove non-interoperable features,  
And also defines the HTTP 1.1 binding better,  
By accepting binding to all the HTTP request methods (not only GET and POST as in version 1.1),

The WSDL 1.2 specification offers better support for RESTful web services,  
And is much simpler to implement.

WSDL 1.2 was not supported by most SOAP servers/vendors.

### WSDL 2.0

WSDL 2.0 became a W3C recommendation in June 2007.  
WSDL 1.2 was renamed to WSDL 2.0 because it has substantial differences from WSDL 1.1.  
Also The meaning of the acronym has changed from version 1.1 where the "D" stood for "Definition".

The changes are the following:

- Added further semantics to the description language
- Removed message constructs
- Operator overloading not supported
- PortTypes renamed to interfaces
- Ports renamed to endpoints

## Building Blocks

- ### Service

  Contains a set of system functions that have been exposed to the Web-based protocols.

- ### Port

  Defines the address or connection point to a Web service.  
  It is typically represented by a simple HTTP URL string.

- ### Binding

  Specifies the interface and defines the SOAP binding style (RPC/Document) and transport (SOAP Protocol).  
  The binding section also defines the operations.

- ### PortType

  Defines a Web service,  
  The operations that can be performed,  
  And the messages that are used to perform the operation.

- ### Operation

  Defines the SOAP actions and the way the message is encoded,  
  For example: "literal"

  An operation is like a method or function call in a traditional programming language.

- ### Message

  Typically, a message corresponds to an operation.  
  The message contains the information needed to perform the operation.

  Each message is made up of one or more logical parts.  
  Each part is associated with a message-typing attribute.

  The message name attribute provides a unique name among all messages.  
  The part name attribute provides a unique name among all the parts of the enclosing message.

  Parts are a description of the logical content of a message.  
  In RPC binding, a binding may reference the name of a part in order to specify binding-specific information about the part.  
  A part may represent a parameter in the message;  
  The bindings define the actual meaning of the part.

  Messages were removed in WSDL 2.0,  
  In which XML schema types for defining bodies of inputs,  
  Outputs and faults are referred to simply and directly.

- ### Types

  Describes the data.  
  The XML Schema language (also known as XSD) is used (inline or referenced) for this purpose.

### Terms

| WSDL 1.1 Term | WSDL 2.0 Term |
| ------------- | ------------- |
| Service       | Service       |
| Port          | Endpoint      |
| Binding       | Binding       |
| PortType      | Interface     |
| Operation     | Operation     |
| Message       | —             |
| Types         | Types         |

## Examples

A WSDL 2.0 example:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<description xmlns="http://www.w3.org/ns/wsdl"
             xmlns:tns="http://www.tmsws.com/wsdl20sample"
             xmlns:whttp="http://schemas.xmlsoap.org/wsdl/http/"
             xmlns:wsoap="http://schemas.xmlsoap.org/wsdl/soap/"
             targetNamespace="http://www.tmsws.com/wsdl20sample">

  <documentation>
      This is a sample WSDL 2.0 document.
  </documentation>

<!-- Abstract type -->
   <types>
      <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
                xmlns="http://www.tmsws.com/wsdl20sample"
                targetNamespace="http://www.example.com/wsdl20sample">

         <xs:element name="request"> ... </xs:element>
         <xs:element name="response"> ... </xs:element>
      </xs:schema>
   </types>

<!-- Abstract interfaces -->
   <interface name="Interface1">
      <fault name="Error1" element="tns:response"/>
      <operation name="Get" pattern="http://www.w3.org/ns/wsdl/in-out">
         <input messageLabel="In" element="tns:request"/>
         <output messageLabel="Out" element="tns:response"/>
      </operation>
   </interface>

<!-- Concrete Binding Over HTTP -->
   <binding name="HttpBinding" interface="tns:Interface1"
            type="http://www.w3.org/ns/wsdl/http">
      <operation ref="tns:Get" whttp:method="GET"/>
   </binding>

<!-- Concrete Binding with SOAP-->
   <binding name="SoapBinding" interface="tns:Interface1"
            type="http://www.w3.org/ns/wsdl/soap"
            wsoap:protocol="http://www.w3.org/2003/05/soap/bindings/HTTP/"
            wsoap:mepDefault="http://www.w3.org/2003/05/soap/mep/request-response">
      <operation ref="tns:Get" />
   </binding>

<!-- Web Service offering endpoints for both bindings-->
   <service name="Service1" interface="tns:Interface1">
      <endpoint name="HttpEndpoint"
                binding="tns:HttpBinding"
                address="http://www.example.com/rest/"/>
      <endpoint name="SoapEndpoint"
                binding="tns:SoapBinding"
                address="http://www.example.com/soap/"/>
   </service>
</description>
```

## References

- [en.wikipedia.org/wiki/Web_Services_Description_Language](https://en.wikipedia.org/wiki/Web_Services_Description_Language)
