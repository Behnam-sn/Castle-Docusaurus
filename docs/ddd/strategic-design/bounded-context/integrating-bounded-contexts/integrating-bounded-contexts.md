# Integrating Bounded Contexts

## Introduction

Models in different bounded contexts can be evolved and implemented independently.  
That said, bounded contexts themselves are not independent.

A system cannot be built out of independent components.  
The components have to interact with one another to achieve the system’s overarching goals.

Implementations in bounded contexts can evolve independently, but they have to integrate with one another.  
As a result, there will always be touch-points between bounded contexts.  
These are called **contracts**.

## Why Do We Need Contracts?

The need for contracts results from differences in bounded contexts’ models and languages.

Since each contract affects more than one party, they need to be defined and coordinated.

Also, by definition, two bounded contexts are using different ubiquitous languages.  
Which language will be used for integration purposes?

These integration concerns should be evaluated and addressed by the solution’s design.

## Integration Patterns in DDD

Domain-driven design has multiple patterns for defining relationships and integrations between bounded contexts.

These patterns are driven by the nature of collaboration between teams working on bounded contexts.  
We will divide the patterns into 3 groups, each representing a type of team collaboration:

### Cooperation

Cooperation patterns relate to bounded contexts implemented by teams with well established communication.

In the simplest case, these are bounded contexts implemented by a single team.  
This also applies to teams with dependent goals, where one team’s success depends on the success of the other, and vice versa.

Again, the main criterion here is the quality of the teams’ communication and collaboration.

Let’s look at 2 DDD patterns suitable for cooperating teams:

- **Partnership**  
  Bounded contexts are integrated in an ad hoc manner.

- **Shared Kernel**  
  Two or more bounded contexts are integrated by sharing a limited overlapping model that belongs to all participating bounded contexts.

### Customer–Supplier

One of the bounded contexts (the supplier) provides a service for its customers.  
The service provider is “upstream” and the customer or consumer is “downstream.”

Unlike in the cooperation case, both teams (upstream and downstream) can succeed independently.

Consequently, in most cases we have an imbalance of power:  
Either the upstream or the downstream team can dictate the integration contract.

These 3 patterns will address such power differences:

- **Conformist**  
  The consumer conforms to the service provider’s model.

- **Anticorruption Layer**  
  The consumer translates the service provider’s model into a model that fits the consumer’s needs.

- **Open-Host Service**  
  The service provider implements a published language—a model optimized for its consumers’ needs.

### Separate Ways

It’s less expensive to duplicate particular functionality than to collaborate and integrate it.
