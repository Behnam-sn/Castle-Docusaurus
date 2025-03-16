# XSD Notes

https://en.wikipedia.org/wiki/XML_Schema_(W3C)
https://www.w3schools.com/xml/schema_intro.asp
https://www.techtarget.com/whatis/definition/XSD-XML-Schema-Definition
https://www.ibm.com/docs/en/iis/11.5?topic=types-xml-schema-definition-xsd-assets
https://learn.microsoft.com/en-us/previous-versions/windows/desktop/ms765537(v=vs.85)
https://learn.microsoft.com/en-us/dotnet/standard/serialization/xml-schema-definition-tool-xsd-exe

## What

XSD (XML Schema Definition), specifies how to formally describe the elements in an Extensible Markup Language (XML) document.

It can be used by programmers to verify each piece of item content in a document,  
To assure it adheres to the description of the element it is placed in.

XSD is a recommendation of the World Wide Web Consortium (W3C).

Like all XML schema languages,  
XSD can be used to express a set of rules to which an XML document must conform to be considered "valid" according to that schema.

However, unlike most other schema languages,  
XSD was also designed with the intent that determination of a document's validity would produce a collection of information adhering to specific data types.

Such a post-validation `infoset` can be useful in the development of XML document processing software.

An XML Schema describes the structure of an XML document.

The XML Schema language is also referred to as XML Schema Definition (XSD).

The purpose of an XML Schema is to define the legal building blocks of an XML document:

- The elements and attributes that can appear in a document
- The number of (and order of) child elements
- Data types for elements and attributes
- Default and fixed values for elements and attributes

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

## Why

## History

XML Schema published as a W3C recommendation in May 2001,  
Is one of several XML schema languages.

It was the first separate schema language for XML to achieve Recommendation status by the W3C.

Because of confusion between XML Schema as a specific W3C specification,  
And the use of the same term to describe schema languages in general,  
Some parts of the user community referred to this language as WXS, an initialism for W3C XML Schema,  
While others referred to it as XSD, an initialism for XML Schema Definition.

In Version 1.1 the W3C has chosen to adopt XSD as the preferred name.

In its appendix of references,  
The XSD specification acknowledges the influence of DTDs and other early XML schema efforts such as DDML, SOX, XML-Data, and XDR.

It has adopted features from each of these proposals but is also a compromise among them.

Of those languages, XDR and SOX continued to be used and supported for a while after XML Schema was published.

A number of Microsoft products supported XDR until the release of MSXML 6.0 (which dropped XDR in favor of XML Schema) in December 2006.

Commerce One, Inc. supported its SOX schema language until declaring bankruptcy in late 2004.

The most obvious features offered in XSD that are not available in XML's native Document Type Definitions (DTDs) are namespace awareness and data-types, that is, the ability to define element and attribute content as containing values such as integers and dates rather than arbitrary text.

The XSD 1.0 specification was originally published in 2001,  
With a second edition following in 2004 to correct large numbers of errors.  
XSD 1.1 became a W3C Recommendation in April 2012.

### Version 1.1

XSD 1.1 became a W3C Recommendation in April 2012,  
Which means it is an approved W3C specification.

Significant new features in XSD 1.1 are:

- The ability to define assertions against the document content by means of XPath 2.0 expressions.  
  (an idea borrowed from Schematron).

- The ability to select the type against which an element will be validated based on the values of the element's attributes ("conditional type assignment").

- Relaxing the rules whereby explicit elements in a content model must not match wildcards also allowed by the model.

- The ability to specify wildcards for both elements and attributes,  
  That apply to all types in the schema,  
  So that they all implement the same extensibility policy.

Until the Proposed Recommendation draft,  
XSD 1.1 also proposed the addition of a new numeric data type, precisionDecimal.  
This proved controversial,  
And was therefore dropped from the specification at a late stage of development.

## Schemas and schema documents (files)

Technically, a schema is an abstract collection of metadata,  
Consisting of a set of schema components:

chiefly element and attribute declarations and complex and simple type definitions.

These components are usually created by processing a collection of schema documents,  
Which contain the source language definitions of these components.

In popular usage, however, a schema document is often referred to as a schema.

Schema documents are organized by namespace:  
All the named schema components belong to a target namespace,  
And the target namespace is a property of the schema document as a whole.

A schema document may include other schema documents for the same namespace,  
And may import schema documents for a different namespace.

