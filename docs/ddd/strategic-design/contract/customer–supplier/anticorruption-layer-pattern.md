---
sidebar_position: 4
---

# Anticorruption Layer Pattern

As in the conformist pattern,  
The balance of power in this relationship is still skewed toward the upstream service.

However, in this case, the downstream bounded context is not willing to conform.  
Instead, it can translate the upstream bounded context’s model into a model tailored to its own needs via an anticorruption layer.

The anticorruption layer pattern addresses scenarios in which it is not desirable or worth the effort to conform to the supplier’s model, such as the following:

- **When the downstream bounded context contains a core subdomain**  
  A core subdomain’s model requires extra attention,  
  And adhering to the supplier’s model might impede the modeling of the problem domain.

- **When the upstream model is inefficient or inconvenient for the consumer’s needs**  
  If a bounded context conforms to a mess, it risks becoming a mess itself.  
  That is often the case when integrating with legacy systems.

- **When the supplier’s contract changes often**  
  The consumer wants to protect its model from frequent changes.  
  With an anti‐corruption layer, the changes in the supplier’s model only affect the translation mechanism.

From a modeling perspective, the translation of the supplier’s model isolates the downstream consumer from foreign concepts that are not relevant to its bounded context.  
Hence, it simplifies the consumer’s ubiquitous language and model.
