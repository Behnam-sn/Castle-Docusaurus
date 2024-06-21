---
sidebar_position: 2
---

# Entity

## What is an Entity?

## What is the Difference Between Entity & Value Object?

### Identification

An entity requires an explicit identification field,  
To distinguish between the different instances of the entity.

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

The class contains only one field:  
`Name` (a value object)

However, This design is sub-optimal;  
Because different people can have exactly the same names.

But that doesn’t make them the same person.  
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

In the preceding code,  
We introduced the identification field `Id` of type `PersonId`.

`PersonId` is a value object,  
And it can use any underlying data types that fit the business domain’s needs.

For example,  
The `Id` can be a GUID, a number, a string, or a domain-specific value such as a Social Security number.

The central requirement for the identification field,  
Is that it should be unique for each instance of the entity.  
(For each person, in our case)

:::note
Except for very rare exceptions,  
The value of an entity’s identification field should remain immutable throughout the entity’s lifecycle.
:::

### Mutability

The second conceptual difference between value objects and entities is mutability.

Contrary to value objects,  
Entities are not immutable and are expected to change.

### Roles

Another difference between entities and value objects,  
Is that value objects describe an entity’s properties.

Earlier you saw an example of the entity `Person`,  
And it had two value objects describing each instance:  
`PersonId` and `Name`.

## How to Implement an Entity?

Entities are an essential building block of any business domain.

But we don’t implement entities independently,  
Instead we do in the context of the **Aggregate Pattern**.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