When an instance document is validated against a schema (a process known as assessment),  
The schema to be used for validation can either be supplied as a parameter to the validation engine,  
Or it can be referenced directly from the instance document using two special attributes,  
xsi:schemaLocation and xsi:noNamespaceSchemaLocation.

(The latter mechanism requires the client invoking validation to trust the document sufficiently to know that it is being validated against the correct schema.  
"xsi" is the conventional prefix for the namespace "http://www.w3.org/2001/XMLSchema-instance".)

XML Schema Documents usually have the filename extension ".xsd".

A unique Internet Media Type is not yet registered for XSDs,  
So "application/xml" or "text/xml" should be used, as per RFC 3023.

## Schema components

The main components of a schema are:

### Element declarations,

Which define properties of elements.

These include the element name and target namespace.

An important property is the type of the element,  
Which constrains what attributes and children the element can have.

In XSD 1.1, the type of the element may be conditional on the values of its attributes.

An element may belong to a substitution group;  
If element `E` is in the substitution group of element `H`,  
Then wherever the schema permits `H` to appear,  
`E` may appear in its place.

Elements may have integrity constraints:  
Uniqueness constraints determining that particular values must be unique within the subtree rooted at an element,  
And referential constraints determining that values must match the identifier of some other element.

Element declarations may be global or local,  
Allowing the same name to be used for unrelated elements in different parts of an instance document.

### Attribute declarations,

which define properties of attributes.

Again the properties include the attribute name and target namespace.

The attribute type constrains the values that the attribute may take.

An attribute declaration may also include a default value or a fixed value (which is then the only value the attribute may take.)

### Simple and complex types.

These are described in the following section.

### Model group and attribute group definitions.

These are essentially macros:  
Named groups of elements and attributes that can be reused in many different type definitions.

### attribute use

An attribute use represents the relationship of a complex type and an attribute declaration,  
And indicates whether the attribute is mandatory or optional when it is used in that type.

### element particle

An element particle similarly represents the relationship of a complex type and an element declaration,  
And indicates the minimum and maximum number of times the element may appear in the content.

As well as element particles,  
Content models can include model group particles,  
Which act like non-terminals in a grammar:  
They define the choice and repetition units within the sequence of permitted elements.

In addition,  
Wildcard particles are allowed,  
Which permit a set of different elements (perhaps any element provided it is in a certain namespace).

### Others

Other more specialized components include annotations, assertions, notations, and the schema component which contains information about the schema as a whole.

## Types

Simple types (also called data types) constrain the textual values that may appear in an element or attribute.

This is one of the more significant ways in which XML Schema differs from DTDs.

For example, an attribute might be constrained to hold only a valid date or a decimal number.

XSD provides a set of 19 primitive data types  
(anyURI, base64Binary, boolean, date, dateTime, decimal, double, duration, float, hexBinary, gDay, gMonth, gMonthDay, gYear, gYearMonth, NOTATION, QName, string, and time).

It allows new data types to be constructed from these primitives by three mechanisms:

- restriction (reducing the set of permitted values),
- list (allowing a sequence of values), and
- union (allowing a choice of values from several types).

Twenty-five derived types are defined within the specification itself,  
And further derived types can be defined by users in their own schemas.

The mechanisms available for restricting data types include the ability to specify minimum and maximum values, regular expressions, constraints on the length of strings, and constraints on the number of digits in decimal values. XSD 1.1 again adds assertions, the ability to specify an arbitrary constraint by means of an XPath 2.0 expression.

Complex types describe the permitted content of an element,  
Including its element and text children and its attributes.

A complex type definition consists of a set of attribute uses and a content model.

Varieties of content model include:

- element-only content, in which no text may appear (other than whitespace, or text enclosed by a child element)
- simple content, in which text is allowed but child elements are not
- empty content, in which neither text nor child elements are allowed
- mixed content, which permits both elements and text to appear

A complex type can be derived from another complex type by restriction (disallowing some elements, attributes, or values that the base type permits) or by extension (allowing additional attributes and elements to appear).

In XSD 1.1, a complex type may be constrained by assertions—XPath 2.0 expressions evaluated against the content that must evaluate to true.

## Features

### Post-Schema-Validation Infoset

After XML Schema-based validation,  
It is possible to express an XML document's structure and content in terms of the data model that was implicit during validation.

The XML Schema data model includes:

- The vocabulary (element and attribute names)
- The content model (relationships and structure)
- The data types

