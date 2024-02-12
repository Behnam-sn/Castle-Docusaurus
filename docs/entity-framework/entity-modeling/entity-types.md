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

## References

- https://learn.microsoft.com/en-us/ef/core/modeling/entity-types
