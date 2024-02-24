---
sidebar_position: 4
---

# Generated Values

Database columns can have their values generated in various ways:  
Primary key columns are frequently auto-incrementing integers,  
Other columns have default or computed values, etc.  
This page details various patterns for configuration value generation with EF Core.

## Default Values

On relational databases, a column can be configured with a default value;  
If a row is inserted without a value for that column, the default value will be used.

You can configure a default value on a property:

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Rating)
        .HasDefaultValue(3);
}
```

You can also specify a SQL fragment that is used to calculate the default value:

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Created)
        .HasDefaultValueSql("getdate()");
}
```

## Computed Columns

On most relational databases, a column can be configured to have its value computed in the database,  
Typically with an expression referring to other columns:

```cs
modelBuilder.Entity<Person>()
    .Property(p => p.DisplayName)
    .HasComputedColumnSql("[LastName] + ', ' + [FirstName]");
```

The above creates a virtual computed column, whose value is computed every time it is fetched from the database.  
You may also specify that a computed column be stored (sometimes called persisted),  
Meaning that it is computed on every update of the row, and is stored on disk alongside regular columns:

```cs
modelBuilder.Entity<Person>()
    .Property(p => p.NameLength)
    .HasComputedColumnSql("LEN([LastName]) + LEN([FirstName])", stored: true);
```

### Primary Keys

By convention, non-composite primary keys of type `short`, `int`, `long`, or `Guid` are set up to have values generated for inserted entities if a value isn't provided by the application.

Your database provider typically takes care of the necessary configuration;  
For example, a numeric primary key in SQL Server is automatically set up to be an `IDENTITY` column.

For more information, see the documentation about keys and guidance for specific inheritance mapping strategies.

## Explicitly Configuring Value Generation

We saw above that EF Core automatically sets up value generation for primary keys,  
But we may want to do the same for non-key properties.

You can configure any property to have its value generated for inserted entities as follows:

**Data Annotations**

```cs
public class Blog
{
    public int BlogId { get; set; }
    public string Url { get; set; }

    [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
    public DateTime Inserted { get; set; }
}
```

**Fluent API**

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Inserted)
        .ValueGeneratedOnAdd();
}
```

Similarly, a property can be configured to have its value generated on add or update:

**Data Annotations**

```cs
public class Blog
{
    public int BlogId { get; set; }
    public string Url { get; set; }

    [DatabaseGenerated(DatabaseGeneratedOption.Computed)]
    public DateTime LastUpdated { get; set; }
}
```

**Fluent API**

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.LastUpdated)
        .ValueGeneratedOnAddOrUpdate();
}
```

Unlike with default values or computed columns, we are not specifying how the values are to be generated;  
That depends on the database provider being used.

Database providers may automatically set up value generation for some property types,  
But others may require you to manually set up how the value is generated.

For example, on SQL Server, when a `GUID` property is configured as a primary key,  
The provider automatically performs value generation client-side,  
Using an algorithm to generate optimal sequential `GUID` values.

However, specifying `ValueGeneratedOnAdd` on a `DateTime` property will have no effect.  
See the section below for `DateTime` value generation.

<!-- Similarly, `byte[]` properties that are configured as generated on add or update and marked as concurrency tokens are set up with the `rowversion` data type, so that values are automatically generated in the database.
However, specifying `ValueGeneratedOnAdd` has no effect. -->

Consult your Database provider's documentation for the specific value generation techniques it supports.

## Overriding Value Generation

Although a property is configured for value generation,  
In many cases you may still explicitly specify a value for it.

Whether this will actually work depends on the specific value generation mechanism that has been configured;  
While you may specify an explicit value instead of using a column's default value, the same cannot be done with computed columns.

To override value generation with an explicit value,  
Simply set the property to any value that is not the CLR default value for that property's type.  
null for string, 0 for int, Guid.Empty for Guid, etc.
