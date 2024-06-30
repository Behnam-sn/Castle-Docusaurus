---
sidebar_position: 5
---

# Shadow Properties

## What are Shadow Properties?

Shadow properties are properties that aren't defined in your .NET entity class but are defined for that entity type in the EF Core model.  
The value and state of these properties are maintained purely in the Change Tracker.  
Shadow properties are useful when there's data in the database that shouldn't be exposed on the mapped entity types.

## Foreign Key Shadow Properties

Shadow properties are most often used for foreign key properties,  
Where they are added to the model by convention,  
When no foreign key property has been found by convention or configured explicitly.

The relationship is represented by navigation properties,  
But in the database it is enforced by a foreign key constraint,  
And the value for the foreign key column is stored in the corresponding shadow property.

The property will be named `<navigation property name><principal key property name>`  
(the navigation on the dependent entity, which points to the principal entity, is used for the naming).

If the principal key property name starts with the name of the navigation property,  
Then the name will just be `<principal key property name>`.

If there is no navigation property on the dependent entity,  
Then the principal type name concatenated with the primary or alternate key property name is used in its place `<principal type name><principal key property name>`.

For example, the following code listing will result in a `BlogId` shadow property being introduced to the `Post` entity:

```cs
internal class MyContext : DbContext
{
    public DbSet<Blog> Blogs { get; set; }
    public DbSet<Post> Posts { get; set; }
}

public class Blog
{
    public int BlogId { get; set; }
    public string Url { get; set; }
    public List<Post> Posts { get; set; }
}

public class Post
{
    public int PostId { get; set; }
    public string Title { get; set; }
    public string Content { get; set; }
    // Since there is no CLR property which holds the foreign
    // key for this relationship, a shadow property is created.
    public Blog Blog { get; set; }
}
```

## Configuring Shadow Properties

You can use the Fluent API to configure shadow properties.  
Once you have called the `string` overload of `Property<TProperty>(String)`,  
You can chain any of the configuration calls you would for other properties.

In the following sample, since `Blog` has no CLR property named `LastUpdated`, a shadow property is created:

```cs
internal class MyContext : DbContext
{
    public DbSet<Blog> Blogs { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Blog>()
            .Property<DateTime>("LastUpdated");
    }
}

public class Blog
{
    public int BlogId { get; set; }
    public string Url { get; set; }
}
```

:::note
If the name supplied to the Property method matches the name of an existing property,  
A shadow property or one defined on the entity class,  
Then the code will configure that existing property rather than introducing a new shadow property.
:::

## Accessing Shadow Properties

Shadow property values can be obtained and changed through the `ChangeTracker` API:

```cs
context.Entry(myBlog).Property("LastUpdated").CurrentValue = DateTime.Now;
```

Shadow properties can be referenced in LINQ queries via the `EF.Property` static method:

```cs
var blogs = context.Blogs
    .OrderBy(b => EF.Property<DateTime>(b, "LastUpdated"));
```

:::note
Shadow properties cannot be accessed after a no-tracking query since the entities returned are not tracked by the change tracker.
:::

## References

- https://learn.microsoft.com/en-us/ef/core/modeling/shadow-properties
