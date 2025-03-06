# Protocols Notes

https://aws.amazon.com/what-is/api/

https://aws.amazon.com/what-is/restful-api/

## Apis Protocols

There are four different ways that APIs can work depending on when and why they were created.

SOAP APIs

These APIs use Simple Object Access Protocol.

Client and server exchange messages using XML.

This is a less flexible API that was more popular in the past.

RPC APIs

These APIs are called Remote Procedure Calls.

The client completes a function (or procedure) on the server,  
And the server sends the output back to the client.

Websocket APIs

Websocket API is another modern web API development that uses JSON objects to pass data.

A WebSocket API supports two-way communication between client apps and the server.

The server can send callback messages to connected clients,  
Making it more efficient than REST API.

REST APIs

These are the most popular and flexible APIs found on the web today.

The client sends requests to the server as data.

The server uses this client input to start internal functions and returns output data back to the client.

## What are REST APIs?

REST stands for Representational State Transfer.

REST defines a set of functions like GET, PUT, DELETE, etc.

That clients can use to access server data.

Clients and servers exchange data using HTTP.

The main feature of REST API is statelessness.

Statelessness means that servers do not save client data between requests.

Client requests to the server are similar to URLs you type in your browser to visit a website.

The response from the server is plain data, without the typical graphical rendering of a web page.

## What are the benefits of REST APIs?

REST APIs offer four main benefits:

1. Integration
   APIs are used to integrate new applications with existing software systems. This increases development speed because each functionality doesn’t have to be written from scratch. You can use APIs to leverage existing code.

2. Innovation
   Entire industries can change with the arrival of a new app. Businesses need to respond quickly and support the rapid deployment of innovative services. They can do this by making changes at the API level without having to re-write the whole code.

3. Expansion
   APIs present a unique opportunity for businesses to meet their clients’ needs across different platforms. For example, maps API allows map information integration via websites, Android,iOS, etc. Any business can give similar access to their internal databases by using free or paid APIs.

4. Ease of maintenance
   The API acts as a gateway between two systems. Each system is obliged to make internal changes so that the API is not impacted. This way, any future code changes by one party do not impact the other party.

How to secure a REST API?
All APIs must be secured through proper authentication and monitoring. The two main ways to secure REST APIs include:

1. Authentication tokens
   These are used to authorize users to make the API call. Authentication tokens check that the users are who they claim to be and that they have access rights for that particular API call. For example, when you log in to your email server, your email client uses authentication tokens for secure access.

2. API keys
   API keys verify the program or application making the API call. They identify the application and ensure it has the access rights required to make the particular API call. API keys are not as secure as tokens but they allow API monitoring in order to gather data on usage. You may have noticed a long string of characters and numbers in your browser URL when you visit different websites. This string is an API key the website uses to make internal API calls.

What is GraphQL?
GraphQL is a query language that was developed specifically for APIs. It prioritizes giving clients exactly the data they request and no more. It is designed to make APIs fast, flexible, and developer-friendly. As an alternative to REST, GraphQL gives front-end developers the ability to query multiple databases, microservices, and APIs with a single GraphQL endpoint. Organizations choose to build APIs with GraphQL because it helps them develop applications faster. Read more about GraphQL here.

AWS AppSync is a fully managed service that makes it easy to develop GraphQL APIs by handling the heavy lifting of securely connecting to data sources like AWS DynamoDB, AWS Lambda, and more AWS AppSync can push real-time data updates over Websockets to millions of clients. For mobile and web applications, AppSync also provides local data access when devices go offline. Once deployed, AWS AppSync automatically scales GraphQL API execution engine up and down to meet API request volumes.
