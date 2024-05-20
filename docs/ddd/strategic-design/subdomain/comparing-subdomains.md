---
sidebar_position: 4
---

# Comparing Subdomains

Now that we have a greater understanding of the 3 types of business subdomains,  
Let’s see their differences from different angles and see how they affect strategic software design decisions.

## The Subdomains Comparison Table

| Subdomain Type | Competitive Advantage | Complexity | Volatility |   Implementation   |   Problem   |
| :------------: | :-------------------: | :--------: | :--------: | :----------------: | :---------: |
|      Core      |          Yes          |    High    |    High    |      In-house      | Interesting |
|    Generic     |          No           |    High    |    Low     |     Buy/Adopt      |   Solved    |
|   Supporting   |          No           |    Low     |    Low     | In-house/Outsource |   Obvious   |

## Which Subdomain is More Important?

Core subdomains provide the company its ability to compete with other players in the industry.  
That’s a business-critical responsibility,  
But does it mean that supporting and generic subdomains are not important? of course not.

All subdomains are required for the company to work in its business domain.  
The subdomains are like foundational building blocks,  
Take one away and the whole structure may fall down.

That said, we can leverage the inherent properties of the different types of subdomains to choose implementation strategies to implement each type of subdomain in the most efficient manner.

## How To Distinguish Subdomains From Each Other?

At times it may be challenging to differentiate between core and supporting subdomains;  
Complexity is a useful guiding principle.

Ask whether the subdomain in question can be turned into a side business?  
Would someone pay for it on its own?  
If so, this is a core subdomain.

Similar reasoning applies for differentiating supporting and generic subdomains:  
would it be simpler and cheaper to hack your own implementation, rather than integrating an external one?  
If so, this is a supporting subdomain.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
