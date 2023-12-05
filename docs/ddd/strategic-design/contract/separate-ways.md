---
sidebar_position: 3
---

# Separate Ways

## What is Separate Ways Pattern?

The last collaboration option is not to collaborate at all.

This pattern can arise for different reasons,  
In cases where the teams are unwilling or unable to collaborate.  
Or it’s less expensive to duplicate particular functionality than to collaborate and integrate it.

## When to Use Separate Ways Pattern?

### Communication Issues

A common reason for avoiding collaboration is communication difficulties driven by the organization’s size or internal politics.  
When teams have a hard time collaborating and agreeing,  
It may be more cost-effective to go their separate ways and duplicate functionality in multiple bounded contexts.

### Generic Subdomains

The nature of the duplicated subdomain can also be a reason for teams to go their separate ways.

When the subdomain in question is generic,  
And if the generic solution is easy to integrate,  
It may be more cost-effective to integrate it locally in each bounded context.

An example is a logging framework.  
It would make little sense for one of the bounded contexts to expose it as a service.

The added complexity of integrating such a solution  
Would outweigh the benefit of not duplicating the functionality in multiple contexts.

Duplicating the functionality would be less expensive than collaborating.

### Model Differences

Differences in the bounded contexts’ models can also be a reason to go with a separate ways collaboration.

The models may be so different that a conformist relationship is impossible,  
And implementing an anticorruption layer would be more expensive than duplicating the functionality.

In such a case, it is again more cost-effective for the teams to go their separate ways.

## When not to Use Separate Ways Pattern?

The separate ways pattern should be avoided when integrating core subdomains.

Duplicating the implementation of such subdomains would defy the company’s strategy to implement them in the most effective and optimized way.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
