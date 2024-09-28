# Cookies

## Overview

An HTTP cookie stores information in a user's web browser.

Web servers generate cookies and send them to browsers,  
Which then include the cookies in future HTTP requests.

## What Are Cookies?

Cookies are small files of information that a web server generates and sends to a web browser.

Web browsers store the cookies they receive for a predetermined period of time,  
Or for the length of a user's session on a website.

They attach the relevant cookies to any future requests the user makes of the web server.

Cookies help inform websites about the user,  
Enabling the websites to personalize the user experience.

For example,  
E-commerce websites use cookies to know what merchandise users have placed in their shopping carts.

In addition,  
Some cookies are necessary for security purposes,  
Such as authentication.

:::note
The cookies that are used on the Internet are also called "HTTP cookies".  
Like much of the web, cookies are sent using the HTTP protocol.
:::

## Where Are Cookies Stored?

Web browsers store cookies in a designated file on users' devices.

For instance,  
The Google Chrome web browser stores all cookies in a file labeled "Cookies".

## What Are Cookies Used For?

### User Sessions

Cookies help associate website activity with a specific user.

A session cookie contains a unique string (a combination of letters and numbers),  
That matches a user session with relevant data and content for that user.

Suppose Alice has an account on a shopping website.  
She logs into her account from the website's homepage.

When she logs in,  
The website's server generates a session cookie,  
And sends the cookie to Alice's browser.

This cookie tells the website to load Alice's account content,  
So that the homepage now reads, "Welcome, Alice".

Alice then clicks to a product page displaying a pair of jeans.

When Alice's web browser sends an HTTP request to the website for the jeans product page,

it includes Alice's session cookie with the request.

Because the website has this cookie,  
It recognizes the user as Alice,  
And she does not have to log in again when the new page loads.

## References

- [www.cloudflare.com/learning/privacy/what-are-cookies/](https://www.cloudflare.com/learning/privacy/what-are-cookies/)