This collection of information is called the Post-Schema-Validation Infoset (PSVI).

The PSVI gives a valid XML document its "type" and facilitates treating the document as an object, using object-oriented programming (OOP) paradigms.

### Secondary uses for XML Schemas

The primary reason for defining an XML schema is to formally describe an XML document;  
However the resulting schema has a number of other uses that go beyond simple validation.

#### Code generation

The schema can be used to generate code,  
Referred to as XML Data Binding.

This code allows contents of XML documents to be treated as objects within the programming environment.

#### Generation of XML file structure documentation

The schema can be used to generate human-readable documentation of an XML file structure;  
This is especially useful where the authors have made use of the annotation elements.

No formal standard exists for documentation generation,  
But a number of tools are available,  
Such as the Xs3p stylesheet,  
That will produce high-quality readable HTML and printed material.

## Criticism

Although XML Schema is successful in that it has been widely adopted and largely achieves what it set out to,  
It has been the subject of a great deal of severe criticism,  
Perhaps more so than any other W3C Recommendation.

Good summaries of the criticisms are provided by James Clark, Anders Møller and Michael Schwartzbach, Rick Jelliffe and David Webber.

### General problems

- It is too complicated (the spec is several hundred pages in a very technical language),  
  So it is hard to use by non-experts—but many non-experts need schemas to describe data formats.

  The W3C Recommendation itself is extremely difficult to read.  
  Most users find W3Cs XML Schema Primer much easier to understand.

- XSD lacks any formal mathematical specification.  
  This makes it difficult to reason about schemas,  
  For example to prove that a modification to a schema is backwards compatible.

- There are many surprises in the language,  
  For example that restriction of elements works differently from restriction of attributes.

### Practical limitations of expressibility

- XSD offers very weak support for unordered content.

- XSD cannot require a specific root element (so extra information is required to validate even the simplest documents).

- When describing mixed content,  
  The character data cannot be constrained in any way (not even a set of valid characters can be specified).

- Content and attribute declarations cannot depend on attributes or element context (this was also listed as a central problem of DTD).

- It is not 100% self-describing (as a trivial example, see the previous point),  
  Even though that was an initial design requirement.

- Defaults cannot be specified separately from the declarations.  
  This makes it hard to make families of schemas that only differ in the default values .  
  Element defaults can only be character data (not containing markup).

### Technical problems

- Although it technically is namespace-conformant,  
  It does not seem to follow the namespace spirit (e.g. "unqualified locals").

- XSD 1.0 provided no facilities to state that the value or presence of one attribute is dependent on the values or presence of other attributes (so-called co-occurrence constraints).  
  This has been fixed in XSD 1.1.

- The set of XSD datatypes on offer is highly arbitrary.[10]

- The two tasks of validation and augmentation (adding type information and default values) should be kept separate.

## Elements

### Schema

The `<schema>` element is the root element of every XML Schema:

<?xml version="1.0"?>

```xml
<xs:schema>
...
...
</xs:schema>
```

The `<schema>` element may contain some attributes. A schema declaration often looks something like this:

```xml
<?xml version="1.0"?>

<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
targetNamespace="https://www.w3schools.com"
xmlns="https://www.w3schools.com"
elementFormDefault="qualified">
...
...
</xs:schema>
```

The following fragment:

```xml
xmlns:xs="http://www.w3.org/2001/XMLSchema"
```

indicates that the elements and data types used in the schema come from the `http://www.w3.org/2001/XMLSchema` namespace.

It also specifies that the elements and data types that come from the `http://www.w3.org/2001/XMLSchema` namespace should be prefixed with xs:

```xml
targetNamespace="https://www.w3schools.com"
```

indicates that the elements defined by this schema (note, to, from, heading, body.) come from the "https://www.w3schools.com" namespace.

This fragment:

```xml
xmlns="https://www.w3schools.com"
```

indicates that the default namespace is "https://www.w3schools.com".

This fragment:

```xml
elementFormDefault="qualified"
```

indicates that any elements used by the XML instance document which were declared in this schema must be namespace qualified.

### Simple Element

#### What is a Simple Element?

A simple element is an XML element that can contain only text.  
It cannot contain any other elements or attributes.

However, the "only text" restriction is quite misleading.  
The text can be of many different types.  
It can be one of the types included in the XML Schema definition (boolean, string, date, etc.),  
Or it can be a custom type that you can define yourself.

