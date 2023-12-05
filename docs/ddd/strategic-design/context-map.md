---
sidebar_position: 8
---

# Context Map

## What is a Context Map?

The context map is a visual representation of the system’s bounded contexts and the integrations between them.

## Why Use a Context Map?

This visual notation gives valuable strategic insight on multiple levels:

### High-level Design

A context map provides an overview of the system’s components and the models they implement.

### Communication Patterns

A context map depicts the communication patterns among teams.  
For example, which teams are collaborating and which prefer “less intimate” integration patterns,  
Such as the anticorruption layer and separate ways patterns.

### Organizational Issues

A context map can give insight into organizational issues.  
For example, what does it mean if a certain upstream team’s downstream consumers all resort to implementing an anticorruption layer,  
Or if all implementations of the separate ways pattern are concentrated around the same team?

## How to Use a Context Map?

### Initiation

Ideally, a context map should be introduced into a project right from the get-go,  
And be updated to reflect additions of new bounded contexts and modifications to the existing one.

### Maintenance

Since the context map potentially contains information originating from the work of multiple teams,  
It’s best to define the maintenance of the context map as a shared effort.  
Each team is responsible for updating its own integrations with other bounded contexts.

A context map can be managed and maintained as code, using a tool like Context Mapper.

### Limitations

It’s important to note that charting a context map can be a challenging task.

When a system’s bounded contexts encompass multiple subdomains,  
There can be multiple integration patterns at play.

For example,  
Two bounded contexts with two integration patterns:  
Partnership and Anti-Corruption layer.

Moreover, even if bounded contexts are limited to a single subdomain,  
There still can be multiple integration patterns at play.  
For example, if the subdomains’ modules require different integration strategies.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
