---
sidebar_position: 4
---

# Comparing Subdomains

Now that we have a greater understanding of the three types of business subdomains,  
let’s explore their differences from additional angles and see how they affect strategic software design decisions.

| Subdomain type | Competitive advantage | Complexity | Volatility |   Implementation   |   Problem   |
| :------------: | :-------------------: | :--------: | :--------: | :----------------: | :---------: |
|      Core      |          Yes          |    High    |    High    |      In-house      | Interesting |
|    Generic     |          No           |    High    |    Low     |     Buy/Adopt      |   Solved    |
|   Supporting   |          No           |    Low     |    Low     | In-house/Outsource |   Obvious   |

## Subdomains Importance

Core subdomains provide the company its ability to compete with other players in the industry.  
That’s a business-critical responsibility,  
but does it mean that supporting and generic subdomains are not important? Of course not.

All subdomains are required for the company to work in its business domain.  
The subdomains are like foundational building blocks: take one away and the whole structure may fall down.

That said, we can leverage the inherent properties of the different types of subdomains to choose implementation strategies to implement each type of subdomain in the most efficient manner.

From a more technical perspective,  
it’s important to identify the core subdomains whose complexity will affect software design.  
because when we are designing the software,  
we have to choose tools and techniques that accommodate the complexity of the business requirements.

## How differentiate Subdomains?

As we discussed earlier, a core subdomain is not necessarily related to software.  
Another useful guiding principle for identifying software related core subdomains is to evaluate the complexity of the business logic that you will have to model and implement in code.  
Does the business logic resemble CRUD interfaces for data entry,  
or do you have to implement complex algorithms or business processes orchestrated by complex business rules and invariants?
In the former case, it’s a sign of a supporting subdomain, while the latter is a typical core subdomain.

At times it may be challenging to differentiate between core and supporting subdomains.  
Complexity is a useful guiding principle.

Ask whether the subdomain in question can be turned into a side business.  
Would someone pay for it on its own?  
If so, this is a core subdomain.

Similar reasoning applies for differentiating supporting and generic subdomains:  
would it be simpler and cheaper to hack your own implementation, rather than integrating an external one?  
If so, this is a supporting subdomain.
