# APIs Notes 2

https://aws.amazon.com/what-is/api/

https://en.wikipedia.org/wiki/API

https://www.postman.com/what-is-an-api/

https://www.ibm.com/think/topics/api

## What is an API?

APIs are mechanisms that enable two software components to communicate with each other using a set of definitions and protocols.

For example, the weather bureau’s software system contains daily weather data.  
The weather app on your phone “talks” to this system via APIs and shows you daily weather updates on your phone.

An application programming interface (API) is a connection between computers or between computer programs.

It is a type of software interface, offering a service to other pieces of software.

## What is API specification?

A document or standard that describes how to build such a connection or interface is called an API specification.

### What does API stand for?

API stands for **Application Programming Interface**.

In the context of APIs,  
The word Application refers to any software with a distinct function.

Interface can be thought of as a contract of service between two applications.

This contract defines how the two communicate with each other using requests and responses.

Their API documentation contains information on how developers are to structure those requests and responses.

## Why?

One purpose of APIs is to hide the internal details of how a system works, exposing only those parts a programmer will find useful and keeping them consistent even if the internal details later change. An API may be custom-built for a particular pair of systems, or it may be a shared standard allowing interoperability among many systems.

## How do APIs work?

API architecture is usually explained in terms of client and server.

The application sending the request is called the client,  
And the application sending the response is called the server.

So in the weather example, the bureau’s weather database is the server, and the mobile app is the client.

There are four different ways that APIs can work depending on when and why they were created.

In contrast to a user interface, which connects a computer to a person, an application programming interface connects computers or pieces of software to each other. It is not intended to be used directly by a person (the end user) other than a computer programmer who is incorporating it into software. An API is often made up of different parts which act as tools or services that are available to the programmer. A program or a programmer that uses one of these parts is said to call that portion of the API. The calls that make up the API are also known as subroutines, methods, requests, or endpoints. An API specification defines these calls, meaning that it explains how to use or implement them.

## What is web API?

A Web API or Web Service API is an application processing interface between a web server and web browser.

All web services are APIs but not all APIs are web services.

REST API is a special type of Web API that uses the standard architectural style explained above.

The different terms around APIs,  
Like Java API or service APIs,  
Exist because historically,  
APIs were created before the world wide web.

Modern web APIs are REST APIs and the terms can be used interchangeably.

The term API is often used to refer to web APIs,[2] which allow communication between computers that are joined by the internet. There are also APIs for programming languages, software libraries, computer operating systems, and computer hardware. APIs originated in the 1940s, though the term did not emerge until the 1960s and 70s.

## What are API integrations?

API integrations are software components that automatically update data between clients and servers.

Some examples of API integrations are when automatic data sync to the cloud from your phone image gallery,  
Or the time and date automatically sync on your laptop when you travel to another time zone.

Enterprises can also use them to efficiently automate many system functions.

## How to create an API?

Due diligence and effort are required to build an API that other developers will want to work with and trust. These are the five steps required for high-quality API design:

1. Plan the API
   API specifications, like OpenAPI, provide the blueprint for your API design. It is better to think about different use cases in advance and ensure the API adheres to current API development standards.

2. Build the API
   API designers prototype APIs using boilerplate code. Once the prototype is tested, developers can customize it to internal specifications.

3. Test the API  
   API testing is the same as software testing and must be done to prevent bugs and defects. API testing tools can be used to strength test the API against cyber attacks.

4. Document the API  
   While APIs are self-explanatory, API documentation acts as a guide to improve usability. Well-documented APIs that offer a range of functions and use cases tend to be more popular in a service-oriented architecture.

5. Market the API
   Just as Amazon is an online marketplace for retail, API marketplaces exist for developers to buy and sell other APIs. Listing your API can allow you to monetize it.

## Extra

A computer system that meets this standard is said to implement or expose an API.

The term API may refer either to the specification or to the implementation.
