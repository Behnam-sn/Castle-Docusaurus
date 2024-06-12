---
sidebar_position: 2
---

# Evolving Design Decisions

In the modern, fast-paced world we inhabit, companies cannot afford to be lethargic.  
To keep up with the competition, they have to continually change, evolve, and even reinvent themselves over time.

We cannot ignore this fact when designing systems,  
Especially if we intend to design software that’s well adapted to the requirements of its business domain.

When changes are not managed properly,  
Even the most sophisticated and thoughtful design will eventually become a nightmare to maintain and evolve.

This chapter discusses how changes in a software project’s environment can affect design decisions and how to evolve the design accordingly.

We will examine the four most common vectors of change:

- Business Domain
- Organizational Structure
- Domain Knowledge
- Growth

## Conclusion

As Heraclitus famously said,  
The only constant in life is change.

Businesses are no exception.  
To stay competitive,  
Companies constantly strive to evolve and reinvent themselves.  
Those changes should be treated as first-class elements of the design process.

As the business domain evolves,  
Changes to its subdomains must be identified and acted on in the system’s design.

Make sure your past design decisions are aligned with the current state of the business domain and its subdomains.  
When needed, evolve your design to better match the current business strategy and needs.

It’s also important to recognize that changes in the organizational structure can affect communication and cooperation among teams and the ways their bounded contexts can be integrated.

Learning about the business domain is an ongoing process.  
As more domain knowledge is discovered over time,  
It has to be leveraged to evolve strategic and tactical design decisions.

Finally, software growth is a desired type of change,  
but when it is not managed correctly,  
It may have disastrous effects on the system design and architecture.  
Therefore:

- When a subdomain’s functionality is expanded, try to identify more finer-grained subdomain boundaries that will enable you to make better design decisions.

- Don’t allow a bounded context to become a “jack of all trades.” Make sure the models encompassed by bounded contexts are focused to solve specific problems.

- Make sure your aggregates’ boundaries are as small as possible. Use the heuristic of strongly consistent data to detect possibilities to extract business logic into new aggregates.

My final words of wisdom on the topic are to continuously check the different
boundaries for signs of growth-driven complexity. Act to eliminate accidental com‐
plexities, and use domain-driven design tools to manage the business domain’s essen‐
tial complexity.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
