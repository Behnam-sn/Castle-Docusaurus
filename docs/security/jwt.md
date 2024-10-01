# JWT

## Overview

JSON Web Tokens (JWT) are an open and industry standard (RFC 7519) method,  
For representing claims securely between two parties.

## What Is Json Web Tokens?

A JSON Web Token (JWT),  
Defines a compact and self-contained way,  
For securely transmitting information between parties,  
As a JSON object.

This information can be verified and trusted because it is digitally signed.

JWTs can be signed using a secret with the **HMAC** algorithm,  
Or a public/private key pair using **RSA** or **ECDSA**.

Let’s explain some concepts of this definition further.

- **Compact**

  Because of its size,  
  It can be sent through an URL, POST parameter, or inside an HTTP header.

  Additionally, due to its size its transmission is fast.

- **Self-Contained**

  The payload contains all the required information about the user,  
  To avoid querying the database more than once.

<!-- It's about encrypted JWTs -->
<!--
:::note
JWTs can be encrypted to provide secrecy between parties,
But we will focus on signed tokens.
:::

Signed tokens can verify the integrity of the claims contained within it,
While encrypted tokens hide those claims from other parties.

When tokens are signed using public/private key pairs,
The signature also certifies that only the party holding the private key is the one that signed it. -->

## Why Should We Use Json Web Tokens?

Let's talk about the benefits of **JSON Web Tokens (JWT)**,  
When compared to **Simple Web Tokens (SWT)**,  
And **Security Assertion Markup Language Tokens (SAML)**.

As JSON is less verbose than XML,  
When it is encoded its size is also smaller,  
Making JWT more compact than SAML.

This makes JWT a good choice to be passed in HTML and HTTP environments.

Security-wise,  
SWT can only be symmetrically signed by a shared secret using the HMAC algorithm.

However, JWT and SAML tokens can use a public/private key pair in the form of a X.509 certificate for signing.

Signing XML with XML Digital Signature without introducing obscure security holes is very difficult when compared to the simplicity of signing JSON.

JSON parsers are common in most programming languages because they map directly to objects.  
Conversely, XML doesn't have a natural document-to-object mapping.  
This makes it easier to work with JWT than SAML assertions.

Regarding usage, JWT is used at Internet scale.  
This highlights the ease of client-side processing of the JSON Web token on multiple platforms, especially mobile.

## When Should You Use Json Web Tokens?

Here are some scenarios where JSON Web Tokens are useful:

### Authorization

This is the most common scenario for using JWT.

Once the user is logged in,  
Each subsequent request will include the JWT,  
Allowing the user to access routes, services, and resources that are permitted with that token.

Single Sign On is a feature that widely uses JWT nowadays,  
Because of its small overhead and its ability to be easily used across different domains.

### Information Exchange

JSON Web Tokens are a good way of securely transmitting information between parties.

Because JWTs can be signed,  
(For example, using public/private key pairs),  
You can be sure the senders are who they say they are.

Additionally,  
As the signature is calculated using the header and the payload,  
You can also verify that the content hasn't been tampered with.

## How Do Json Web Tokens Work?

In authentication,  
When the user successfully logs in using their credentials,  
A JSON Web Token will be returned.

Since tokens are credentials,
Great care must be taken to prevent security issues.

Whenever the user wants to access a protected route or resource,  
The user agent should send the JWT,  
Typically in the **Authorization** header using the **Bearer** schema.

The content of the header should look like the following:

```console
Authorization: Bearer <token>
```

This can be,  
In certain cases,  
A stateless authorization mechanism.

The server's protected routes will check for a valid JWT in the Authorization header,  
And if it's present, the user will be allowed to access protected resources.

If the JWT contains the necessary data,  
The need to query the database for certain operations may be reduced,  
Though this may not always be the case.

Note that if you send JWT tokens through HTTP headers,  
You should try to prevent them from getting too big.

Some servers don't accept more than 8 KB in headers.  
If you are trying to embed too much information in a JWT token, like by including all the user's permissions, you may need an alternative solution, like Auth0 Fine-Grained Authorization.

If the token is sent in the Authorization header,  
Cross-Origin Resource Sharing (CORS) won't be an issue as it doesn't use cookies.

Do note that with signed tokens, all the information contained within the token is exposed to users or other parties, even though they are unable to change it. This means you should not put secret information within the token.

## What Is The Json Web Token Structure?

In its compact form,  
JSON Web Tokens consist of three parts separated by dots (.),  
Which are:

- Header
- Payload
- Signature

Therefore, a JWT typically looks like the following.

```console
xxxxx.yyyyy.zzzzz
```

Let's break down the different parts:

### Header

The header typically consists of two parts:

The type of the token,  
Which is JWT,

And the signing algorithm being used,  
Such as HMAC SHA256 or RSA.

For example:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

Then, this JSON is **Base64Url** encoded to form the first part of the JWT.

### Payload

The second part of the token is the payload,  
Which contains the claims.

Claims are statements about an entity (typically, the user) and additional data.

There are three types of claims:

#### Registered Claims

These are a set of pre-defined claims which are not mandatory but recommended,  
 To provide a set of useful, interoperable claims.

Some of them are: iss (issuer), exp (expiration time), sub (subject), aud (audience), and others.

:::note
Notice that the claim names are only three characters long as JWT is meant to be compact.
:::

#### Public Claims

These can be defined at will by those using JWTs.

But to avoid collisions they should be defined in the IANA JSON Web Token Registry or be defined as a URI that contains a collision resistant namespace.

#### Private Claims

These are the custom claims created to share information between parties that agree on using them and are neither registered or public claims.

An example payload could be:

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

The payload is then **Base64Url** encoded to form the second part of the JSON Web Token.

:::note
Do note that for signed tokens this information,  
Though protected against tampering,  
Is readable by anyone.

Do not put secret information in the payload or header elements of a JWT unless it is encrypted.
:::

### Signature

To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

For example if you want to use the HMAC SHA256 algorithm, the signature will be created in the following way:

```console
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

The signature is used to verify the message wasn't changed along the way, and, in the case of tokens signed with a private key, it can also verify that the sender of the JWT is who it says it is.

### Putting All Together

The output is three Base64-URL strings separated by dots that can be easily passed in HTML and HTTP environments, while being more compact when compared to XML-based standards such as SAML.

The following shows a JWT that has the previous header and payload encoded, and it is signed with a secret.

```console
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c`
```

## References

- [jwt.io/introduction](https://jwt.io/introduction)

## More On

- https://auth0.com/learn/json-web-tokens
- https://auth0.com/docs/secure/tokens/json-web-tokens
