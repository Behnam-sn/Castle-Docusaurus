---
sidebar_position: 5
---

# Domain Knowledge Changes

As you’ll recall, the core tenet of domain-driven design is,  
Domain knowledge is essential for designing a successful software system.

Acquiring domain knowledge is one of the most challenging aspects of software engineering,
Especially for the core subdomains.

A core subdomain’s logic is not only complicated,  
But also expected to change often.

Moreover, modeling is an ongoing process.  
Models have to improve as more knowledge of the business domain is acquired.

Many times, the business domain’s complexity is implicit.  
Initially, everything seems simple and straightforward.

The initial simplicity is often deceptive and it quickly morphs into complexity.  
As more functionality is added, more and more edge cases, invariants, and rules are discovered.

Such insights are often disruptive,  
Requiring rebuilding the model from the ground up,  
Including the boundaries of the bounded contexts, aggregates, and other implementation details.

From a strategic design standpoint,  
It’s a useful heuristic to design the bounded contexts’ boundaries according to the level of domain knowledge.

The cost of decomposing a system into bounded contexts,  
Over time, that turn out to be incorrect can be high.

Therefore, when the domain logic is unclear and changes often,  
It makes sense to design the bounded contexts with broader boundaries.

Then, as domain knowledge is discovered over time and changes to the business logic stabilize,  
Those broad bounded contexts can be decomposed into contexts with narrower boundaries, or microservices.

When new domain knowledge is discovered,  
It should be leveraged to evolve the design and make it more resilient.

Unfortunately, changes in domain knowledge are not always positive:  
Domain knowledge can be lost.

As time goes by,  
Documentation often becomes stale.

People who were working on the original design leave the company,  
And new functionality is added in an ad hoc manner until,  
At one point, the codebase gains the dubious status of a legacy system.

It’s vital to prevent such degradation of domain knowledge proactively.  
An effective tool for recovering domain knowledge is the EventStorming workshop.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
