---
sidebar_position: 1
---

# Conformist Pattern

## What is The Conformist Pattern?

In some cases,  
The balance of power favors the upstream team,  
Which has no real motivation to support its clients’ needs.

Instead,  
It just provides the integration contract,  
Defined according to its own model (take it or leave it).

## When to use Conformist Pattern?

Such power imbalances can be caused by integration with service providers that are external to the organization or simply by organizational politics.

If the downstream team can accept the upstream team’s model,  
The bounded contexts’ relationship is called conformist.

The downstream conforms to the upstream bounded context’s model.

## Why use Conformist Pattern?

The downstream team’s decision to give up some of its autonomy can be justified in multiple ways.  
For example,  
The contract exposed by the upstream team may be an industry-standard,  
Well-established model,  
Or it may just be good enough for the downstream team’s needs.

The anticorruption layer pattern addresses the case in which a consumer is not willing to accept the supplier’s model.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
