---
sidebar_position: 2
---

# Entities

## What is a Entity?

An _entity_ is the opposite of a value object.

It requires an explicit identification field to distinguish between the different instances of the entity.

### Identification

A trivial example of an entity is a person.  
Consider the following class:

```cs
class Person
{
    public Name Name { get; set; }

    public Person(Name name)
    {
        this.Name = name;
    }
}
```

The class contains only one field: Name (a value object).

This design, however, is sub-optimal  
because different people can be namesakes and can have exactly the same names.

That, of course, doesn’t make them the same person.  
Hence, an identification field is needed to properly identify people:

```cs
class Person
{
    public readonly PersonId Id;
    public Name Name { get; set; }

    public Person(PersonId id, Name name)
    {
        this.Id = id;
        this.Name = name;
    }
}
```

In the preceding code, we introduced the identification field Id of type `PersonId`.

`PersonId` is a value object, and it can use any underlying data types that fit the business domain’s needs.  
For example, The `Id` can be a GUID, a number, a string, or a domain-specific value such as a Social Security number.

The central requirement for the identification field is that it should be unique for each instance of the entity,  
For each person, in our case.

Furthermore, except for very rare exceptions, the value of an entity’s identification field should remain immutable throughout the entity’s lifecycle.

### Mutability

The second conceptual difference between value objects and entities.  
Contrary to value objects, entities are not immutable and are expected to change.

### Entities & Value Objects

Another difference between entities and value objects is that value objects describe an entity’s properties.

## Entities & Domain Model

Entities are an essential building block of any business domain.

That said, you may have noticed that _entity_ was'nt included in the list of the domain model’s building blocks.  
That’s not a mistake.

The reason _entity_ was omitted is because we don’t implement entities independently,  
But only in the context of the **aggregate pattern**.
