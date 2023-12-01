---
sidebar_position: 6
---

# Bounded Context

## What is a Bounded Context?

Whenever we stumble upon an inherent conflict in the domain experts’ mental models,  
We have to decompose the ubiquitous language into multiple bounded contexts.

<!-- A ubiquitous language should be consistent within the scope of its bounded context.
However, across bounded contexts, the same terms can have different meanings. -->

<!-- While subdomains are discovered, bounded contexts are designed.
The division of the domain into bounded contexts is a strategic design decision. -->

<!-- A bounded context and its ubiquitous language can be implemented and maintained by one team.
No two teams can share the work on the same bounded context.
However, one team can work on multiple bounded contexts. -->

<!-- Bounded contexts decompose a system into physical components—services, subsystems, and so on.
Each bounded context’s lifecycle is decoupled from the rest.
Each bounded context can evolve independently from the rest of the system.
However, the bounded contexts have to work together to form a system.
Some of the changes will inadvertently affect another bounded context.
In the next chapter, we’ll talk about the different patterns for integrating bounded contexts that can be used to protect them
from cascading changes. -->

## What Problem Bounded Context is Trying to Solve?

### Inconsistent Models

As you know by now, To ensure a project’s success it’s crucial that you develop a ubiquitous language that can be used for communication by all stakeholders, from software engineers to domain experts.

The language should reflect the domain experts’ mental models of the business domain’s inner workings and underlying principles.

Since our goal is to use ubiquitous language to drive software design decisions,  
the language must be clear and consistent.  
It should be free of ambiguity, implicit assumptions, and extraneous details.

However, on an organizational scale, the domain experts’ mental models can be inconsistent themselves.  
Different domain experts can use different models of the same business domain.

#### An Example of Inconsistent Models

Let’s go back to the example of a telemarketing company.  
The company’s marketing department generates leads through online advertisements.  
Its sales department is in charge of soliciting prospective customers to buy its products or services.

An examination of the domain experts’ language reveals a peculiar observation.  
The term "lead" has different meanings in the marketing and sales departments:

- **Marketing Department**  
  For the marketing people, a lead represents a notification that somebody is interested in one of the products.  
  The event of receiving the prospective customer’s contact details is considered a lead.

- **Sales Department**  
  In the context of the sales department, a lead is a much more complex entity.  
  It represents the entire lifecycle of the sales process.  
  It’s not a mere event, but a long-running process.

How do we formulate a ubiquitous language in the case of this telemarketing company?

### Over-Engineering & Under-Engineering

On the one hand, we know the ubiquitous language has to be consistent (each term should have one meaning).  
On the other hand, we know the ubiquitous language has to reflect the domain experts’ mental models.

In this case, the mental model of the “lead” is inconsistent among the domain experts in the sales and marketing departments.

This ambiguity doesn’t present that much of a challenge in person-to-person communications.  
Indeed, communication can be more challenging among people from different departments,  
But it’s easy enough for humans to infer the exact meaning from the interaction’s context.

However, it is more difficult to represent such a divergent model of the business domain in software.  
Source code doesn’t cope well with ambiguity.

If we were to bring the sales department’s complicated model into marketing,  
It would introduce complexity where it’s not needed (far more detail and behavior than marketing people need for optimizing advertising campaigns).

But if we were to try to simplify the sales model according to the marketing world view,  
It wouldn’t fit the sales subdomain’s needs,  
Because it’s too simplistic for managing and optimizing the sales process.  
We’d have an over-engineered solution in the first case and an under-engineered one in the second.

### Domain Complexity

How do we solve this catch-22?

The traditional solution to this problem is to design a single model that can be used for all kinds of problems.  
Such models result in enormous entity relationship diagrams (ERDs) spanning whole office walls.

As the saying goes, “jack of all trades, master of none”.  
Such models are supposed to be suitable for everything but eventually are effective for nothing.

No matter what you do, you are always facing complexity:  
The complexity of filtering out extraneous details,  
The complexity of finding what you do need,  
And most importantly,  
The complexity of keeping the data in a consistent state.

Another solution would be to prefix the problematic term with a definition of the context:  
“marketing lead” and “sales lead”.

That would allow the implementation of the two models in code.  
However, this approach has two main disadvantages:

1. It induces cognitive load.  
   When should each model be used?  
   The closer the implementations of the conflicting models are, the easier it is to make a mistake.

2. The implementation of the model won’t be aligned with the ubiquitous language.  
   No one would use the prefixes in conversations.  
   People don’t need this extra information.  
   They can rely on the conversation’s context.

Let’s turn to the domain-driven design pattern for tackling such scenarios:  
The bounded context pattern

## What is Bounded Context Solution?

The solution in domain-driven design is trivial:

Divide the ubiquitous language into multiple smaller languages,  
Then assign each one to the explicit context in which it can be applied:  
Its bounded context.

In a sense, terminology conflicts and implicit contexts are an inherent part of any decent-sized business.  
With the bounded context pattern, the contexts are modeled as an explicit and integral part of the business domain.

## What is an Example of a Bounded Context?

In the preceding example,  
We can identify two bounded contexts:  
Marketing and sales.

