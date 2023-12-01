---
sidebar_position: 5
---

# Types of Boundaries

As Ruth Malan says, architectural design is inherently about boundaries:

> Architectural design is system design.  
> System design is contextual design,  
> It is inherently about boundaries (what’s in, what’s out, what spans, what moves between),  
> and about trade-offs.  
> It reshapes what is outside, just as it shapes what is inside.  
> The bounded context pattern is the domain-driven design tool for defining physical and ownership boundaries.

## Physical Boundaries

Bounded contexts serve not only as model boundaries,  
But also as physical boundaries of the systems implementing them.

Each bounded context should be implemented as an individual service/project,  
Meaning it is implemented, evolved, and versioned independently of other bounded contexts.

Clear physical boundaries between bounded contexts allow us to implement each bounded context with the technology stack that best fits its needs.

As we discussed earlier, a bounded context can contain multiple subdomains.  
In such a case, the bounded context is a physical boundary, while each of its subdomains is a logical boundary.

Logical boundaries bear different names in different programming languages: namespaces, modules, or packages.

## Ownership Boundaries

Studies show that good fences do indeed make good neighbors.

In software projects, we can leverage model boundaries (bounded contexts) for the peaceful coexistence of teams.  
The division of work between teams is another strategic decision that can be made using the bounded context pattern.

A bounded context should be implemented, evolved, and maintained by one team only.  
No two teams can work on the same bounded context.

This segregation eliminates implicit assumptions that teams might make about one another’s models.  
Instead, they have to define communication protocols for integrating their models and systems explicitly.

It’s important to note that the relationship between teams and bounded contexts is one-directional:  
A bounded context should be owned by only one team.  
However, a single team can own multiple bounded contexts.
