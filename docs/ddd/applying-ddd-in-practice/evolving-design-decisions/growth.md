---
sidebar_position: 6
---

# Growth

Growth is a sign of a healthy system.

When new functionality is continuously added,  
It’s a sign that the system is successful.

It means it brings value to its users,  
And is expanded to further address users needs,  
And keep up with competing products.

But growth has a dark side.

As a software project grows,  
Its codebase can grow into a big ball of mud:

> A big ball of mud is a haphazardly structured, sprawling, sloppy, duct-tape and baling-wire, spaghetti-code jungle.  
> These systems show unmistakable signs of unregulated growth, and repeated, expedient repair.  
> — Brian Foote and Joseph Yoder

The unregulated growth that leads to big balls of mud,  
Results from extending a software system’s functionality without re-evaluating its design decisions.

Growth blows up the components’ boundaries,  
Increasingly extending their functionality.

It’s crucial to examine the effects of growth on design decisions,  
Especially since many domain-driven design tools are all about setting boundaries:

- Business building blocks (subdomains)
- Model (bounded contexts)
- Immutability (value objects)
- Consistency (aggregates)

The guiding principle for dealing with growth-driven complexity is to identify and eliminate accidental complexity:  
The complexity caused by outdated design decisions.

The essential complexity,  
Or inherent complexity of the business domain,  
Should be managed using domain-driven design tools and practices.

When we discuss DDD in earlier chapters,  
We follow the process of first analyzing the business domain and its strategic components,  
Designing the relevant models of the business domain,  
And then designing and implementing the models in code.

Let’s follow the same script for dealing with growth-driven complexity.

## Subdomains

the subdomains’ boundaries can be challenging to identify,  
And as a result, instead of striving for boundaries that are perfect,  
We must strive for boundaries that are useful.

That is, the subdomains should allow us to identify components of different business value,  
And use the appropriate tools to design and implement the solution.

As the business domain grows,  
The subdomains’ boundaries can become even more blurred,  
Making it harder to identify cases of a subdomain spanning multiple, finer-grained subdomains.

Hence, it’s important to revisit the identified subdomains,  
And follow the heuristic of coherent use cases (sets of use cases working on the same set of data) to try to identify where to split a subdomain.

If you are able to identify finer-grained subdomains of different types,  
This is an important insight that will allow you to manage the business domain’s essential complexity.

The more precise the information about the subdomains and their types is,  
The more effective you will be at choosing technical solutions for each subdomain.

Identifying inner subdomains that can be extracted and made explicit is especially important for core subdomains.  
We should always aim to distill core subdomains as much as possible from all others so that we can invest our effort where it matters most from a business strategy perspective.

## Bounded Contexts

you learned that the bounded context pattern allows us to use different models of the business domain.

Instead of building a “jack of all trades, master of none” model,  
we can build multiple models,  
Each focused on solving a specific problem.

As a project evolves and grows,  
It’s not uncommon for the bounded contexts to lose their focus and accumulate logic related to different problems.  
That’s accidental complexity.

As with subdomains,  
It’s crucial to revisit the bounded contexts’ boundaries from time to time.

Always look for opportunities to simplify the models,  
By extracting bounded contexts that are laser focused at solving specific problems.

Growth can also make existing implicit design issues explicit.  
For example, you may notice that a number of bounded contexts become increasingly “chatty” over time,  
Unable to complete any operation without calling another bounded context.

That can be a strong signal of an ineffective model,  
And should be addressed by redesigning the bounded contexts’ boundaries to increase their autonomy.

## Aggregates

When we discussed the domain model pattern,  
We used the following guiding principle for designing aggregates’ boundaries:

> The rule of thumb is to keep the aggregates as small as possible,  
> And include only objects that are required to be in a strongly consistent state by the business domain.

As the system’s business requirements grow,  
It can be “convenient” to distribute the new functionalities among the existing aggregates,  
Without revisiting the principle of keeping aggregates small.

If an aggregate grows to include data that is not needed to be strongly consistent by all of its business logic, again, that’s accidental complexity
that has to be eliminated.

Extracting business functionality into a dedicated aggregate not only simplifies the
original aggregate, but potentially can simplify the bounded context it belongs to.
Often, such refactoring uncovers an additional hidden model that, once made
explicit, should be extracted into a different bounded context.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
