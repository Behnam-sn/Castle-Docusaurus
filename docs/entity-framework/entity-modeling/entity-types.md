---
sidebar_position: 1
---

# Entity Types

Including a `DbSet` of a type on your context means that it is included in EF Core's model;  
We usually refer to such a type as an entity.

EF Core can read and write entity instances from/to the database,  
And if you're using a relational database, EF Core can create tables for your entities via migrations.

## Including Types in the Model

By convention, types that are exposed in DbSet properties on your context are included in the model as entities.  
Entity types that are specified in the `OnModelCreating` method are also included,  
As are any types that are found by recursively exploring the navigation properties of other discovered entity types.

For example:

```cs
public class MyContext : DbContext
{
    public DbSet<Blog> Blogs { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<AuditEntry>();
    }
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

    public Blog Blog { get; set; }
}

public class AuditEntry
{
    public int AuditEntryId { get; set; }
    public string Username { get; set; }
    public string Action { get; set; }
}
```

In the code sample above, all types are included:

- `Blog` is included because it's exposed in a `DbSet` property on the context.
- `Post` is included because it's discovered via the `Blog.Posts` navigation property.
- `AuditEntry` because it is specified in `OnModelCreating`.

## Excluding Types From the Model

If you don't want a type to be included in the model, you can exclude it:

### Fluent API

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Ignore<BlogMetadata>();
}
```

### Data Annotations

```cs
[NotMapped]
public class BlogMetadata
{
    public DateTime LoadedFromDatabase { get; set; }
}
```

## Excluding From Migrations

It is sometimes useful to have the same entity type mapped in multiple `DbContext` types.  
This is especially true when using bounded contexts,  
For which it is common to have a different `DbContext` type for each bounded context.

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<IdentityUser>()
        .ToTable("AspNetUsers", t => t.ExcludeFromMigrations());
}
```

With this configuration migrations will not create the `AspNetUsers` table,  
But `IdentityUser` is still included in the model and can be used normally.

If you need to start managing the table using migrations again,  
Then a new migration should be created where `AspNetUsers` is not excluded.  
The next migration will now contain any changes made to the table.

## Table Name

By convention, each entity type will be set up to map to a database table with the same name as the `DbSet` property that exposes the entity.  
If no `DbSet` exists for the given entity, the class name is used.

You can manually configure the table name:

### Fluent API

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .ToTable("blogs");
}
```

### Data Annotations

```cs
[Table("blogs")]
public class Blog
{
    public int BlogId { get; set; }
    public string Url { get; set; }
}
```

## Table Schema

When using a relational database, tables are by convention created in your database's default schema.  
For example, Microsoft SQL Server will use the `dbo` schema (SQLite does not support schemas).

You can configure tables to be created in a specific schema as follows:

### Fluent API

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .ToTable("blogs", schema: "blogging");
}
```

### Data Annotations

```cs
[Table("blogs", Schema = "blogging")]
public class Blog
{
    public int BlogId { get; set; }
    public string Url { get; set; }
}
```

Rather than specifying the schema for each table,  
You can also define the default schema at the model level with the fluent API:

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.HasDefaultSchema("blogging");
}
```

Note that setting the default schema will also affect other database objects, such as sequences.

## View Mapping

Entity types can be mapped to database views using the Fluent API.
EF will assume that the referenced view already exists in the database, it will not create it automatically in a migration.

```cs
modelBuilder.Entity<Blog>()
    .ToView("blogsView", schema: "blogging");
```

Mapping to a view will remove the default table mapping,  
But the entity type can also be mapped to a table explicitly.  
In this case the query mapping will be used for queries and the table mapping will be used for updates.

## Table-valued Function Mapping

It's possible to map an entity type to a table-valued function (TVF) instead of a table in the database.

To illustrate this, let's define another entity that represents blog with multiple posts.  
In the example, the entity is keyless, but it doesn't have to be.

```cs
public class BlogWithMultiplePosts
{
    public string Url { get; set; }
    public int PostCount { get; set; }
}
```

Next, create the following table-valued function in the database,  
Which returns only blogs with multiple posts as well as the number of posts associated with each of these blogs:

```sql
CREATE FUNCTION dbo.BlogsWithMultiplePosts()
RETURNS TABLE
AS
RETURN
(
    SELECT b.Url, COUNT(p.BlogId) AS PostCount
    FROM Blogs AS b
    JOIN Posts AS p ON b.BlogId = p.BlogId
    GROUP BY b.BlogId, b.Url
    HAVING COUNT(p.BlogId) > 1
)

```

Now, the entity `BlogWithMultiplePosts` can be mapped to this function in a following way:

```cs
modelBuilder.Entity<BlogWithMultiplePosts>()
    .HasNoKey()
    .ToFunction("BlogsWithMultiplePosts");
```

:::note
In order to map an entity to a table-valued function the function must be parameterless.
:::

Conventionally, the entity properties will be mapped to matching columns returned by the TVF.  
If the columns returned by the TVF have different names than the entity property,  
then the entity's columns can be configured using `HasColumnName` method, just like when mapping to a regular table.

When the entity type is mapped to a table-valued function, the query:

```cs
var query = from b in context.Set<BlogWithMultiplePosts>()
            where b.PostCount > 3
            select new { b.Url, b.PostCount };
```

Produces the following SQL:

```sql
SELECT [b].[Url], [b].[PostCount]
FROM [dbo].[BlogsWithMultiplePosts]() AS [b]
WHERE [b].[PostCount] > 3
```

## Table Comments

You can set an arbitrary text comment that gets set on the database table,  
Allowing you to document your schema in the database:

### Fluent API

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>().ToTable(
        tableBuilder => tableBuilder.HasComment("Blogs managed on the website"));
}
```

### Data Annotations

```cs
[Comment("Blogs managed on the website")]
public class Blog
{
    public int BlogId { get; set; }
    public string Url { get; set; }
}
```

## Shared-type Entity Types

Entity types that use the same CLR type are known as shared-type entity types.  
These entity types need to be configured with a unique name, which must be supplied whenever the shared-type entity type is used, in addition to the CLR type.  
This means that the corresponding `DbSet` property must be implemented using a `Set` call.

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

## References

- https://learn.microsoft.com/en-us/ef/core/modeling/entity-types
