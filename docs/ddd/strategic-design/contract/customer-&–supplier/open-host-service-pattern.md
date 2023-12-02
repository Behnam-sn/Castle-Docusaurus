---
sidebar_position: 3
---

# Open-Host Service Pattern

## What is The Open-Host Service Pattern?

This pattern addresses cases in which the power is skewed toward the consumers.

The supplier is interested in protecting its consumers and providing the best service possible.

To protect the consumers from changes in its implementation model,  
The upstream supplier decouples the implementation model from the public interface.

This decoupling allows the supplier to evolve its implementation and public models at different rates.

The supplier’s public interface is not intended to conform to its ubiquitous language.  
Instead, it is intended to expose a protocol convenient for the consumers, expressed in an integration-oriented language.

As such, the public protocol is called the published language.

In a sense, the open-host service pattern is a reversal of the anticorruption layer pattern:  
instead of the consumer, the supplier implements the translation of its internal model.

Decoupling the bounded context’s implementation and integration models gives the upstream bounded context the freedom to evolve its implementation without affecting the downstream contexts.  
Of course, that’s only possible if the modified implementation model can be translated into the published language the consumers are already using.

Furthermore, the integration model’s decoupling allows the upstream bounded context to simultaneously expose multiple versions of the published language, allowing the consumer to migrate to the new version gradually.
