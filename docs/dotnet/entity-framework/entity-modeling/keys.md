---
sidebar_position: 3
---

# Keys

A key serves as a unique identifier for each entity instance.  
Most entities in EF have a single key, which maps to the concept of a primary key in relational databases.

<!-- For entities without keys, see Keyless entities.
Entities can have additional keys beyond the primary key.
See Alternate Keys for more information. -->

## Configuring a Primary Key

### Conventions

By convention, a property named `Id` or `<TypeName>Id` will be configured as the primary key of an entity.

```cs
internal class Car
{
    public string Id { get; set; }
    public string Make { get; set; }
    public string Model { get; set; }
}
```

```cs
internal class Truck
{
    public string TruckId { get; set; }
    public string Make { get; set; }
    public string Model { get; set; }
}
```

### Single Property as Key

You can configure a single property to be the primary key of an entity as follows:

**Data Annotations**

```cs
internal class Car
{
    [Key]
    public string LicensePlate { get; set; }
    public string Make { get; set; }
    public string Model { get; set; }
}
```

**Fluent API**

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Car>()
        .HasKey(c => c.LicensePlate);
}
```

### Multiple Properties as Key

You can also configure multiple properties to be the key of an entity.  
This is known as a composite key.  
Conventions will only set up a composite key in specific cases, like for an owned type collection.

**Data Annotations**

```cs
[PrimaryKey(nameof(State), nameof(LicensePlate))]
internal class Car
{
    public string State { get; set; }
    public string LicensePlate { get; set; }
    public string Make { get; set; }
    public string Model { get; set; }
}
```

**Fluent API**

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Car>()
        .HasKey(c => new { c.State, c.LicensePlate });
}
```

## Value Generation

For non-composite numeric and GUID primary keys, EF Core sets up value generation for you by convention.  
For example, a numeric primary key in SQL Server is automatically set up to be an `IDENTITY` column.  
For more information, see the documentation on value generation and guidance for specific inheritance mapping strategies.

## Primary Key Name

## Key Types and Values

## Alternate Keys

## References

- https://learn.microsoft.com/en-us/ef/core/modeling/keys
