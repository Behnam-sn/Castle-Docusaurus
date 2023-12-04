---
sidebar_position: 1
---

# Partnership Pattern

## What is The Partnership Pattern?

In the partnership model,  
The integration between bounded contexts is coordinated in an ad hoc manner.

## How to Use Partnership Pattern?

One team can notify a second team about a change in the API.  
And the second team will cooperate and adapt (no drama or conflicts).

The coordination of integration here is two-way.  
No one team dictates the language that is used for defining the contracts.

The teams can work out the differences and choose the most appropriate solution.  
Also, both sides cooperate in solving any integration issues that might come up.  
Neither team is interested in blocking the other one.

## When to Use Partnership Pattern?

Well-established collaboration practices,  
High levels of commitment,  
And frequent synchronizations between teams,  
Are required for successful integration in this manner.

From a technical perspective,  
Continuous integration of the changes applied by both teams is needed to further minimize the integration feedback loop.

This pattern might not be a good fit for geographically distributed teams since it may present synchronization and communication challenges.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
