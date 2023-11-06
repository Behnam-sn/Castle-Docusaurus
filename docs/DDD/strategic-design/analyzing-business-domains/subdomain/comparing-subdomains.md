---
sidebar_position: 2
---

# Comparing Subdomains

Now that we have a greater understanding of the three types of business subdomains,  
let’s explore their differences from additional angles and see how they affect strategic software design decisions.

## Competitive Advantage

- **Core Subdomains**  
  Only core subdomains provide a competitive advantage to a company.  
  Core subdomains are the company’s strategy for differentiating itself from its competitors.

- **Generic Subdomains**  
  Generic subdomains, by definition, cannot be a source for any competitive advantage.  
  These are generic solutions the same solutions used by the company and its competitors.

- **Supporting Subdomains**  
  Supporting subdomains have low entry barriers and cannot provide a competitive advantage either.  
  Usually, a company wouldn’t mind its competitors copying its supporting subdomains this won’t affect its competitiveness in the industry.  
  On the contrary, strategically the company would prefer its supporting subdomains to be generic, ready-made solutions, thus eliminating the need to design and build their implementation.

The more complex the problems a company is able to tackle, the more business value it can provide.  
The complex problems are not limited to delivering services to consumers.

A complex problem can be, for example, making the business more optimized and efficient.  
Or, providing the same level of service as competitors do, but at lower operational costs, is a competitive advantage as well.

## Complexity

From a more technical perspective, it’s important to identify the organization’s subdomains,  
because the different types of subdomains have different levels of complexity.

- **Core Subdomains**  
  Core subdomains are complex.  
  They should be as hard for competitors to copy as possible the company’s profitability depends on it.  
  That’s why strategically, companies are looking to solve complex problems as their core subdomains.

- **Generic Subdomains**  
  Generic subdomains are complicated.  
  There should be a good reason why others have already invested time and effort in solving these problems.  
  These solutions are neither simple nor trivial.  
  Consider, for example, encryption algorithms or authentication mechanisms.

  From a knowledge availability perspective, generic subdomains are “known unknowns.”
  These are the things that you know you don’t know. Furthermore, this knowledge is readily available.  
  You can either use industry-accepted best practices or, if needed, hire a consultant specializing in the area to help design a custom solution.

- **Supporting Subdomains**  
  Supporting subdomains are simple.  
  These are basic ETL operations and CRUD interfaces, and the business logic is obvious.  
  Often, it doesn’t go beyond validating inputs or converting data from one structure to another.

At times it may be challenging to differentiate between core and supporting subdomains.  
Complexity is a useful guiding principle.

Ask whether the subdomain in question can be turned into a side business.  
Would someone pay for it on its own?  
If so, this is a core subdomain.

Similar reasoning applies for differentiating supporting and generic subdomains:  
would it be simpler and cheaper to hack your own implementation, rather than integrating an external one?  
If so, this is a supporting subdomain.

:::tip Note
From a more technical perspective,  
it’s important to identify the core subdomains whose complexity will affect software design.

As we discussed earlier, a core subdomain is not necessarily related to software.  
Another useful guiding principle for identifying software related core subdomains is to evaluate the complexity of the business logic that you will have to model and implement in code.  
Does the business logic resemble CRUD interfaces for data entry,  
or do you have to implement complex algorithms or business processes orchestrated by complex business rules and invariants?
In the former case, it’s a sign of a supporting subdomain, while the latter is a typical core subdomain.
:::

When designing software, we have to choose tools and techniques that accommodate the complexity of the business requirements.  
Therefore, identifying subdomains is essential for designing a sound software solution.
