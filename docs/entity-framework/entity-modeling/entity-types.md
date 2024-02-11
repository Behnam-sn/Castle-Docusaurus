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

## References

- https://learn.microsoft.com/en-us/ef/core/modeling/entity-types
