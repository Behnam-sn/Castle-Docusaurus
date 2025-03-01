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
