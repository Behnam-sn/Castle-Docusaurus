# XSD Notes

https://www.techtarget.com/whatis/definition/XSD-XML-Schema-Definition
https://www.ibm.com/docs/en/iis/11.5?topic=types-xml-schema-definition-xsd-assets
https://learn.microsoft.com/en-us/previous-versions/windows/desktop/ms765537(v=vs.85)
https://learn.microsoft.com/en-us/dotnet/standard/serialization/xml-schema-definition-tool-xsd-exe

## What

It is primarily used to define the elements, attributes and data types the document can contain.

The information in the XSD is used to verify if each element, attribute or data type in the document matches its description.

An XSD is similar to earlier XML schema languages,  
Such as Document Type Definition (DTD),  
But it is a more powerful alternative as it provides greater control over the XML structure.

### XML schema details

In general, a schema is an abstract representation of an object's characteristics and relationship to other objects in a document.

An XML schema represents the relationships between the attributes and elements of an XML object.

The process of creating a schema involves analyzing the document's structure and defining each structural element encountered.

For example, a schema for a document describing a website would define a website element,  
A webpage element and other elements that describe possible content divisions within any page on that site.  
These elements are defined within a set of tags in HTML and also in XML.

## Features

The purpose of an XML Schema is to define the legal building blocks of an XML document:

- The elements and attributes that can appear in a document
- The number of (and order of) child elements
- Data types for elements and attributes
- Default and fixed values for elements and attributes

### Automation

It can be used by programmers to verify each piece of item content in a document,  
To assure it adheres to the description of the element it is placed in.

### Log

Like all XML schema languages,  
XSD can be used to express a set of rules,  
To which an XML document must conform to be considered **valid** according to that schema.

However, unlike most other schema languages,  
XSD was also designed with the intent that determination of a document's validity would produce a collection of information adhering to specific data types.

Such a post-validation infoset can be useful in the development of XML document processing software.

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

```xml
<?xml version="1.0"?>
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

### Elements Only

#### Complex Types Containing Elements Only

An "elements-only" complex type contains an element that contains only other elements.

An XML element, "person", that contains only other elements:

```xml
<person>
  <firstname>John</firstname>
  <lastname>Smith</lastname>
</person>
```

You can define the "person" element in a schema, like this:

```xml
<xs:element name="person">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="firstname" type="xs:string"/>
      <xs:element name="lastname" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

Notice the `<xs:sequence>` tag.  
It means that the elements defined ("firstname" and "lastname") must appear in that order inside a "person" element.

Or you can give the complexType element a name,  
And let the "person" element have a type attribute that refers to the name of the complexType  
(if you use this method, several elements can refer to the same complex type):

```xml
<xs:element name="person" type="persontype"/>

<xs:complexType name="persontype">
  <xs:sequence>
    <xs:element name="firstname" type="xs:string"/>
    <xs:element name="lastname" type="xs:string"/>
  </xs:sequence>
</xs:complexType>
```

### Text-Only Elements

#### What

A complex text-only element can contain text and attributes.

This type contains only simple content (text and attributes),  
Therefore we add a simpleContent element around the content.

When using simple content,  
You must define an extension OR a restriction within the simpleContent element, like this:

```xml
<xs:element name="somename">
  <xs:complexType>
    <xs:simpleContent>
      <xs:extension base="basetype">
        ....
        ....
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>
</xs:element>
```

OR

```xml
<xs:element name="somename">
  <xs:complexType>
    <xs:simpleContent>
      <xs:restriction base="basetype">
        ....
        ....
      </xs:restriction>
    </xs:simpleContent>
  </xs:complexType>
</xs:element>
```

:::tip
Use the extension/restriction element to expand or to limit the base simple type for the element.
:::

Here is an example of an XML element, "shoesize", that contains text-only:

```xml
<shoesize country="france">35</shoesize>
```

The following example declares a complexType, "shoesize".  
The content is defined as an integer value, and the "shoesize" element also contains an attribute named "country":

```xml
<xs:element name="shoesize">
  <xs:complexType>
    <xs:simpleContent>
      <xs:extension base="xs:integer">
        <xs:attribute name="country" type="xs:string" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>
</xs:element>
```

We could also give the complexType element a name,  
And let the "shoesize" element have a type attribute that refers to the name of the complexType  
(if you use this method, several elements can refer to the same complex type):

