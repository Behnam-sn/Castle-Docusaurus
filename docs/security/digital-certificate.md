# Digital Certificate

## What is a Digital Certificate?

<!-- Digital certificates contain information about a user or firm that has been vouched for by a trusted organization. -->

Digital certificates, also known as identity certificates or public key certificates,  
Is a form of electronic credential that can prove the authenticity of a user, device, server, or website.

## How does Digital Certificates Works?

A website, organization, or individual can request a digital certificate,  
That will then need to be validated by a publicly trusted certificate authority (CA).

Anyone can create a digital certificate,  
But not everyone can get a well-respected signing authority to vouch for the certificate’s information and sign the certificate with its private key.

Public key certificates are issued by trusted third parties, a CA (Certificate Authority), who signs the certificate,  
Thus verifying the identity of the device or user that is requesting access.

A Digital Certificate uses **PKI (Public Key Infrastructure)** to help exchange communications and data securely.  
This form of authentication is a type of cryptography that requires the use of public and private keys to validate users.

To ensure validity, the public key will be matched with a corresponding private key that only the recipient has knowledge of.  
Digital certificates have a specific key pair that they are associated with: one public and one private.

A digital certificate contains the following identifiable information:

- User’s name
- Company or department of user
- IP (internet protocol) address or serial number of device
- Copy of the public key from a certificate holder
- Duration of time the certificate is valid for
- Domain certificate is authorized to represent

<!-- ## Why we Need Digital Certificates?

Digital certificates, are like ID cards.
We all carry many forms of identification.
Some IDs, such as passports and drivers’ licenses, are trusted enough to prove one’s identity in many situations.

For example, a U.S. driver’s license is sufficient proof of identity to let you board an airplane to New York.

More trusted forms of identification, such as passports, are signed and stamped by a government on special paper.
They are harder to forge, so they inherently carry a higher level of trust.

Some corporate badges and smart cards include electronics to help strengthen the identity of the carrier.
Some top-secret government organizations even need to match up your fingerprints or retinal capillary patterns with your ID before trusting it! -->

## What Are Types of Digital Certificates?

There are 3 different types of public key certificates:

### TLS/SSL Certificates

The TLS/SSL certificate is used to secure communications between a computer and the server, and it is hosted by the server.

When a client computer seeks to access the server,  
The server will present the digital certificate to prove that it is authentic and the desired destination.

The HTTPS designation at the beginning of a web address or URL indicates the presence of a digital certificate.

### Client Certificates

This is a form of a digital ID that can identify one machine to another or a specific user to another user.  
This can be used to allow a user to access a protected and secure database and also for email.

### Code Signing Certificates

This type of digital certificate involves software or files.  
The publisher or developer of software will sign it to validate its authenticity to users downloading it.

This can be highly beneficial when software is downloaded through a third-party,  
Ensuring that it is what it should be and has not been tampered with by malicious actors.

This can confirm that files or software downloaded from the internet are valid and authentic.

## References

- [okta.com](https://www.okta.com/identity-101/digital-certificate)
- [wikipedia.org](https://en.wikipedia.org/wiki/Public_key_certificate)
- HTTP The Definitive Guide - David Gourley, Brian Totty - OReilly

https://www.techtarget.com/searchsecurity/definition/digital-certificate
