# APIs Notes

## References

https://blog.postman.com/different-types-of-apis/

https://blog.postman.com/rest-api-examples/

https://blog.postman.com/what-are-the-components-of-an-api/

## What

APIs are one of the most important components of modern-day development,  
Forming the bridges between applications to transfer information and deliver services.

However, even as developers and C-suite executives increasingly consider APIs early in the development lifecycle,  
There remains some confusion about which types of APIs are best suited to particular applications.

Each API type has its own architecture,  
Which evolved to meet the demands of that time.

And as technology has developed over the years,  
And our relationship to technology has shifted,  
We’ve seen APIs emerge to fill new gaps and serve different uses.

## Types

### REST

REST APIs are designed to make server-side data readily available,  
By representing it in simple formats such as JSON and XML.

The acronym stands for **REpresentational State Transfer**,  
And it was released in 2000 after being introduced in an academic thesis by Roy Fielding.

This particular type of API adheres to 6 specific architectural constraints:

- A uniform interface
- Completely stateless
- Native caching
- Client-server architecture
- A layered system
- The ability to provide executable code to the client

#### Pros

Operations are executed with different HTTP methods including GET, POST, PUT, DELETE, OPTIONS, and PATCH.

By leveraging these functions,  
REST APIs become extremely capable across the internet.

The key benefits of this API type are that the client and the server are completely decoupled from one another.  
This allows for abstraction layers that help to maintain flexibility even as a system grows and evolves.

In addition, REST is cache friendly and supports multiple formats,  
Which is important when you’re building public-facing APIs.

The flexible data formatting that you get as a result makes them extremely useful for varied applications.

REST APIs are most commonly used as management APIs to interact with objects in a system.

They also are useful when you’re building simple resource-driven apps that don’t need much in terms of query flexibility.

#### Cons

Where REST APIs fall short is that their rich metadata creates big payloads,  
That can sometimes cause more trouble than they’re worth.

You can get over- and under-fetching problems that require further API requests, bogging down the process.

From an industry perspective,  
Another key externality resulting from the flexibility is that there is no binding contract on what structure is used for messages.  
As a result, there is a lot of back and forth when it comes to implementation,  
Which can cause unnecessary frustration and bottlenecks.
