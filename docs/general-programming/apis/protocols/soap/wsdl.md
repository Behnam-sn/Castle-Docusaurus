# WSDL

## What is WSDL?

The Web Services Description Language (WSDL),  
Is an XML-based interface description language,  
That is used for describing the functionality offered by a web service.

WSDL provides a machine-readable description of how the service can be called,  
What parameters it expects,  
And what data structures it returns.

WSDL is often used in combination with SOAP and an XML Schema,  
To provide web services over the Internet.

## How Does WSDL Work?

A client program connecting to a web service can read the WSDL file,  
To determine what operations are available on the server.

Any special data-types used are embedded in the WSDL file in the form of XML Schema.

The client can then use SOAP to actually call one of the operations listed in the WSDL file,  
Using for example XML over HTTP.

## Versions

### WSDL 1.0

In the year 2000,  
WSDL 1.0 was developed by IBM, Microsoft, and Ariba;  
To describe web services for their SOAP toolkit.

It was built by combining two service description languages:

- NASSL (Network Application Service Specification Language) from IBM
- And SDL (Service Description Language) from Microsoft

### WSDL 1.1

WSDL 1.1, published in 2001, is the formalization of WSDL 1.0.  
No major changes were introduced between 1.0 and 1.1.

Version 1.1 has not been endorsed by the W3C,  
But version 2.0 is a W3C recommendation.

### WSDL 1.2

In 2003 WSDL 1.2 was a working draft at W3C,  
But has become WSDL 2.0.

According to W3C:  
WSDL 1.2 is easier and more flexible for developers than the previous version.  
WSDL 1.2 attempts to remove non-interoperable features,  
And also defines the HTTP 1.1 binding better,  
By accepting binding to all the HTTP request methods (not only GET and POST as in version 1.1).

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

However support for this specification is still poor in software development kits for web services,  
Which often offer tools only for WSDL 1.1.

## WSDL Structure

A WSDL Document follows a specific structure,  
Consisting of 6 main sections:

### Definitions

The `<definitions>` element is the **root of a WSDL document**.  
It contains the namespace and the service name.

```xml
<definitions name="MyService"
             targetNamespace="http://example.com/service"
             xmlns="http://schemas.xmlsoap.org/wsdl/"
             xmlns:tns="http://example.com/service"
             xmlns:xsd="http://www.w3.org/2001/XMLSchema"
             xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/">
```

Key Attributes:

- `targetNamespace`

  Unique identifier for the service

- `xmlns` attributes

  Define XML namespaces

### Types

This section **defines the data types** used in the messages.  
It typically contains an **XML Schema (XSD)**.

```xml
<types>
  <xsd:schema targetNamespace="http://example.com/service">
    <xsd:element name="GetUser">
      <xsd:complexType>
        <xsd:element name="id" type="xsd:int"/>
      </xsd:complexType>
    </xsd:element>

    <xsd:complexType name="User">
      <xsd:sequence>
        <xsd:element name="Name" type="xsd:string"/>
        <xsd:element name="Age" type="xsd:int"/>
      </xsd:sequence>
    </xsd:complexType>
  </xsd:schema>
</types>
```

### Message

A `message` is a set of parameters exchanged in a web service call.

Each `message` has one or more `part` elements.  
A `part` can refers to an `element` or a `complexType` in `<types>`.

```xml
<message name="GetUserRequest">
  <part name="Body" element="tns:GetUser"/>
</message>

<message name="GetUserResponse">
  <part name="Body" type="tns:User"/>
</message>
```

### PortType

This section defines what **operations** the service provides.

A `<portType>` contains multiple `<operation>` elements.  
Each `<operation>` has:

- `<input>`

  Defines request message

- `<output>`

  Defines response message

```xml
<portType name="UserServicePort">
  <operation name="GetUser">
    <input message="tns:GetUserRequest"/>
    <output message="tns:GetUserResponse"/>
  </operation>
</portType>
```

The abstract definitions of `portTypes` and `messages` are separated from their concrete use or instance,  
Allowing the reuse of these definitions.

### Binding

The `<binding>` section specifies:

- Which `portType` it binds to.
- Which communication protocol (e.g., SOAP, HTTP).
- How messages are encoded.

```xml
<binding name="UserServiceBinding" type="tns:UserServicePort">
  <soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http"/>

  <operation name="GetUser">
    <soap:operation soapAction="http://example.com/GetUser"/>

    <input>
      <soap:body use="literal"/>
    </input>

    <output>
      <soap:body use="literal"/>
    </output>
  </operation>
</binding>
```

### Service

This section specifies where the service is hosted.

The `<service>` element contains one or more `<port>` elements.  
Each `<port>` has a binding and an endpoint URL.

```xml
<service name="UserService">
  <port name="UserServicePort" binding="tns:UserServiceBinding">
    <soap:address location="http://example.com/service"/>
  </port>
</service>
```

A `port` is defined by associating a network address with a reusable `binding`.  
For example:  
The `UserService` is available at `http://example.com/service`.

### Terms Difference

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

The main structure of a WSDL document looks like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<definitions name="UserService"
             targetNamespace="http://example.com/service"
             xmlns="http://schemas.xmlsoap.org/wsdl/"
             xmlns:tns="http://example.com/service"
             xmlns:xsd="http://www.w3.org/2001/XMLSchema"
             xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/">

  <types>
    <xsd:schema targetNamespace="http://example.com/service">
      <xsd:element name="GetUser">
        <xsd:complexType>
          <xsd:element name="id" type="xsd:int"/>
        </xsd:complexType>
      </xsd:element>

      <xsd:complexType name="User">
        <xsd:sequence>
          <xsd:element name="Name" type="xsd:string"/>
          <xsd:element name="Age" type="xsd:int"/>
        </xsd:sequence>
      </xsd:complexType>
    </xsd:schema>
  </types>

  <message name="GetUserRequest">
    <part name="Body" element="tns:GetUser"/>
  </message>

  <message name="GetUserResponse">
    <part name="Body" type="tns:User"/>
  </message>

  <portType name="UserServicePort">
    <operation name="GetUser">
      <input message="tns:GetUserRequest"/>
      <output message="tns:GetUserResponse"/>
    </operation>
  </portType>

  <binding name="UserServiceBinding" type="tns:UserServicePort">
    <soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http"/>

    <operation name="GetUser">
      <soap:operation soapAction="http://example.com/GetUser"/>
      <input>
        <soap:body use="literal"/>
      </input>
      <output>
        <soap:body use="literal"/>
      </output>
    </operation>
  </binding>

  <service name="UserService">
    <port name="UserServicePort" binding="tns:UserServiceBinding">
      <soap:address location="http://example.com/service"/>
    </port>
  </service>

</definitions>
```

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
- [w3schools.com/Xml/xml_wsdl.asp](https://www.w3schools.com/Xml/xml_wsdl.asp)

## Read More

- [w3.org/TR/wsdl.html](https://www.w3.org/TR/wsdl.html)
- [w3.org/TR/wsdl20/](https://www.w3.org/TR/wsdl20/)
- [w3.org/TR/wsdl/](https://www.w3.org/TR/wsdl/)