You can also add restrictions (facets) to a data type in order to limit its content,  
Or you can require the data to match a specific pattern.

#### Defining a Simple Element

The syntax for defining a simple element is:

```xml
<xs:element name="xxx" type="yyy"/>
```

Where xxx is the name of the element and yyy is the data type of the element.

Example:

```xml
<xs:element name="lastname" type="xs:string"/>
<xs:element name="age" type="xs:integer"/>
<xs:element name="dateborn" type="xs:date"/>
```

#### Default and Fixed Values for Simple Elements

Simple elements may have a default value OR a fixed value specified.  
A default value is automatically assigned to the element when no other value is specified.

In the following example the default value is "red":

```xml
<xs:element name="color" type="xs:string" default="red"/>
```

A fixed value is also automatically assigned to the element, and you cannot specify another value.  
In the following example the fixed value is "red":

```xml
<xs:element name="color" type="xs:string" fixed="red"/>
```

### Attributes

#### What is an Attribute?

Simple elements cannot have attributes.  
If an element has attributes, it is considered to be of a complex type.  
But the attribute itself is always declared as a simple type.

#### How to Define an Attribute?

The syntax for defining an attribute is:

```xml
<xs:attribute name="xxx" type="yyy"/>
```

Where xxx is the name of the attribute and yyy specifies the data type of the attribute.

Example:

```xml
<xs:attribute name="lang" type="xs:string"/>
```

#### Default and Fixed Values for Attributes

Attributes may have a default value OR a fixed value specified.  
A default value is automatically assigned to the attribute when no other value is specified.

In the following example the default value is "EN":

```xml
<xs:attribute name="lang" type="xs:string" default="EN"/>
```

A fixed value is also automatically assigned to the attribute,  
And you cannot specify another value.

In the following example the fixed value is "EN":

```xml
<xs:attribute name="lang" type="xs:string" fixed="EN"/>
```

#### Optional and Required Attributes

Attributes are optional by default.  
To specify that the attribute is required, use the "use" attribute:

```xml
<xs:attribute name="lang" type="xs:string" use="required"/>
```

#### Restrictions on Content

When an XML element or attribute has a data type defined,  
It puts restrictions on the element's or attribute's content.

If an XML element is of type "xs:date"  
And contains a string like "Hello World",  
The element will not validate.

With XML Schemas,  
You can also add your own restrictions to your XML elements and attributes.  
These restrictions are called facets.

### Restrictions/Facets

#### What

Restrictions are used to define acceptable values for XML elements or attributes.  
Restrictions on XML elements are called facets.

Restrictions on Values

The following example defines an element called "age" with a restriction.  
The value of age cannot be lower than 0 or greater than 120:

```xml
<xs:element name="age">
  <xs:simpleType>
    <xs:restriction base="xs:integer">
      <xs:minInclusive value="0"/>
      <xs:maxInclusive value="120"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

#### Restrictions on a Set of Values

To limit the content of an XML element to a set of acceptable values,  
We would use the enumeration constraint.

The example below defines an element called "car" with a restriction.  
The only acceptable values are: Audi, Golf, BMW:

```xml
<xs:element name="car">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:enumeration value="Audi"/>
      <xs:enumeration value="Golf"/>
      <xs:enumeration value="BMW"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

The example above could also have been written like this:

```xml
<xs:element name="car" type="carType"/>

<xs:simpleType name="carType">
  <xs:restriction base="xs:string">
    <xs:enumeration value="Audi"/>
    <xs:enumeration value="Golf"/>
    <xs:enumeration value="BMW"/>
  </xs:restriction>
</xs:simpleType>
```

:::note
In this case the type "carType" can be used by other elements because it is not a part of the "car" element.
:::

#### Restrictions on a Series of Values

To limit the content of an XML element to define a series of numbers or letters that can be used,  
We would use the pattern constraint.

The example below defines an element called "letter" with a restriction.  
The only acceptable value is `ONE` of the `LOWERCASE` letters from `a` to `z`:

```xml
<xs:element name="letter">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="[a-z]"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

The next example defines an element called "initials" with a restriction.  
The only acceptable value is THREE of the UPPERCASE letters from a to z:

```xml
<xs:element name="initials">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="[A-Z][A-Z][A-Z]"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

The next example also defines an element called "initials" with a restriction.  
The only acceptable value is THREE of the LOWERCASE OR UPPERCASE letters from a to z:

