---
sidebar_position: 1
---

# Partnership Pattern

In the partnership model,  
The integration between bounded contexts is coordinated in an ad hoc manner.  
One team can notify a second team about a change in the API,  
And the second team will cooperate and adapt (no drama or conflicts).

The coordination of integration here is two-way.  
No one team dictates the language that is used for defining the contracts.  
The teams can work out the differences and choose the most appropriate solution.  
Also, both sides cooperate in solving any integration issues that might come up.  
Neither team is interested in blocking the other one.

Well-established collaboration practices, high levels of commitment, and frequent synchronizations between teams are required for successful integration in this manner.

From a technical perspective, continuous integration of the changes applied by both teams is needed to further minimize the integration feedback loop.

:::warning

This pattern might not be a good fit for geographically distributed teams since it may present synchronization and communication challenges.

:::
