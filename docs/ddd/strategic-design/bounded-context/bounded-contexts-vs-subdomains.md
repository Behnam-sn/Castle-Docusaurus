---
sidebar_position: 4
---

# Bounded Contexts Vs Subdomains

A business domain consists of multiple subdomains.  
So far, We explored the notion of decomposing a business domain into a set of fine-grained problem domains or bounded contexts.

At first, the two methods of decomposing business domains might seem redundant.  
However, that’s not the case.

Let’s examine why we need both boundaries:

**Subdomains**  
To comprehend a company’s business strategy, we have to analyze its business domain.

According to domain-driven design methodology,  
The analysis phase involves identifying the different subdomains (core, supporting, and generic).  
That’s how the organization works and plans its competitive strategy.

As you learned, a subdomain resembles a set of interrelated use cases.  
The use cases are defined by the business domain and the system’s requirements.

As software engineers, we do not define the requirements.  
That’s the responsibility of the business.  
Instead, we are analyzing the business domain to identify the subdomains.

**Bounded Contexts**  
Bounded contexts, on the other hand, are designed.  
Choosing models’ boundaries is a strategic design decision.  
We decide how to divide the business domain into smaller, manageable problem domains.

## The Interplay Between Subdomains and Bounded Contexts

Theoretically, though impractically, a single model could span the entire business domain.  
This strategy could work for a small system.

When conflicting models arise, we can follow the domain experts’ mental models and decompose the systems into bounded contexts.

If the models are still large and hard to maintain, we can decompose them into even smaller bounded contexts;  
for example, by having a bounded context for each subdomain.

Either way, this is a design decision. We design those boundaries as a part of the solution.

Having a one-to-one relationship between bounded contexts and subdomains can be perfectly reasonable in some scenarios.  
In others, however, different decomposition strategies can be more suitable.

It’s crucial to remember that subdomains are discovered and bounded contexts are designed.
The subdomains are defined by the business strategy.  
However, we can design the software solution and its bounded contexts to address the specific project’s context and constraints.

Finally, as you learned, a model is intended to solve a specific problem.  
In some cases, it can be beneficial to use multiple models of the same concept simultaneously to solve different problems.  
As different types of maps provide different types of information about our planet, it may be reasonable to use different models of the same subdomain to solve different problems.  
Limiting the design to one-to-one relationships between bounded contexts would inhibit this flexibility and force us to use a single model of a subdomain in its bounded context.