```xml
<xs:element name="shoesize" type="shoetype"/>

<xs:complexType name="shoetype">
  <xs:simpleContent>
    <xs:extension base="xs:integer">
      <xs:attribute name="country" type="xs:string" />
    </xs:extension>
  </xs:simpleContent>
</xs:complexType>
```

### Mixed Content

#### Complex Types with Mixed Content

A mixed complex type element can contain attributes, elements, and text.

An XML element, "letter", that contains both text and other elements:

```xml
<letter>
  Dear Mr. <name>John Smith</name>.
  Your order <orderid>1032</orderid>
  will be shipped on <shipdate>2001-07-13</shipdate>.
</letter>
```

The following schema declares the "letter" element:

```xml
<xs:element name="letter">
  <xs:complexType mixed="true">
    <xs:sequence>
      <xs:element name="name" type="xs:string"/>
      <xs:element name="orderid" type="xs:positiveInteger"/>
      <xs:element name="shipdate" type="xs:date"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

:::note
To enable character data to appear between the child-elements of "letter", the mixed attribute must be set to "true".  
The `<xs:sequence>` tag means that the elements defined (name, orderid and shipdate) must appear in that order inside a "letter" element.
:::

We could also give the complexType element a name, and let the "letter" element have a type attribute that refers to the name of the complexType (if you use this method, several elements can refer to the same complex type):

```xml
<xs:element name="letter" type="lettertype"/>

<xs:complexType name="lettertype" mixed="true">
  <xs:sequence>
    <xs:element name="name" type="xs:string"/>
    <xs:element name="orderid" type="xs:positiveInteger"/>
    <xs:element name="shipdate" type="xs:date"/>
  </xs:sequence>
</xs:complexType>
```

### Indicators

We can control HOW elements are to be used in documents with indicators.

There are 7 indicators:

Order indicators:

- All
- Choice
- Sequence

Occurrence indicators:

- maxOccurs
- minOccurs

Group indicators:

- Group name
- attributeGroup name

#### Order Indicators

Order indicators are used to define the order of the elements.

##### All Indicator

The `<all>` indicator specifies that the child elements can appear in any order,  
And that each child element must occur only once:

```xml
<xs:element name="person">
  <xs:complexType>
    <xs:all>
      <xs:element name="firstname" type="xs:string"/>
      <xs:element name="lastname" type="xs:string"/>
    </xs:all>
  </xs:complexType>
</xs:element>
```

:::note
When using the `<all>` indicator you can set the `<minOccurs>` indicator to 0 or 1 and the `<maxOccurs>` indicator can only be set to 1 (the `<minOccurs>` and `<maxOccurs>` are described later).
:::

##### Choice Indicator

The `<choice>` indicator specifies that either one child element or another can occur:

```xml
<xs:element name="person">
  <xs:complexType>
    <xs:choice>
      <xs:element name="employee" type="employee"/>
      <xs:element name="member" type="member"/>
    </xs:choice>
  </xs:complexType>
</xs:element>
```

##### Sequence Indicator

The `<sequence>` indicator specifies that the child elements must appear in a specific order:

```xml
<xs:element name="person">
   <xs:complexType>
    <xs:sequence>
      <xs:element name="firstName" type="xs:string"/>
      <xs:element name="lastName" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

#### Occurrence Indicators

Occurrence indicators are used to define how often an element can occur.

:::note
For all "Order" and "Group" indicators (any, all, choice, sequence, group name, and group reference) the default value for maxOccurs and minOccurs is 1.
:::

##### maxOccurs Indicator

The `<maxOccurs>` indicator specifies the maximum number of times an element can occur:

```xml
<xs:element name="person">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="full_name" type="xs:string"/>
      <xs:element name="child_name" type="xs:string" maxOccurs="10"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

The example above indicates that the "child_name" element can occur a minimum of one time (the default value for minOccurs is 1) and a maximum of ten times in the "person" element.

##### minOccurs Indicator

The `<minOccurs>` indicator specifies the minimum number of times an element can occur:

```xml
<xs:element name="person">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="full_name" type="xs:string"/>
      <xs:element name="child_name" type="xs:string"
      maxOccurs="10" minOccurs="0"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

The example above indicates that the "child_name" element can occur a minimum of zero times and a maximum of ten times in the "person" element.

Tip: To allow an element to appear an unlimited number of times, use the maxOccurs="unbounded" statement:

A working example:

An XML file called "Myfamily.xml":

