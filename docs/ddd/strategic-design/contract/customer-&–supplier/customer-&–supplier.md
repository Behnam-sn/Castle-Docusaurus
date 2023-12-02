---
sidebar_position: 2
---

# Customer & Supplier

## What are Customer & Supplier Patterns?

One of the bounded contexts (the supplier) provides a service for its customers.

The service provider is “upstream” and the customer or consumer is “downstream.”

Unlike in the cooperation case, both teams (upstream and downstream) can succeed independently.

Consequently, in most cases we have an imbalance of power:  
Either the upstream or the downstream team can dictate the integration contract.

## Types of Customer & Supplier Patterns

These 3 patterns will address such power differences:

- ### Conformist

  The consumer conforms to the service provider’s model.

- ### Anticorruption Layer

  The consumer translates the service provider’s model into a model that fits the consumer’s needs.

- ### Open-Host Service

  The service provider implements a published language.  
  A model optimized for its consumers’ needs.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
