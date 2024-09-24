# SOA vs Microservices

Service-oriented architecture (SOA),  
Is a design approach in which multiple services collaborate to provide a certain end set of capabilities.

A service here typically means a completely separate operating system process.

Communication between these services occurs via calls across a network rather than method calls within a process boundary.

SOA emerged as an approach to combat the challenges of large, monolithic applications.

This approach aims to promote the reusability of software;  
Two or more end-user applications, for example, could use the same services.

SOA aims to make it easier to maintain or rewrite software,  
As theoretically we can replace one service with another without anyone knowing,  
As long as the semantics of the service don’t change too much.

SOA at its heart is a sensible idea.  
However, despite many efforts, there is a lack of good consensus on how to do SOA well.

In my opinion,  
Much of the industry failed to look holistically enough at the problem,  
And present a compelling alternative to the narrative set out by various vendors in this space.

Many of the problems laid at the door of SOA,  
Are actually problems with things like communication protocols (e.g., SOAP), vendor middleware, a lack of guidance about service granularity, or the wrong guidance on picking places to split your system.

A cynic might suggest that vendors co-opted (and in some cases drove) the SOA movement as a way to sell more products,  
And those selfsame products in the end undermined the goal of SOA.

I’ve seen plenty of examples of SOA in which teams were striving to make the services smaller,  
But they still had everything coupled to a database,  
And had to deploy everything together.

Service oriented? Yes.  
But it’s not microservices.

The microservice approach has emerged from real-world use,  
Taking our better understanding of systems and architecture to do SOA well.

You should think of microservices as being a specific approach for SOA in the same way that Extreme Programming (XP) or Scrum is a specific approach for Agile software development.

## References

- Building Microservices 2nd Edition - Sam Newman - O'Reilly