```xml
<?xml version="1.0" encoding="UTF-8"?>

<persons xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:noNamespaceSchemaLocation="family.xsd">

  <person>
    <full_name>Hege Refsnes</full_name>
    <child_name>Cecilie</child_name>
  </person>

  <person>
    <full_name>Tove Refsnes</full_name>
    <child_name>Hege</child_name>
    <child_name>Stale</child_name>
    <child_name>Jim</child_name>
    <child_name>Borge</child_name>
  </person>

  <person>
    <full_name>Stale Refsnes</full_name>
  </person>

</persons>
```

#### Group Indicators

Group indicators are used to define related sets of elements.

##### Element Groups

Element groups are defined with the group declaration, like this:

```xml
<xs:group name="groupname">
...
</xs:group>
```

You must define an all, choice, or sequence element inside the group declaration.  
The following example defines a group named "persongroup",  
That defines a group of elements that must occur in an exact sequence:

```xml
<xs:group name="persongroup">
  <xs:sequence>
    <xs:element name="firstname" type="xs:string"/>
    <xs:element name="lastname" type="xs:string"/>
    <xs:element name="birthday" type="xs:date"/>
  </xs:sequence>
</xs:group>
```

After you have defined a group,  
You can reference it in another definition,  
Like this:

```xml
<xs:group name="persongroup">
  <xs:sequence>
    <xs:element name="firstname" type="xs:string"/>
    <xs:element name="lastname" type="xs:string"/>
    <xs:element name="birthday" type="xs:date"/>
  </xs:sequence>
</xs:group>

<xs:element name="person" type="personinfo"/>

<xs:complexType name="personinfo">
  <xs:sequence>
    <xs:group ref="persongroup"/>
    <xs:element name="country" type="xs:string"/>
  </xs:sequence>
</xs:complexType>
```

##### Attribute Groups

Attribute groups are defined with the attributeGroup declaration,  
Like this:

```xml
<xs:attributeGroup name="groupname">
...
</xs:attributeGroup>
```

The following example defines an attribute group named "personattrgroup":

```xml
<xs:attributeGroup name="personattrgroup">
  <xs:attribute name="firstname" type="xs:string"/>
  <xs:attribute name="lastname" type="xs:string"/>
  <xs:attribute name="birthday" type="xs:date"/>
</xs:attributeGroup>
```

After you have defined an attribute group,  
You can reference it in another definition,  
Like this:

```xml
<xs:attributeGroup name="personattrgroup">
  <xs:attribute name="firstname" type="xs:string"/>
  <xs:attribute name="lastname" type="xs:string"/>
  <xs:attribute name="birthday" type="xs:date"/>
</xs:attributeGroup>

<xs:element name="person">
  <xs:complexType>
    <xs:attributeGroup ref="personattrgroup"/>
  </xs:complexType>
</xs:element>
```

### any

The `<any>` element enables us to extend the XML document with elements not specified by the schema.

The following example is a fragment from an XML schema called "family.xsd".  
It shows a declaration for the "person" element.  
By using the `<any>` element we can extend (after `<lastname>`) the content of "person" with any element:

```xml
<xs:element name="person">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="firstname" type="xs:string"/>
      <xs:element name="lastname" type="xs:string"/>
      <xs:any minOccurs="0"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

Now we want to extend the "person" element with a "children" element.  
In this case we can do so,  
Even if the author of the schema above never declared any "children" element.

Look at this schema file, called "children.xsd":

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
targetNamespace="https://www.w3schools.com"
xmlns="https://www.w3schools.com"
elementFormDefault="qualified">

<xs:element name="children">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="childname" type="xs:string"
      maxOccurs="unbounded"/>
    </xs:sequence>
  </xs:complexType>
</xs:element>

</xs:schema>
```

The XML file below (called "Myfamily.xml"),  
Uses components from two different schemas;  
"family.xsd" and "children.xsd":

```xml
<?xml version="1.0" encoding="UTF-8"?>

<persons xmlns="http://www.microsoft.com"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://www.microsoft.com family.xsd
https://www.w3schools.com children.xsd">

  <person>
    <firstname>Hege</firstname>
    <lastname>Refsnes</lastname>
    <children>
      <childname>Cecilie</childname>
    </children>
  </person>

  <person>
    <firstname>Stale</firstname>
    <lastname>Refsnes</lastname>
  </person>

</persons>
```

The XML file above is valid because the schema "family.xsd" allows us to extend the "person" element with an optional element after the "lastname" element.

The `<any>` and `<anyAttribute>` elements are used to make EXTENSIBLE documents!  
They allow documents to contain additional elements that are not declared in the main XML schema.

