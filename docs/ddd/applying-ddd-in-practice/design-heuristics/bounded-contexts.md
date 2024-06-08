---
sidebar_position: 1
---

# Bounded Contexts

As you’ll recall from Chapter 3,  
Both wide and narrow boundaries could fit the definition of a valid bounded context encompassing a consistent ubiquitous language.

But still, what is the optimal size of a bounded context?  
This question is especially important in light of the frequent equation of bounded contexts with microservices.

Should we always strive for the smallest possible bounded contexts?  
As my friend Nick Tune says:

> There are many useful and revealing heuristics for defining the boundaries of a service.  
> Size is one of the least useful.

Rather than making the model a function of the desired size (optimizing for small bounded contexts),  
It’s much more effective to do the opposite:  
Treat the bounded context’s size as a function of the model it encompasses.

Software changes affecting multiple bounded contexts are expensive and require lots of coordination,  
Especially if the affected bounded contexts are implemented by different teams.

Such changes that are not encapsulated in a single bounded context signal ineffective design of the contexts boundaries.

Unfortunately, refactoring bounded context boundaries is an expensive undertaking,  
And in many cases, the ineffective boundaries remain unattended and end up accumulating technical debt.

Changes that invalidate the bounded contexts’ boundaries typically occur,  
When the business domain is not well known,  
Or the business requirements change frequently.

As you learned in Chapter 1, both volatility and uncertainty are the properties of core subdomains,  
Especially at the early stages of implementation.  
We can use it as a heuristic for designing bounded context boundaries.

Broad bounded context boundaries,  
Or those that encompass multiple subdomains,  
Make it safer to be wrong about the boundaries or the models of the included subdomains.

Refactoring logical boundaries is considerably less expensive than refactoring physical boundaries.

Hence, when designing bounded contexts, start with wider boundaries.  
If required, decompose the wide boundaries into smaller ones as you gain domain knowledge.

This heuristic applies mainly to bounded contexts encompassing core subdomains,  
As both generic and supporting subdomains are more formularized and much less volatile.

When creating a bounded context that contains a core subdomain,  
You can protect yourself against unforeseen changes,  
By including other subdomains that the core subdomain interacts with most often.

This can be other core subdomains, or even supporting and generic subdomains.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
