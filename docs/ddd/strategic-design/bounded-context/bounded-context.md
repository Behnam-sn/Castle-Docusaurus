---
sidebar_position: 6
---

# Bounded Context

## What Is a Bounded Context?

Whenever we stumble upon an inherent conflict in the domain experts’ mental models,  
We have to decompose the ubiquitous language into multiple bounded contexts.  
A ubiquitous language should be consistent within the scope of its bounded context.  
However, across bounded contexts, the same terms can have different meanings.

While subdomains are discovered, bounded contexts are designed.  
The division of the domain into bounded contexts is a strategic design decision.

A bounded context and its ubiquitous language can be implemented and maintained by one team.  
No two teams can share the work on the same bounded context.  
However, one team can work on multiple bounded contexts.

Bounded contexts decompose a system into physical components—services, subsystems, and so on.  
Each bounded context’s lifecycle is decoupled from the rest.  
Each bounded context can evolve independently from the rest of the system.  
However, the bounded contexts have to work together to form a system.  
Some of the changes will inadvertently affect another bounded context.  
In the next chapter, we’ll talk about the different patterns for integrating bounded contexts that can be used to protect them
from cascading changes.

## What Problem Bounded Context is Trying to Solve?

To ensure a project’s success it’s crucial that you develop a ubiquitous language that can be used for communication by all stakeholders, from software engineers to domain experts.

The language should reflect the domain experts’ mental models of the business domain’s inner workings and underlying principles.

Since our goal is to use ubiquitous language to drive software design decisions,  
the language must be clear and consistent.  
It should be free of ambiguity, implicit assumptions, and extraneous details.

However, on an organizational scale, the domain experts’ mental models can be inconsistent themselves.  
Different domain experts can use different models of the same business domain.

### Inconsistent Models

Let’s go back to the example of a telemarketing company.  
The company’s marketing department generates leads through online advertisements.  
Its sales department is in charge of soliciting prospective customers to buy its products or services.

An examination of the domain experts’ language reveals a peculiar observation.  
The term lead has different meanings in the marketing and sales departments:

- **Marketing department**  
  For the marketing people, a lead represents a notification that somebody is interested in one of the products.  
  The event of receiving the prospective customer’s contact details is considered a lead.

- **Sales department**  
  In the context of the sales department, a lead is a much more complex entity.  
  It represents the entire lifecycle of the sales process.  
  It’s not a mere event, but a long-running process.

How do we formulate a ubiquitous language in the case of this telemarketing company?

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
We’d have an overengineered solution in the first case and an under-engineered one in the second.

### Managing Domain Complexity

How do we solve this catch-22?  
The traditional solution to this problem is to design a single model that can be used for all kinds of problems.  
Such models result in enormous entity relationship diagrams (ERDs) spanning whole office walls.

As the saying goes, “jack of all trades, master of none”.  
Such models are supposed to be suitable for everything but eventually are effective for nothing.

No matter what you do, you are always facing complexity:  
The complexity of filtering out extraneous details,  
The complexity of finding what you do need,  
And most importantly, the complexity of keeping the data in a consistent state.

Another solution would be to prefix the problematic term with a definition of the context:  
“marketing lead” and “sales lead.”

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
divide the ubiquitous language into multiple smaller languages,  
Then assign each one to the explicit context in which it can be applied: Its bounded context.

In a sense, terminology conflicts and implicit contexts are an inherent part of any decent-sized business.  
With the bounded context pattern, the contexts are modeled as an explicit and integral part of the business domain.
