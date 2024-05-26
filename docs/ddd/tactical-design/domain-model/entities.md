---
sidebar_position: 2
---

# Entities

## What is a Entity?

An entity is the opposite of a value object.

## What is The Difference Between Entity and Value Object?

### Identification

An entity requires an explicit identification field to distinguish between the different instances of the entity.

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
`Name` (a value object).

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

In the preceding code, we introduced the identification field `Id` of type `PersonId`.

`PersonId` is a value object, and it can use any underlying data types that fit the business domain’s needs.  
For example, The `Id` can be a GUID, a number, a string, or a domain-specific value such as a Social Security number.

The central requirement for the identification field is that it should be unique for each instance of the entity, for each person, in our case.

Except for very rare exceptions,  
The value of an entity’s identification field should remain immutable throughout the entity’s lifecycle.

### Mutability

The second conceptual difference between value objects and entities is mutability.  
Contrary to value objects, entities are not immutable and are expected to change.

### Roles

Another difference between entities and value objects is that value objects describe an entity’s properties.

Earlier you saw an example of the entity `Person`,  
And it had two value objects describing each instance:  
`PersonId` and `Name`.

## What is The Relation Between Entity and Domain Model Pattern?

Entities are an essential building block of any business domain.

That said, you may have noticed that entity was'nt included in the list of the domain model’s building blocks.  
That’s not a mistake.

The reason entity was omitted is because we don’t implement entities independently,  
But only in the context of the **Aggregate Pattern**.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
