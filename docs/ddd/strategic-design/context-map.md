---
sidebar_position: 8
---

# Context Map

After analyzing the integration patterns between a system’s bounded contexts, we can plot them on a context map.

The context map is a visual representation of the system’s bounded contexts and the integrations between them.  
This visual notation gives valuable strategic insight on multiple levels:

- **High-level design**

  A context map provides an overview of the system’s components and the models they implement.

- **Communication patterns**

  A context map depicts the communication patterns among teams—for example, which teams are collaborating and which prefer “less intimate” integration patterns, such as the anticorruption layer and separate ways patterns.

- **Organizational issues**

  A context map can give insight into organizational issues.  
  For example, what does it mean if a certain upstream team’s downstream consumers all resort to implementing an anticorruption layer, or if all implementations of the separate ways pattern are concentrated around the same team?

## Maintenance

Ideally, a context map should be introduced into a project right from the get-go, and be updated to reflect additions of new bounded contexts and modifications to the existing one.

Since the context map potentially contains information originating from the work of multiple teams, it’s best to define the maintenance of the context map as a shared effort: each team is responsible for updating its own integrations with other bounded contexts.

A context map can be managed and maintained as code, using a tool like Context Mapper.

## Limitations

It’s important to note that charting a context map can be a challenging task.  
When a system’s bounded contexts encompass multiple subdomains, there can be multiple integration patterns at play.

For example, two bounded contexts with two integration patterns:  
partnership and anticorruption layer.

Moreover, even if bounded contexts are limited to a single subdomain, there still can be multiple integration patterns at play—for example, if the subdomains’ modules require different integration strategies.
