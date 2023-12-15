# Digital Certificates

## What are Digital Certificates?

Digital certificates contain information about a user or firm that has been vouched for by a trusted organization.  
Digital certificates, are like ID cards.

A digital certificate is a file or electronic password that proves the authenticity of a device, server, or user through the use of cryptography and the public key infrastructure (PKI).

Digital certificate authentication helps organizations ensure that only trusted devices and users can connect to their networks. Another common use of digital certificates is to confirm the authenticity of a website to a web browser, which is also known as a secure sockets layer or SSL certificate.

## Why we Need Digital Certificates?

We all carry many forms of identification.  
Some IDs, such as passports and drivers’ licenses, are trusted enough to prove one’s identity in many situations.

For example, a U.S. driver’s license is sufficient proof of identity to let you board an airplane to New York.

More trusted forms of identification, such as passports, are signed and stamped by a government on special paper.  
They are harder to forge, so they inherently carry a higher level of trust.

Some corporate badges and smart cards include electronics to help strengthen the identity of the carrier.  
Some top-secret government organizations even need to match up your fingerprints or retinal capillary patterns with your ID before trusting it!

## What is in a Digital Certificate?

A digital certificate contains identifiable information, such as a user’s name, company, or department and a device’s Internet Protocol (IP) address or serial number. Digital certificates contain a copy of a public key from the certificate holder, which needs to be matched to a corresponding private key to verify it is real. A public key certificate is issued by certificate authorities (CAs), which sign certificates to verify the identity of the requesting device or user.

Digital certificates also contain a set of information, all of which is digitally signed by an official “certificate authority.”  
Basic digital certificates commonly contain basic things common to printed IDs, such as:

- Subject’s name (person, server, organization, etc.)
- Expiration date
- Certificate issuer (who is vouching for the certificate)
- Digital signature from the certificate issuer

Additionally, digital certificates often contain the public key of the subject,  
as well as descriptive information about the subject and about the signature algorithm used.

## What Are the Types of Digital Certificates?

There are three different types of public key certificates:  
a transport layer security (TLS)/SSL certificate, a code signing certificate, and a client certificate.

### TLS/SSL Certificate

A TLS/SSL certificate sits on a server— such as an application, mail, or web server—to ensure communication with its clients is private and encrypted.
The certificate provides authentication for the server to send and receive encrypted messages to clients.
The existence of a TLS/SSL certificate is signified by the Hypertext Transfer Protocol Secure (HTTPS) designation at the start of a Uniform Resource Locator (URL) or web address. It comes in three forms:

#### Domain Validated

A domain validated certificate is a quick validation method that is acceptable for any website. It is cheap to obtain and can be issued in a matter of minutes.

#### Organization Validated

This provides light business authentication and is ideal for organizations selling products online through e-commerce.

#### Extended Validation

This offers full business authentication, which is required by larger organizations or any business dealing with highly sensitive information. It is typically used by businesses in the financial industry and offers the highest level of authentication, security, and trust.

### Code Signing Certificate

A code signing certificate is used to confirm the authenticity of software or files downloaded through the internet. The developer or publisher signs the software to confirm that it is genuine to users that download it. This is useful for software providers that make their programs available on third-party sites to prove that files have not been tampered with.

### Client Certificate

A client certificate is a digital ID that identifies an individual user to another user or machine, or one machine to another. A common example of this is email, where a sender signs a communication digitally and its signature is verified by the recipient. Client certificates can also be used to help users access protected databases.

### Who Can Issue a Digital Certificate?

Anyone can create a digital certificate,  
But not everyone can get a well-respected signing authority to vouch for the certificate’s information and sign the certificate with its private key.

Digital certificates are issued by CAs, which sign a certificate to prove the authenticity of the individual or organization that issued the request. A CA is responsible for managing domain control verification and verifying that the public key attached to the certificate belongs to the user or organization that requested it. They play an important part in the PKI process and keeping internet traffic secure.

## References

- HTTP The Definitive Guide - David Gourley, Brian Totty - OReilly
- [fortinet.com](https://www.fortinet.com/resources/cyberglossary/digital-certificates)

https://www.okta.com/identity-101/digital-certificate
https://en.wikipedia.org/wiki/Public_key_certificate
https://www.techtarget.com/searchsecurity/definition/digital-certificate
