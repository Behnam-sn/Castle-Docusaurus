---
sidebar_position: 2
---

# Entity Properties

Each entity type in your model has a set of properties,  
Which EF Core will read and write from the database.

If you're using a relational database, entity properties map to table columns.

## Include Properties

By convention, all public properties with a getter and a setter will be included in the model.

## Exclude Properties

Specific properties can be excluded as follows:

**Fluent API**

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Ignore(b => b.LoadedFromDatabase);
}
```

**Data Annotations**

```cs
public class Blog
{
    public int BlogId { get; set; }
    public string Url { get; set; }

    [NotMapped]
    public DateTime LoadedFromDatabase { get; set; }
}
```

## Column Names

By convention, when using a relational database, entity properties are mapped to table columns having the same name as the property.  
If you prefer to configure your columns with different names, you can do so as following code snippet:

**Fluent API**

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.BlogId)
        .HasColumnName("blog_id");
}
```

**Data Annotations**

```cs
public class Blog
{
    [Column("blog_id")]
    public int BlogId { get; set; }

    public string Url { get; set; }
}
```

## Column Data Types

When using a relational database, the database provider selects a data type based on the .NET type of the property.  
It also takes into account other metadata, such as the configured maximum length, whether the property is part of a primary key, etc.

For example, SQL Server maps `DateTime` properties to `datetime2(7)` columns,  
And string properties to `nvarchar(max)` columns or to `nvarchar(450)` for properties that are used as a key.

You can also configure your columns to specify an exact data type for a column.  
For example, the following code configures `Url` as a non-unicode string with maximum length of 200 and Rating as `decimal` with precision of 5 and scale of 2:

**Fluent API**

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>(
        eb =>
        {
            eb.Property(b => b.Url).HasColumnType("varchar(200)");
            eb.Property(b => b.Rating).HasColumnType("decimal(5, 2)");
        });
}
```

**Data Annotations**

```cs
public class Blog
{
    public int BlogId { get; set; }

    [Column(TypeName = "varchar(200)")]
    public string Url { get; set; }

    [Column(TypeName = "decimal(5, 2)")]
    public decimal Rating { get; set; }
}
```

## Maximum Length

Configuring a maximum length provides a hint to the database provider about the appropriate column data type to choose for a given property.  
Maximum length only applies to `array` data types, such as `string` and `byte[]`.

In the following example, configuring a maximum length of 500 will cause a column of type `nvarchar(500)` to be created on SQL Server:

**Fluent API**

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Url)
        .HasMaxLength(500);
}
```

**Data Annotations**

```cs
public class Blog
{
    public int BlogId { get; set; }

    [MaxLength(500)]
    public string Url { get; set; }
}
```

Entity Framework does not do any validation of maximum length before passing data to the provider.  
It is up to the provider or data store to validate if appropriate.

For example, when targeting SQL Server, exceeding the maximum length will result in an exception as the data type of the underlying column will not allow excess data to be stored.

## Precision and Scale

Some relational data types support the precision and scale facets;  
These control what values can be stored, and how much storage is needed for the column.

Which data types support precision and scale is database-dependent,  
But in most databases `decimal` and `DateTime` types do support these facets.

For `decimal` properties,  
Precision defines the maximum number of digits needed to express any value the column will contain,  
And scale defines the maximum number of decimal places needed.

For `DateTime` properties,  
Precision defines the maximum number of digits needed to express fractions of seconds,  
And scale is not used.

In the following example,  
Configuring the `Score` property to have precision 14 and scale 2 will cause a column of type `decimal(14,2)` to be created on SQL Server,  
And configuring the `LastUpdated` property to have precision 3 will cause a column of type `datetime2(3)`:

**Fluent API**

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Score)
        .HasPrecision(14, 2);

    modelBuilder.Entity<Blog>()
        .Property(b => b.LastUpdated)
        .HasPrecision(3);
}
```

**Data Annotations**

```cs
public class Blog
{
    public int BlogId { get; set; }
    [Precision(14, 2)]
    public decimal Score { get; set; }
    [Precision(3)]
    public DateTime LastUpdated { get; set; }
}
```

Entity Framework does not do any validation of precision or scale before passing data to the provider.  
It is up to the provider or data store to validate as appropriate.

For example, when targeting SQL Server, a column of data type `datetime` does not allow the precision to be set,  
Whereas a `datetime2` one can have precision between 0 and 7 inclusive.

## References

- https://learn.microsoft.com/en-us/ef/core/modeling/entity-properties
