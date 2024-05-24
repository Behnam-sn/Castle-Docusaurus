---
sidebar_position: 2
---

# Tactical Design

## What is Tactical Design?

The second stage of a DDD-based project is **Tactical Design**.  
Where we transform the discoveries of strategic design into software architecture and implementation.

In strategic design, we discussed the “what” and “why” of software.  
You learned to analyze business domains, identify subdomains and their strategic value,  
And turn the knowledge of business domains into the design of bounded contexts.

In tactical design, we will turn from strategy to tactics: the “how” of software design.

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

- ### Transaction Script

  This pattern organizes the system’s operations as simple, straightforward procedural scripts.  
  The procedures ensure that each operation is transactional (either it succeeds or it fails).  
  The transaction script pattern lends itself to supporting subdomains, with business logic resembling simple, ETL-like operations.

- ### Active Record

  When the business logic is simple but operates on complicated data structures,  
  You can implement those data structures as active records.  
  An active record object is a data structure that provides simple CRUD data access methods.

- ### Domain Model Pattern

  DDD’s way of implementing complex business logic

- ### Events

  You will learn to expand the domain model pattern by modeling the dimension of time.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