The term lead exists in both bounded contexts.  
As long as it bears a single meaning in each bounded context,  
Each fine-grained ubiquitous language is consistent and follows the domain experts’ mental models.

## Ubiquitous Language & Bounded Context

Bounded contexts allow us to complete the definition of a ubiquitous language.  
A ubiquitous language is not “ubiquitous” in the sense that it should be used and applied “ubiquitously” throughout the organization.

_A ubiquitous language is not universal._  
_Instead, a ubiquitous language is ubiquitous only in the boundaries of its bounded context._

The language is focused on describing only the model that is encompassed by the bounded context.  
As a model cannot exist without a problem it is supposed to address,  
A ubiquitous language cannot be defined or used without an explicit context of its applicability.

## Scope of a Bounded Context

Different domain experts held conflicting mental models of the same business entity.

To model the business domain,  
We had to divide the model and define a strict applicability context for each fine-grained model (its bounded context).

The consistency of the ubiquitous language only helps to identify the widest boundary of that language.  
It cannot be any larger, because then there will be inconsistent models and terminology.  
However, we can still further decompose the models into even smaller bounded contexts.

Defining the scope of a ubiquitous language (its bounded context) is a strategic design decision.  
Boundaries can be wide, following the business domain’s inherent contexts,  
Or narrow, further dividing the business domain into smaller problem domains.

A bounded context’s size, by itself, is not a deciding factor.  
Models shouldn’t necessarily be big or small.  
Models need to be useful.

The wider the boundary of the ubiquitous language is, the harder it is to keep it consistent.

It may be beneficial to divide a large ubiquitous language into smaller and more manageable problem domains,  
But striving for small bounded contexts can backfire too.  
The smaller they are, the more integration overhead the design induces.

Hence, the decision for how big your bounded contexts should depend on the specific problem domain.  
Sometimes, using a wide boundary will be clearer,  
While at other times, decomposing it further will make more sense.

The reasons for extracting finer-grained bounded contexts out of a larger one include:  
Constituting new software engineering teams  
Or addressing some of the system’s non‐functional requirements.

For example,  
When you need to separate the development lifecycles of some of the components originally residing in a single bounded context.  
Another common reason for extracting one functionality is the ability to scale it independently from the rest of the bounded context’s functionalities.

Therefore, keep your models useful and align the bounded contexts’ sizes with your business needs and organizational constraints.

One thing to beware of is splitting a coherent functionality into multiple bounded contexts.  
Such division will hinder the ability to evolve each context independently.  
Instead, the same business requirements and changes will simultaneously affect the bounded contexts and require simultaneous deployment of the changes.  
To avoid such ineffective decomposition, use the rule of thumb we discussed in Chapter 1 to find subdomains:  
Identify sets of coherent use cases that operate on the same data and avoid decomposing them into multiple bounded contexts.

## Bounded Contexts Vs Subdomains

<!-- A business domain consists of multiple subdomains. -->

So far, We explored the notion of decomposing a business domain into a set of fine-grained problem domains or bounded contexts.

At first, the two methods of decomposing business domains might seem redundant.  
However, that’s not the case.

Let’s examine why we need both boundaries:

<!-- To comprehend a company’s business strategy,
We have to analyze its business domain.

According to domain-driven design methodology,
The analysis phase involves identifying the different subdomains (core, supporting, and generic).
That’s how the organization works and plans its competitive strategy.

As you learned, a subdomain resembles a set of interrelated use cases.
The use cases are defined by the business domain and the system’s requirements. -->

- **Subdomains**  
  As software engineers, we do not define the subdomains.  
  That’s the responsibility of the business.  
  Instead, we are analyzing the business domain to identify the subdomains.

- **Bounded Contexts**  
  Bounded contexts, on the other hand, are designed.  
  Choosing models’ boundaries is a strategic design decision.  
  We decide how to divide the business domain into smaller, manageable problem domains.

## The Interplay Between Subdomains and Bounded Contexts

### Monolithic bounded context

Theoretically (though impractically), a single model could span the entire business domain.  
This strategy could work for a small system.

### Bounded contexts driven by the consistency of the ubiquitous language

When conflicting models arise,  
We can follow the domain experts’ mental models and decompose the systems into bounded contexts.

### Bounded contexts aligned with subdomains’ boundaries

If the models are still large and hard to maintain,  
We can decompose them into even smaller bounded contexts.  
For example, by having a bounded context for each subdomain.

Either way, this is a design decision.  
We design those boundaries as a part of the solution.

Having a one-to-one relationship between bounded contexts and subdomains can be perfectly reasonable in some scenarios.  
In others however, different decomposition strategies can be more suitable.

<!-- It’s crucial to remember that subdomains are discovered and bounded contexts are designed.
The subdomains are defined by the business strategy.
However, we can design the software solution and its bounded contexts to address the specific project’s context and constraints. -->

Finally, as you learned, a model is intended to solve a specific problem.  
In some cases, it can be beneficial to use multiple models of the same concept simultaneously to solve different problems.

As different types of maps provide different types of information about our planet,  
It may be reasonable to use different models of the same subdomain to solve different problems.

Limiting the design to one-to-one relationships between bounded contexts would inhibit this flexibility and force us to use a single model of a subdomain in its bounded context.
