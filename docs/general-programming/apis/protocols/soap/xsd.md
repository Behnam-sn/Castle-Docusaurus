# XSD

## What is XSD?

XSD (XML Schema Definition),  
Is used to describe and validate,  
The structure and content of,  
An XML document.

XSD is a recommendation of the W3C.

## History

### Versions

## Elements

## Example

```xml
<?xml version="1.0"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

  <xs:element name="note">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="to" type="xs:string"/>
        <xs:element name="from" type="xs:string"/>
        <xs:element name="heading" type="xs:string"/>
        <xs:element name="body" type="xs:string"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>

</xs:schema>
```

## Why Use XSD?

## Why Not Use XSD?

## References

- [en.wikipedia.org/wiki/XML-Schema-(W3C)](<https://en.wikipedia.org/wiki/XML_Schema_(W3C)>)
- [w3schools.com/xml/schema_intro.asp](https://www.w3schools.com/xml/schema_intro.asp)
