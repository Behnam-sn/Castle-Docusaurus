---
sidebar_position: 6
---

# Indexer Properties

## What are Indexer Properties?

Indexer properties are entity type properties, which are backed by an indexer in .NET entity class.  
They can be accessed using the indexer on the .NET class instances.  
It also allows you to add additional properties to the entity type without changing the CLR class.

## Configuring Indexer Properties

You can use the Fluent API to configure indexer properties.  
Once you've called the method `IndexerProperty`, you can chain any of the configuration calls you would for other properties.

In the following sample, `Blog` has an indexer defined and it will be used to create an indexer property:

```cs
internal class MyContext : DbContext
{
    public DbSet<Blog> Blogs { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Blog>().IndexerProperty<DateTime>("LastUpdated");
    }
}

public class Blog
{
    private readonly Dictionary<string, object> _data = new Dictionary<string, object>();
    public int BlogId { get; set; }

    public object this[string key]
    {
        get => _data[key];
        set => _data[key] = value;
    }
}
```

If the name supplied to the `IndexerProperty` method matches the name of an existing indexer property,  
Then the code will configure that existing property.

If the entity type has a property,  
Which is backed by a property on the entity class,  
Then an exception is thrown since indexer properties must only be accessed via the indexer.

Indexer properties can be referenced in LINQ queries via the `EF.Property` static method as shown above or by using the CLR indexer property.

## Property Bag Entity Types

Entity types that contain only indexer properties are known as property bag entity types.  
These entity types don't have shadow properties, and EF creates indexer properties instead.

Currently only `Dictionary<string, object>` is supported as a property bag entity type.  
It must be configured as a shared-type entity type with a unique name and the corresponding `DbSet` property must be implemented using a `Set` call.

```cs
internal class MyContext : DbContext
{
    public DbSet<Dictionary<string, object>> Blogs => Set<Dictionary<string, object>>("Blog");

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.SharedTypeEntity<Dictionary<string, object>>(
            "Blog", bb =>
            {
                bb.Property<int>("BlogId");
                bb.Property<string>("Url");
                bb.Property<DateTime>("LastUpdated");
            });
    }
}
```

Property bag entity types can be used wherever a normal entity type is used, including as an owned entity type.  
However, they do have certain limitations:

- They can't have shadow properties
- Indexer navigations aren't supported
- Inheritance isn't supported
- Some relationship model-building API lack overloads for shared-type entity types
- Other types can't be marked as property bags

## References

- https://learn.microsoft.com/en-us/ef/core/modeling/shadow-properties
