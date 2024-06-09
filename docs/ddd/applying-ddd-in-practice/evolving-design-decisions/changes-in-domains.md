---
sidebar_position: 1
---

# Changes in Domains

You’ve learned the three types of business subdomains,  
And how they are different from one another:

- Core  
  Activities the company is performing differently from its competitors to gain a competitive advantage.

- Supporting  
  Things the company is doing differently from its competitors, but that do not provide a competitive edge.

- Generic  
  Things all companies do in the same way.

In the previous chapters,  
You saw that the type of subdomain at play affects strategic and tactical design decisions:

- How to design the bounded contexts’ boundaries
- How to orchestrate integration between the contexts
- Which design patterns to use to accommodate the complexity of the business logic

To design software that is driven by the business domain’s needs,  
It’s crucial to identify the business subdomains and their types.

However, that’s not the whole story.  
It’s equally important to be alert to the evolution of the subdomains.

As an organization grows and evolves,
it’s not unusual for some of its subdomains to morph from one type to another.

Let’s look at some examples of such changes.

## Core to Generic

Imagine that an online retail company called BuyIT has been implementing its own order delivery solution.  
It developed an innovative algorithm to optimize its couriers’ delivery routes and thus is able to charge lower delivery fees than its competitors.

One day, another company, DeliverIT disrupts the delivery industry.  
It claims it has solved the “traveling salesman” problem and provides path optimization as a service.  
Not only is DeliverIT’s optimization more advanced,  
It is offered at a fraction of the price that it costs BuyIT to perform the same task.

From BuyIT’s perspective,  
Once DeliverIT’s solution became available as an off-the-shelf product,  
Its core subdomain turned into a generic subdomain.

As a result,  
The optimal solution became available to all of BuyIT’s competitors.

Without massive investments in research and development,  
BuyIT can no longer gain a competitive advantage in the path optimization subdomain.

What was previously considered a competitive advantage for BuyIT has become a commodity available to all of its competitors.

## Generic to Core

Since its inception,  
BuyIT has been using an off-the-shelf solution to manage its inventory.

However, its business intelligence reports are continuously showing inadequate predictions of its customers demands.
Consequently, BuyIT fails to replenish its stock of the most popular products,  
And is wasting warehouse real estate on the unpopular products.

After evaluating a few alternative inventory management solutions,  
BuyIT’s management team makes the strategic decision to invest in designing and building an in-house system.

This in-house solution will consider the intricacies of the products BuyIT sells and make better predictions of customers’ demands.

BuyIT’s decision to replace the off-the-shelf solution with its own implementation has turned inventory management from a generic subdomain into a core subdomain:  
Successful implementation of the functionality will provide BuyIT additional competitive advantage over its competitors.  
The competitors will remain “stuck” with the generic solution,  
And will not be able to use the advanced demand prediction algorithms invented and developed by BuyIT.

A real-life textbook example of a company turning a generic subdomain into a core subdomain is Amazon.  
Like all service providers, Amazon needed an infrastructure on which to run its services.  
The company was able to “reinvent” the way it managed its physical infrastructure,  
And later even turned it into a profitable business: Amazon Web Services.

## Supporting to Generic

BuyIT’s marketing department implements a system for managing the vendors it works with and their contracts.  
There is nothing special or complex about the system.  
It’s just some CRUD user interfaces for entering data.  
In other words, it is a typical supporting subdomain.

However, a few years after BuyIT began implementing the in-house solution,  
An open source contracts management solution came out.  
The open source project implements the same functionality as the existing solution,  
And has more advanced features, like OCR and full-text search.

These additional features had been on BuyIT’s backlog for a long time but were never prioritized because of their low business impact.  
Hence, the company decides to ditch the in-house solution in favor of integrating the open source solution.  
In doing so, the document management subdomain turns from a supporting into a generic subdomain.

## Supporting to Core

A supporting subdomain can also turn into a core subdomain.  
For example, if a company finds a way to optimize the supporting logic in such a way that it either reduces costs or generates additional profits.

The typical symptom of such a transformation is the increasing complexity of the supporting subdomain’s business logic.  
Supporting subdomains, by definition, are simple, mainly resembling CRUD interfaces or ETL processes.  
However, if the business logic becomes more complicated over time,  
There should be a reason for the additional complexity.

If it doesn’t affect the company’s profits, why would it become more complicated?  
That’s accidental business complexity.

On the other hand, if it enhances the company’s profitability,  
It’s a sign of a supporting subdomain becoming a core subdomain.

## Core to Supporting

A core subdomain can, over time, become a supporting subdomain.  
This can happen when the subdomain’s complexity isn’t justified.  
In other words, it’s not profitable.

In such cases,  
The organization may decide to cut the extraneous complexity,  
Leaving the minimum logic needed to support implementation of other subdomains.

## Generic to Supporting

Finally, for the same reason as a core subdomain, a generic subdomain can turn into a supporting one.

Going back to the example of BuyIT’s document management system,  
Assume the company has decided that the complexity of integrating the open source solution doesn’t justify the benefits and has resorted back to the in-house system.

As a result, the generic subdomain has turned into a supporting subdomain.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
