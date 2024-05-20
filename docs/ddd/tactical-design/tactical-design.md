---
sidebar_position: 2
---

# Tactical Design

## What is Tactical Design?

In strategic design, we discussed the “what” and “why” of software.  
You learned to analyze business domains, identify subdomains and their strategic value,  
And turn the knowledge of business domains into the design of bounded contexts.

In tactical design, we will turn from strategy to tactics: the “how” of software design.

The second stage of a DDD-based project is **Tactical Design**.  
Where we transform the discoveries of strategic design into software architecture and implementation.

## What Problem is Tactical Design Trying to Solve?

Business logic is the most important part of software.  
It’s the reason the software is being implemented in the first place.

A system’s UI can be beautiful and its database can be blazing fast and scalable.  
But if the software is not useful for the business, it’s nothing but an expensive technology demo.

As we saw in Strategic Design, not all business subdomains are created equal.  
Different subdomains have different levels of strategic importance and complexity.

DDD’s tactical patterns allow us to write code in a way that:  
Reflects the business domain,  
Addresses its goals,  
And speaks the language of the business.

business logic implementation patterns that allow the code to speak the ubiquitous language of its bounded context.

## What is Tactical Design Solution?

This article begins our exploration of the different ways to model and implement business logic code.

- Transaction script
- Active record
- domain model pattern : DDD’s way of implementing complex business logic
- Events: you will learn to expand the domain model pattern by modeling the dimension of time.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
