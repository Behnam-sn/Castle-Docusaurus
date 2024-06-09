---
sidebar_position: 2
---

# Strategic Design Concerns

A change in a subdomain’s type directly affects its bounded context,  
And, consequently, corresponding strategic design decisions.

As you learned different bounded context integration patterns accommodate the different subdomain types.

The core subdomains have to protect their models by using anticorruption layers,  
And have to protect consumers from frequent changes in the implementation models by using published languages (OHS).

Another integration pattern that is affected by such changes is the separate ways pattern.  
As you saw earlier, teams can use this pattern for supporting and generic subdomains.

If the subdomain morphs into a core subdomain,  
Duplicating its functionality by multiple teams is no longer acceptable.  
Hence, the teams have no choice but to integrate their implementations.  
The customer–supplier relationship will make the most sense in this case,  
Since the core subdomain will only be implemented by one team.

From an implementation strategy standpoint,  
Core and supporting subdomains differ in how they can be implemented.

Supporting subdomains can be outsourced or used as “training wheels” for new hires.

Core subdomains must be implemented in-house,  
As close as possible to the sources of domain knowledge.

Therefore, when a supporting subdomain turns into a core subdomain,  
Its implementation should be moved in-house.

The same logic works the other way around.  
If a core subdomain turns into a supporting subdomain,  
It’s possible to outsource the implementation to let the in-house R&D teams concentrate on the core subdomains.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
