---
sidebar_position: 5
---

# Modeling

let’s look at the ubiquitous language from a different perspective: modeling.

## What Is a Model?

> A model is a simplified representation of a thing or phenomenon that intentionally emphasizes certain aspects while ignoring others. Abstraction with a specific use in mind.  
> — Rebecca Wirfs-Brock

A model is not a copy of the real world but a human construct that helps us make sense of real-world systems.

A canonical example of a model is a map.  
Any map is a model, including navigation maps, terrain maps, world maps, subway maps, and others.

None of these maps represents all the details of our planet.  
Instead, each map contains just enough data to support its particular purpose: the problem it is supposed to solve.

## Effective Modeling

All models have a purpose, and an effective model contains only the details needed to fulfill its purpose.

For example, you won’t see subway stops on a world map.  
On the other hand, you cannot use a subway map to estimate distances.

Each map contains just the information it is supposed to provide.

This point is worth reiterating:  
A useful model is not a copy of the real world.  
Instead, a model is intended to solve a problem,  
And it should provide just enough information for that purpose.

> As statistician George Box put it:  
> All models are wrong, but some are useful.

In its essence, a model is an abstraction.  
The notion of abstraction allows us to handle complexity by omitting unnecessary details and leaving only what’s needed for solving the problem at hand.  
On the other hand, an ineffective abstraction removes necessary information or produces noise by leaving what’s not required.

> As noted by Edsger W. Dijkstra in his paper “The Humble Programmer,”  
> The purpose of abstracting is not to be vague but to create a new semantic level in which one can be absolutely precise.

## Modeling the Business Domain

When cultivating a ubiquitous language, we are effectively building a model of the business domain.  
The model is supposed to capture the domain experts’ mental models—their thought processes about how the business works to implement its function.  
The model has to reflect the involved business entities and their behavior, cause and effect relationships, and invariants.

The ubiquitous language we use is not supposed to cover every possible detail of the domain.  
That would be equivalent to making every stakeholder a domain expert.  
Instead, the model is supposed to include just enough aspects of the business domain to make it possible to implement the required system.  
That is, to address the specific problem the software is intended to solve.

Effective communication between engineering teams and domain experts is vital.  
The importance of this communication grows with the complexity of the business domain.  
The more complex the business domain is, the harder it is to model and implement its business logic in code.  
Even a slight misunderstanding of a complicated business domain, or its underlying principles, will inadvertently lead to an implementation prone to severe bugs.

The only reliable way to verify a business domain’s understanding is to converse with domain experts and do it in the language they understand: the language of the business.