#### anyAttribute

The `<anyAttribute>` element enables us to extend the XML document with attributes not specified by the schema.

The following example is a fragment from an XML schema called "family.xsd".  
It shows a declaration for the "person" element.  
By using the `<anyAttribute>` element we can add any number of attributes to the "person" element:

```xml
<xs:element name="person">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="firstname" type="xs:string"/>
      <xs:element name="lastname" type="xs:string"/>
    </xs:sequence>
    <xs:anyAttribute/>
  </xs:complexType>
</xs:element>
```

Now we want to extend the "person" element with a "eyecolor" attribute.  
In this case we can do so, even if the author of the schema above never declared any "eyecolor" attribute.

Look at this schema file, called "attribute.xsd":

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
targetNamespace="https://www.w3schools.com"
xmlns="https://www.w3schools.com"
elementFormDefault="qualified">

<xs:attribute name="eyecolor">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="blue|brown|green|grey"/>
    </xs:restriction>
  </xs:simpleType>
</xs:attribute>

</xs:schema>
```

The XML file below (called "Myfamily.xml"),  
Uses components from two different schemas;  
"family.xsd" and "attribute.xsd":

```xml
<?xml version="1.0" encoding="UTF-8"?>

<persons xmlns="http://www.microsoft.com"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:SchemaLocation="http://www.microsoft.com family.xsd
  https://www.w3schools.com attribute.xsd">

  <person eyecolor="green">
    <firstname>Hege</firstname>
    <lastname>Refsnes</lastname>
  </person>

  <person eyecolor="blue">
    <firstname>Stale</firstname>
    <lastname>Refsnes</lastname>
  </person>

</persons>
```

The XML file above is valid because the schema "family.xsd" allows us to add an attribute to the "person" element.

The `<any>` and `<anyAttribute>` elements are used to make EXTENSIBLE documents!  
They allow documents to contain additional elements that are not declared in the main XML schema.

#### Substitution

With XML Schemas, one element can substitute another element.

Let's say that we have users from two different countries: England and Norway.  
We would like the ability to let the user choose whether he or she would like to use the Norwegian element names or the English element names in the XML document.

To solve this problem, we could define a substitutionGroup in the XML schema.  
First, we declare a head element and then we declare the other elements which state that they are substitutable for the head element.

```xml
<xs:element name="name" type="xs:string"/>
<xs:element name="navn" substitutionGroup="name"/>
```

In the example above, the "name" element is the head element and the "navn" element is substitutable for "name".  
Look at this fragment of an XML schema:

```xml
<xs:element name="name" type="xs:string"/>
<xs:element name="navn" substitutionGroup="name"/>

<xs:complexType name="custinfo">
  <xs:sequence>
    <xs:element ref="name"/>
  </xs:sequence>
</xs:complexType>

<xs:element name="customer" type="custinfo"/>
<xs:element name="kunde" substitutionGroup="customer"/>
```

A valid XML document (according to the schema above) could look like this:

```xml
<customer>
  <name>John Smith</name>
</customer>
```

or like this:

```xml
<kunde>
  <navn>John Smith</navn>
</kunde>
```

##### Blocking Element Substitution

To prevent other elements from substituting with a specified element, use the block attribute:

```xml
<xs:element name="name" type="xs:string" block="substitution"/>
```

Look at this fragment of an XML schema:

```xml
<xs:element name="name" type="xs:string" block="substitution"/>
<xs:element name="navn" substitutionGroup="name"/>

<xs:complexType name="custinfo">
  <xs:sequence>
    <xs:element ref="name"/>
  </xs:sequence>
</xs:complexType>

<xs:element name="customer" type="custinfo" block="substitution"/>
<xs:element name="kunde" substitutionGroup="customer"/>
```

A valid XML document (according to the schema above) looks like this:

```xml
<customer>
  <name>John Smith</name>
</customer>
```

BUT THIS IS NO LONGER VALID:

```xml
<kunde>
  <navn>John Smith</navn>
</kunde>
```

##### Using substitutionGroup

The type of the substitutable elements must be the same as, or derived from, the type of the head element.  
If the type of the substitutable element is the same as the type of the head element you will not have to specify the type of the substitutable element.

Note that all elements in the substitutionGroup (the head element and the substitutable elements) must be declared as global elements, otherwise it will not work!

##### What are Global Elements?

Global elements are elements that are immediate children of the "schema" element!  
Local elements are elements nested within other elements.