```xml
<xs:element name="initials">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="[a-zA-Z][a-zA-Z][a-zA-Z]"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

The next example defines an element called `choice` with a restriction.  
The only acceptable value is ONE of the following letters: x, y, OR z:

```xml
<xs:element name="choice">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="[xyz]"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

The next example defines an element called `prodid` with a restriction.  
The only acceptable value is FIVE digits in a sequence, and each digit must be in a range from 0 to 9:

```xml
<xs:element name="prodid">
  <xs:simpleType>
    <xs:restriction base="xs:integer">
      <xs:pattern value="[0-9][0-9][0-9][0-9][0-9]"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

#### Other Restrictions on a Series of Values

The example below defines an element called "letter" with a restriction.  
The acceptable value is zero or more occurrences of lowercase letters from a to z:

```xml
<xs:element name="letter">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="([a-z])*"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

The next example also defines an element called "letter" with a restriction.  
The acceptable value is one or more pairs of letters,  
Each pair consisting of a lower case letter followed by an upper case letter.

For example, "sToP" will be validated by this pattern,  
But not "Stop" or "STOP" or "stop":

```xml
<xs:element name="letter">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="([a-z][A-Z])+"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

The next example defines an element called "gender" with a restriction.  
The only acceptable value is male OR female:

```xml
<xs:element name="gender">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="male|female"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

The next example defines an element called "password" with a restriction.  
There must be exactly eight characters in a row and those characters must be lowercase or uppercase letters from a to z, or a number from 0 to 9:

```xml
<xs:element name="password">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="[a-zA-Z0-9]{8}"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

#### Restrictions on Whitespace Characters

To specify how whitespace characters should be handled, we would use the whiteSpace constraint.

This example defines an element called "address" with a restriction.  
The whiteSpace constraint is set to "preserve",  
Which means that the XML processor WILL NOT remove any white space characters:

```xml
<xs:element name="address">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:whiteSpace value="preserve"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

This example also defines an element called "address" with a restriction.  
The whiteSpace constraint is set to "replace",  
which means that the XML processor WILL REPLACE all white space characters (line feeds, tabs, spaces, and carriage returns) with spaces:

```xml
<xs:element name="address">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:whiteSpace value="replace"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

This example also defines an element called "address" with a restriction.  
The whiteSpace constraint is set to "collapse",  
Which means that the XML processor WILL REMOVE all white space characters (line feeds, tabs, spaces, carriage returns are replaced with spaces, leading and trailing spaces are removed, and multiple spaces are reduced to a single space):

```xml
<xs:element name="address">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:whiteSpace value="collapse"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

#### Restrictions on Length

To limit the length of a value in an element,  
We would use the length, maxLength, and minLength constraints.

This example defines an element called "password" with a restriction.  
The value must be exactly eight characters:

```xml
<xs:element name="password">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:length value="8"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

This example defines another element called "password" with a restriction.  
The value must be minimum five characters and maximum eight characters:

```xml
<xs:element name="password">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:minLength value="5"/>
      <xs:maxLength value="8"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

#### Restrictions for Data Types

| Constraint     | Description                                                                                             |
| -------------- | ------------------------------------------------------------------------------------------------------- |
| enumeration    | Defines a list of acceptable values                                                                     |
| fractionDigits | Specifies the maximum number of decimal places allowed. Must be equal to or greater than zero           |
| length         | Specifies the exact number of characters or list items allowed. Must be equal to or greater than zero   |
| maxExclusive   | Specifies the upper bounds for numeric values (the value must be less than this value)                  |
| maxInclusive   | Specifies the upper bounds for numeric values (the value must be less than or equal to this value)      |
| maxLength      | Specifies the maximum number of characters or list items allowed. Must be equal to or greater than zero |
| minExclusive   | Specifies the lower bounds for numeric values (the value must be greater than this value)               |
| minInclusive   | Specifies the lower bounds for numeric values (the value must be greater than or equal to this value)   |
| minLength      | Specifies the minimum number of characters or list items allowed. Must be equal to or greater than zero |
| pattern        | Defines the exact sequence of characters that are acceptable                                            |
| totalDigits    | Specifies the exact number of digits allowed. Must be greater than zero                                 |
| whiteSpace     | Specifies how white space (line feeds, tabs, spaces, and carriage returns) is handled                   |

### Complex Elements

