---
sidebar_position: 1
---

# Modeling & Bounded Context

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
