---
sidebar_position: 2
---

# Shared Kernel Pattern

## What is The Shared Kernel Pattern?

Despite bounded contexts being model boundaries,  
Still there can be cases when the same model of a subdomain,  
Or a part of it,  
Will be implemented in multiple bounded contexts.

It’s crucial to stress that the shared model is designed according to the needs of all of the bounded contexts.  
Moreover, the shared model has to be consistent across all of the bounded contexts that are using it.

## What is an Example of Shared Kernel Pattern?

Consider an enterprise system that uses a tailor-made model for managing users’ permissions.  
Each user can have their permissions granted directly or inherited from one of the organizational units they belong to.

Moreover, each bounded context can modify the authorization model,  
And the changes each bounded context applies have to affect all the other bounded contexts using the model.

## Shared Scope

The overlapping model couples the lifecycles of the participating bounded contexts.  
A change made to the shared model has an immediate effect on all the bounded contexts.

Hence, to minimize the cascading effects of changes,  
The overlapping model should be limited.

Exposing only that part of the model that has to be implemented by both bounded contexts.

Ideally, the shared kernel will consist only of integration contracts and data structures that are intended to be passed across the bounded contexts’ boundaries.

## How to Implement The Shared Kernel Pattern?

The shared kernel is implemented so that any modification to its source code is immediately reflected in all the bounded contexts using it.

If the organization uses the mono-repository approach,  
these can be the same source files referenced by multiple bounded contexts.

If using a shared repository is not possible,  
the shared kernel can be extracted into a dedicated project and referenced in the bounded contexts as a linked library.

Either way,  
each change to the shared kernel must trigger integration tests for all the affected bounded contexts.

The continuous integration of changes is required because the shared kernel belongs to multiple bounded contexts.

Not propagating shared kernel changes to all related bounded contexts,  
leads to inconsistencies in a model.

bounded contexts may rely on stale implementations of the shared kernel,  
leading to data corruption and/or runtime issues.

## When to Use Shared Kernel?

The overarching applicability criterion for the shared kernel pattern is the cost of duplication versus the cost of coordination.

Since the pattern introduces a strong dependency between the participating bounded contexts,  
It should be applied only when the cost of duplication is higher than the cost of coordination.

In other words,  
Only when integrating changes applied to the shared model by both bounded contexts will require more effort than coordinating the changes in the shared codebase.

The difference between the integration and duplication costs depends on the volatility of the model.  
The more frequently it changes, the higher the integration costs will be.

Therefore, the shared kernel will naturally be applied for the subdomains that change the most:  
the core subdomains

In a sense, the shared kernel pattern contradicts the principles of bounded contexts introduced.  
If the participating bounded contexts are not implemented by the same team,  
introducing a shared kernel contradicts the principle that a single team should own a bounded context.

The overlapping model (the shared kernel) is, in effect, being developed by multiple teams.

That’s the reason why the use of a shared kernel has to be justified.  
It’s a pragmatic exception that should be considered carefully.

A common use case for implementing a shared kernel is when communication or collaboration issues prevent implementing the partnership pattern.  
For example, because of geographical constraints or organizational politics.

Implementing a closely related functionality without proper coordination will result in integration issues, desynchronized models, and arguments about which model is better designed.

Minimizing the shared kernel’s scope controls the scope of cascading changes,  
And triggering integration tests for each change is a way to enforce early detection of integration issues.

Another common use case for applying the shared kernel pattern, albeit a temporary one, is the gradual modernization of a legacy system.

In such a scenario, the shared codebase can be a pragmatic intermediate solution for gradually decomposing the system into bounded contexts.

Finally, a shared kernel can be a good fit for integrating bounded contexts owned and implemented by the same team.  
In such a case, an ad hoc integration of the bounded contexts (a partnership) can “wash out” the contexts’ boundaries over time.

A shared kernel can be used for explicitly defining the bounded contexts’ integration contracts.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
