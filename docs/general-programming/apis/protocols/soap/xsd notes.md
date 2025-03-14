# XSD Notes

https://en.wikipedia.org/wiki/XML_Schema_(W3C)

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
