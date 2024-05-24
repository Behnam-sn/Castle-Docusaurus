# Domain Model

## What is Domain Model Pattern?

The domain model pattern is intended to cope with cases of complex business logic.

Here, instead of CRUD interfaces, we deal with:  
Complicated state transitions,  
Business rules,  
And invariants (Rules that have to be protected at all times).

A domain model is an object model of the domain that incorporates both behavior and data.  
DDD’s tactical patterns—aggregates, value objects, domain events, and domain services—are the building blocks of such an object model.

All of these patterns share a common theme: they put the business logic first.  
Let’s see how the domain model addresses different design concerns.

### Complexity

The domain’s business logic is already inherently complex, so the objects used for modeling it should not introduce any additional accidental complexities.  
The model should be devoid of any infrastructural or technological concerns, such as implementing calls to databases or other external components of the system.  
This restriction requires the model’s objects to be plain old objects, objects implementing business logic without relying on or directly incorporating any infrastructural components or frameworks.

### Ubiquitous language

The emphasis on business logic instead of technical concerns makes it easier for the domain model’s objects to follow the terminology of the bounded context’s ubiquitous language.  
In other words, this pattern allows the code to “speak” the ubiquitous language and to follow the domain experts’ mental models.

## Building Blocks

Let’s look at the central domain model building blocks, or tactical patterns, offered by DDD:

- value objects
- aggregates
- domain services
