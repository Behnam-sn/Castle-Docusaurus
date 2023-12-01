---
sidebar_position: 3
---

# Conformist Pattern

In some cases, the balance of power favors the upstream team, which has no real motivation to support its clients’ needs.

Instead, it just provides the integration contract, defined according to its own model (take it or leave it).

Such power imbalances can be caused by integration with service providers that are external to the organization or simply by organizational politics.

If the downstream team can accept the upstream team’s model, the bounded contexts’ relationship is called conformist.  
The downstream conforms to the upstream bounded context’s model.

The downstream team’s decision to give up some of its autonomy can be justified in multiple ways.  
For example, the contract exposed by the upstream team may be an industry-standard, well-established model, or it may just be good enough for the downstream team’s needs.

The next pattern addresses the case in which a consumer is not willing to accept the supplier’s model.
