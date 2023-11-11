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

Let’s look at 2 DDD patterns suitable for cooperating teams.

### Customer–Supplier

The second group of collaboration patterns we’ll examine is the customer–supplier patterns.

One of the bounded contexts (the supplier) provides a service for its customers.  
The service provider is “upstream” and the customer or consumer is “downstream.”

Unlike in the cooperation case, both teams (upstream and downstream) can succeed independently.  
Consequently, in most cases we have an imbalance of power:  
Either the upstream or the downstream team can dictate the integration contract.

This section will discuss 3 patterns addressing such power differences:

Conformist pattern  
Anticorruption layer pattern  
Open-host service pattern

### Separate Ways

The last collaboration option is not to collaborate at all.  
This pattern can arise for different reasons, in cases where the teams are unwilling or unable to collaborate.  
We’ll look at a few of them here.

#### Communication Issues

A common reason for avoiding collaboration is communication difficulties driven by the organization’s size or internal politics.
When teams have a hard time collaborating and agreeing, it may be more cost-effective to go their separate ways and duplicate functionality in multiple bounded contexts.

#### Generic Subdomains

The nature of the duplicated subdomain can also be a reason for teams to go their separate ways.
When the subdomain in question is generic, and if the generic solution is easy to integrate, it may be more cost-effective to integrate it locally in each bounded context.
An example is a logging framework; it would make little sense for one of the bounded contexts to expose it as a service.
The added complexity of integrating such a solution would outweigh the benefit of not duplicating the functionality in
multiple contexts.
Duplicating the functionality would be less expensive than collaborating.
expensive than duplicating the functionality.
In such a case, it is again more cost effective for the teams to go their separate ways.

:::danger
The separate ways pattern should be avoided when integrating core subdomains.  
Duplicating the implementation of such subdomains would defy the company’s strategy to implement them in the most
effective and optimized way.
:::
