---
sidebar_position: 5
---

# Model

## What is a Model?

> A model is a simplified representation of a thing or phenomenon  
> That intentionally emphasizes certain aspects while ignoring others.  
> Abstraction with a specific use in mind.  
> — Rebecca Wirfs-Brock

A model is not a copy of the real world but a human construct that helps us make sense of real-world systems.

## What is an Example of a Model?

A canonical example of a model is a map.

Any map is a model, including navigation maps, terrain maps, world maps, subway maps, and others.

None of these maps represents all the details of our planet.  
Instead, each map contains just enough data to support its particular purpose:  
The problem it is supposed to solve.

## How to Model Effectively?

A useful model is not a copy of the real world.  
Instead, a model is intended to solve a problem,  
And it should provide just enough information for that purpose.

As statistician George Box puts it:

> All models are wrong, but some are useful.

For example, you won’t see subway stops on a world map.  
On the other hand, you cannot use a subway map to estimate distances.

Each map contains just the information it is supposed to provide.

In its essence, a model is an abstraction.  
The notion of abstraction allows us to handle complexity by omitting unnecessary details and leaving only what’s needed for solving the problem at hand.  
On the other hand, an ineffective abstraction removes necessary information or produces noise by leaving what’s not required.

As noted by Edsger W. Dijkstra in his paper “The Humble Programmer":

> The purpose of abstracting is not to be vague but to create a new semantic level in which one can be absolutely precise.

## Model Boundaries

As you already know,  
A model is not a copy of the real world but a construct that helps us make sense of a complex system.  
The problem it is supposed to solve is an inherent part of a model (its purpose).

A model cannot exist without a boundary.  
It will expand to become a copy of the real world.  
That makes defining a model’s boundary (its bounded contexts) an intrinsic part of the modeling process.

Let’s go back to the example of maps as models.  
We saw that each map has its specific context (aerial, nautical, terrain, subway, and so on).  
A map is useful and consistent only within the scope of its specific purpose.

Just as a subway map is useless for nautical navigation,  
A ubiquitous language in one bounded context can be completely irrelevant to the scope of another bounded context.

Bounded contexts define the applicability of a ubiquitous language and of the model it represents.  
They allow defining distinct models according to different problem domains.

In other words, bounded contexts are the consistency boundaries of ubiquitous languages.  
A language’s terminology, principles, and business rules are only consistent inside its bounded context.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