#### What is a Complex Element?

A complex element contains other elements and/or attributes.

There are 4 kinds of complex elements:

- empty elements
- elements that contain only other elements
- elements that contain only text
- elements that contain both other elements and text

Note: Each of these elements may contain attributes as well!

#### Examples of Complex Elements

A complex XML element, "product", which is empty:

```xml
<product pid="1345"/>
```

A complex XML element, "employee", which contains only other elements:

```xml
<employee>
  <firstname>John</firstname>
  <lastname>Smith</lastname>
</employee>
```

A complex XML element, "food", which contains only text:

```xml
<food type="dessert">Ice cream</food>
```

A complex XML element, "description", which contains both elements and text:

```xml
<description>
It happened on <date lang="norwegian">03.03.99</date> ....
</description>
```

#### How to Define a Complex Element

Look at this complex XML element, "employee", which contains only other elements:

```xml
<employee>
  <firstname>John</firstname>
  <lastname>Smith</lastname>
</employee>
```

We can define a complex element in an XML Schema two different ways:

1. The "employee" element can be declared directly by naming the element, like this:

```xml
<xs:element name="employee">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="firstname" type="xs:string"/>
      <xs:element name="lastname" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

If you use the method described above, only the "employee" element can use the specified complex type.  
Note that the child elements, "firstname" and "lastname", are surrounded by the `<sequence>` indicator.

This means that the child elements must appear in the same order as they are declared.  
You will learn more about indicators in the XSD Indicators chapter.

1. The "employee" element can have a type attribute that refers to the name of the complex type to use:

```xml
<xs:element name="employee" type="personinfo"/>

<xs:complexType name="personinfo">
  <xs:sequence>
    <xs:element name="firstname" type="xs:string"/>
    <xs:element name="lastname" type="xs:string"/>
  </xs:sequence>
</xs:complexType>
```

If you use the method described above, several elements can refer to the same complex type, like this:

```xml
<xs:element name="employee" type="personInfo"/>
<xs:element name="student" type="personInfo"/>
<xs:element name="member" type="personInfo"/>

<xs:complexType name="personInfo">
  <xs:sequence>
    <xs:element name="firstname" type="xs:string"/>
    <xs:element name="lastname" type="xs:string"/>
  </xs:sequence>
</xs:complexType>
```

You can also base a complex type on an existing complex type and add some elements, like this:

```xml
<xs:element name="employee" type="fullPersonInfo"/>

<xs:complexType name="personInfo">
  <xs:sequence>
    <xs:element name="firstName" type="xs:string"/>
    <xs:element name="lastName" type="xs:string"/>
  </xs:sequence>
</xs:complexType>

<xs:complexType name="fullPersonInfo">
  <xs:complexContent>
    <xs:extension base="personInfo">
      <xs:sequence>
        <xs:element name="address" type="xs:string"/>
        <xs:element name="city" type="xs:string"/>
        <xs:element name="country" type="xs:string"/>
      </xs:sequence>
    </xs:extension>
  </xs:complexContent>
</xs:complexType>
```

### Empty

#### Complex Empty Elements

An empty complex element cannot have contents, only attributes.

An empty XML element:

```xml
<product prodid="1345" />
```

The "product" element above has no content at all.  
To define a type with no content,  
We must define a type that allows elements in its content, but we do not actually declare any elements, like this:

```xml
<xs:element name="product">
  <xs:complexType>
    <xs:complexContent>
      <xs:restriction base="xs:integer">
        <xs:attribute name="prodid" type="xs:positiveInteger"/>
      </xs:restriction>
    </xs:complexContent>
  </xs:complexType>
</xs:element>
```

In the example above, we define a complex type with a complex content.  
The complexContent element signals that we intend to restrict or extend the content model of a complex type,  
And the restriction of integer declares one attribute but does not introduce any element content.

However, it is possible to declare the "product" element more compactly, like this:

```xml
<xs:element name="product">
  <xs:complexType>
    <xs:attribute name="prodid" type="xs:positiveInteger"/>
  </xs:complexType>
</xs:element>
```

Or you can give the complexType element a name,  
And let the "product" element have a type attribute that refers to the name of the complexType (if you use this method, several elements can refer to the same complex type):

```xml
<xs:element name="product" type="prodType"/>

<xs:complexType name="prodType">
  <xs:attribute name="prodid" type="xs:positiveInteger"/>
</xs:complexType>
```
