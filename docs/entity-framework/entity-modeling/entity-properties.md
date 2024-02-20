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

## Unicode

In some relational databases, different types exist to represent Unicode and non-Unicode text data.

For example, in SQL Server, `nvarchar(x)` is used to represent Unicode data in UTF-16,  
While `varchar(x)` is used to represent non-Unicode data (but see the notes on SQL Server UTF-8 support).  
For databases which don't support this concept, configuring this has no effect.

Text properties are configured as Unicode by default.  
You can configure a column as non-Unicode as follows:

**Data Annotations**

```cs
public class Book
{
    public int Id { get; set; }
    public string Title { get; set; }

    [Unicode(false)]
    [MaxLength(22)]
    public string Isbn { get; set; }
}
```

**Fluent API**

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Book>()
        .Property(b => b.Isbn)
        .IsUnicode(false);
}
```

## Required and Optional Properties

A property is considered optional if it is valid for it to contain `null`.  
If `null` is not a valid value to be assigned to a property then it is considered to be a required property.

When mapping to a relational database schema,  
Required properties are created as non-nullable columns,  
And optional properties are created as nullable columns.

**Conventions**

By convention, a property whose .NET type can contain `null` will be configured as optional,  
Whereas properties whose .NET type cannot contain null will be configured as required.

For example, all properties with .NET value types (`int`, `decimal`, `bool`, etc.) are configured as required,  
And all properties with nullable .NET value types (`int?`, `decimal?`, `bool?`, etc.) are configured as optional.

C# 8 introduced a new feature called nullable reference types (NRT),  
Which allows reference types to be annotated, indicating whether it is valid for them to contain null or not.

This feature is enabled by default in new project templates,  
But remains disabled in existing projects unless explicitly opted into.

Nullable reference types affect EF Core's behavior in the following way:

- If nullable reference types are disabled,  
  All properties with .NET reference types are configured as optional by convention (for example, `string`).
- If nullable reference types are enabled,  
  Properties will be configured based on the C# nullability of their .NET type:  
  `string?` will be configured as optional, but `string` will be configured as required.

The following example shows an entity type with required and optional properties,  
With the nullable reference feature disabled and enabled:

**Without NRT (Default)**

```cs
public class CustomerWithoutNullableReferenceTypes
{
    public int Id { get; set; }

    [Required] // Data annotations needed to configure as required
    public string FirstName { get; set; }

    [Required] // Data annotations needed to configure as required
    public string LastName { get; set; }

    public string MiddleName { get; set; } // Optional by convention
}
```

**With NRT**

```cs
public class Customer
{
    public int Id { get; set; }
    public string FirstName { get; set; } // Required by convention
    public string LastName { get; set; } // Required by convention
    public string? MiddleName { get; set; } // Optional by convention

    // Note the following use of constructor binding, which avoids compiled warnings
    // for uninitialized non-nullable properties.
    public Customer(string firstName, string lastName, string? middleName = null)
    {
        FirstName = firstName;
        LastName = lastName;
        MiddleName = middleName;
    }
}
```

Using nullable reference types is recommended since it flows the nullability expressed in C# code to EF Core's model and to the database, and obviates the use of the Fluent API or Data Annotations to express the same concept twice.

:::note
Exercise caution when enabling nullable reference types on an existing project.  
Reference type properties which were previously configured as optional will now be configured as required,  
Unless they are explicitly annotated to be nullable.

When managing a relational database schema,  
This may cause migrations to be generated which alter the database column's nullability.
:::

## Explicit configuration

A property that would be optional by convention can be configured to be required as follows:

**Data Annotations**

```cs
public class Blog
{
    public int BlogId { get; set; }

    [Required]
    public string Url { get; set; }
}
```

**Fluent API**

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Url)
        .IsRequired();
}
```

## Column Collations

A collation can be defined on text columns, determining how they are compared and ordered.  
For example, the following code snippet configures a SQL Server column to be case-insensitive:

```cs
modelBuilder.Entity<Customer>()
    .Property(c => c.Name)
    .UseCollation("SQL_Latin1_General_CP1_CI_AS");
```

:::note
If all columns in a database need to use a certain collation, define the collation at the database level instead.
:::

## Column Comments

You can set an arbitrary text comment that gets set on the database column,  
Allowing you to document your schema in the database:

**Data Annotations**

```cs
public class Blog
{
    public int BlogId { get; set; }

    [Comment("The URL of the blog")]
    public string Url { get; set; }
}
```

**Fluent API**

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Url)
        .HasComment("The URL of the blog");
}
```

## Column Order

By default when creating a table with Migrations,  
EF Core orders primary key columns first,  
Followed by properties of the entity type and owned types,  
And finally properties from base types.

You can, however, specify a different column order:

**Data Annotations**

```cs
public class EntityBase
{
    [Column(Order = 0)]
    public int Id { get; set; }
}

public class PersonBase : EntityBase
{
    [Column(Order = 1)]
    public string FirstName { get; set; }

    [Column(Order = 2)]
    public string LastName { get; set; }
}

public class Employee : PersonBase
{
    public string Department { get; set; }
    public decimal AnnualSalary { get; set; }
}
```

**Fluent API**

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Employee>(x =>
    {
        x.Property(b => b.Id)
            .HasColumnOrder(0);

        x.Property(b => b.FirstName)
            .HasColumnOrder(1);

        x.Property(b => b.LastName)
            .HasColumnOrder(2);
    });
}
```

:::note
Note that, in the general case, most databases only support ordering columns when the table is created.  
This means that the column order attribute cannot be used to re-order columns in an existing table.
:::

## References

- https://learn.microsoft.com/en-us/ef/core/modeling/entity-properties
