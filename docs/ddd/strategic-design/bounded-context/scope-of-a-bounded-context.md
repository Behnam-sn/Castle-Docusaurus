---
sidebar_position: 3
---

# Scope of a Bounded Context

Different domain experts held conflicting mental models of the same business entity.  
To model the business domain, We had to divide the model and define a strict applicability context for each fine-grained model (its bounded context).

The consistency of the ubiquitous language only helps to identify the widest boundary of that language.  
It cannot be any larger, because then there will be inconsistent models and terminology.  
However, we can still further decompose the models into even smaller bounded contexts.

Defining the scope of a ubiquitous language (its bounded context) is a strategic design decision.  
Boundaries can be wide, following the business domain’s inherent contexts, or narrow, further dividing the business domain into smaller problem
domains.

A bounded context’s size, by itself, is not a deciding factor.  
Models shouldn’t necessarily be big or small. Models need to be useful.

The wider the boundary of the ubiquitous language is, the harder it is to keep it consistent.

It may be beneficial to divide a large ubiquitous language into smaller, more manageable problem domains, but striving for small bounded contexts can backfire too.  
The smaller they are, the more integration overhead the design induces.

Hence, the decision for how big your bounded contexts should depend on the specific problem domain.  
Sometimes, using a wide boundary will be clearer, while at other times, decomposing it further will make more sense.

The reasons for extracting finer-grained bounded contexts out of a larger one include constituting new software engineering teams or addressing some of the system’s non‐functional requirements;  
for example, when you need to separate the development lifecycles of some of the components originally residing in a single bounded context.  
Another common reason for extracting one functionality is the ability to scale it independently from the rest of the bounded context’s functionalities.

Therefore, keep your models useful and align the bounded contexts’ sizes with your business needs and organizational constraints.  
One thing to beware of is splitting a coherent functionality into multiple bounded contexts.  
Such division will hinder the ability to evolve each context independently.  
Instead, the same business requirements and changes will simultaneously affect the bounded contexts and require simultaneous deployment of the changes.  
To avoid such ineffective decomposition, use the rule of thumb we discussed in Chapter 1 to find subdomains: identify sets of coherent use
cases that operate on the same data and avoid decomposing them into multiple bounded contexts.
