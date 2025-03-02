# WSDL Notes

https://www.w3schools.com/Xml/xml_wsdl.asp

https://www.w3.org/TR/wsdl.html

https://www.w3.org/TR/wsdl20/

https://www.w3.org/TR/wsdl/

## Web Services Description Language

<!-- The acronym is also used for any specific WSDL description of a web service (also referred to as a WSDL file),
Which provides a machine-readable description of how the service can be called, what parameters it expects, and what data structures it returns.

Therefore, its purpose is roughly like a type signature in a programming language. -->

The abstract definitions of ports and messages are separated from their concrete use or instance,  
Allowing the reuse of these definitions.

Messages are abstract descriptions of the data being exchanged,  
And port types are abstract collections of supported operations.

The WSDL describes services as collections of network endpoints, or ports.

A port is defined by associating a network address with a reusable binding.

The concrete protocol and data format specifications for a particular port type constitutes a reusable binding,  
Where the operations and messages are then bound to a concrete network protocol and message format.

In this way, WSDL describes the public interface to the Web service.

## WSDL Structure

A WSDL Document follows a specific structure,  
Consisting of six main sections:

- **Types**

  Defines Data Types

- **Message**

  Defines Messages

- **PortType**

  Defines Operations

- **Binding**

  Defines Protocol & Format

- **Service**

  Defines Service Location

- **Definitions**

  Root Element

The main structure of a WSDL document looks like this:

```xml
<definitions>

   <types>
      data type definitions........
   </types>

   <message>
      definition of the data being communicated....
   </message>

   <portType>
      set of operations......
   </portType>

   <binding>
      protocol and data format specification....
   </binding>

</definitions>
```

This is a simplified fraction of a WSDL document:

```xml
<message name="getTermRequest">
  <part name="term" type="xs:string"/>
</message>

<message name="getTermResponse">
  <part name="value" type="xs:string"/>
</message>

<portType name="glossaryTerms">
  <operation name="getTerm">
    <input message="getTermRequest"/>
    <output message="getTermResponse"/>
  </operation>
</portType>
```

In this example the `<portType>` element defines "glossaryTerms" as the name of a port, and "getTerm" as the name of an operation.

The "getTerm" operation has an input message called "getTermRequest" and an output message called "getTermResponse".

The `<message>` elements define the parts of each message and the associated data types.

The `<portType>` Element
The `<portType>` element defines a web service, the operations that can be performed, and the messages that are involved.

The request-response type is the most common operation type, but WSDL defines four types:

Type Definition
One-way The operation can receive a message but will not return a response
Request-response The operation can receive a request and will return a response
Solicit-response The operation can send a request and will wait for a response
Notification The operation can send a message but will not wait for a response

WSDL One-Way Operation
A one-way operation example:

## Structure of a WSDL File

### Definitions (Root Element)

The `<definitions>` element is the root of a WSDL document.  
It contains the namespace and the service name.

```xml
<definitions name="MyService"
             targetNamespace="http://example.com/service"
             xmlns="http://schemas.xmlsoap.org/wsdl/"
             xmlns:tns="http://example.com/service"
             xmlns:xsd="http://www.w3.org/2001/XMLSchema"
             xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/">
```

📌 Key Attributes:

targetNamespace → Unique identifier for the service

xmlns attributes → Define XML namespaces

### Types (Defines Data Types)

This section defines the data types used in the messages.  
It typically contains an **XML Schema (XSD)**.

```xml
<types>
  <xsd:schema targetNamespace="http://example.com/service">
    <xsd:complexType name="User">
      <xsd:sequence>
        <xsd:element name="Name" type="xsd:string"/>
        <xsd:element name="Age" type="xsd:int"/>
      </xsd:sequence>
    </xsd:complexType>
  </xsd:schema>
</types>
```

📌 What’s Inside?

- Defines complex types (User)
- Defines primitive types (string, int, etc.)
- Used to structure messages and operations

### Message

A message is a set of parameters exchanged in a web service call.

```xml
<message name="GetUserRequest">
  <part name="Body" element="tns:GetUser"/>
</message>

<message name="GetUserResponse">
  <part name="Body" element="tns:User"/>
</message>
```

📌 What’s Inside?

- Each message has one or more `part` elements
- A part refers to an element in `<types>`

💡 Example:

- GetUserRequest contains GetUser (which is mapped to User)
- GetUserResponse returns User data

### PortType

This section defines what operations the service provides.

```xml
<portType name="UserServicePort">
  <operation name="GetUser">
    <input message="tns:GetUserRequest"/>
    <output message="tns:GetUserResponse"/>
  </operation>
</portType>
```

📌 What’s Inside?

- A `<portType>` contains multiple `<operation>` elements
- Each `<operation>` has:
  - `<input>` → Defines request message
  - `<output>` → Defines response message

💡 Example:

The operation `GetUser` takes a `GetUserRequest` and returns `GetUserResponse`.
