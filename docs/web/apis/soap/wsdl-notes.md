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
