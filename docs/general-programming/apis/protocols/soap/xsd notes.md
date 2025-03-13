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
