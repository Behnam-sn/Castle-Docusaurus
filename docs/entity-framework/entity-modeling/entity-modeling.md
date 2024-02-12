# Entity Modeling

## What is Entity Modeling?

EF Core uses a metadata model to describe how the application's entity types are mapped to the underlying database.

## How to Configure a Model in EF?

This model is built using a set of conventions.  
The model can then be customized using mapping attributes (also known as data annotations),  
And/or calls to the `ModelBuilder` methods (also known as fluent API) in `OnModelCreating`,  
Both of which will override the configuration performed by conventions.

Most configuration can be applied to a model targeting any data store.  
Providers may also enable configuration that is specific to a particular data store and they can also ignore configuration that is not supported or not applicable.

### Conventions

EF Core includes many model building conventions that are enabled by default.

You can find all of them in the list of classes that implement the `IConvention` interface.  
However, that list doesn't include conventions introduced by third-party database providers and plugins.

Applications can remove or replace any of these conventions,  
As well as add new custom conventions that apply configuration for patterns that are not recognized by EF out of the box.

### Fluent API

You can override the `OnModelCreating` method in your derived context and use the fluent API to configure your model.  
This is the most powerful method of configuration and allows configuration to be specified without modifying your entity classes.

Fluent API configuration has the highest precedence and will override conventions and data annotations.

The configuration is applied in the order the methods are called and if there are any conflicts the latest call will override previously specified configuration.

```cs
public class MyContext : DbContext
{
    public DbSet<Blog> Blogs { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        modelBuilder.Entity<Blog>()
            .Property(b => b.Url)
            .IsRequired();
    }
}

public class Blog
{
    public int BlogId { get; set; }
    public string Url { get; set; }
}
```

#### Grouping Configuration

To reduce the size of the `OnModelCreating` method all configuration for an entity type can be extracted to a separate class implementing `IEntityTypeConfiguration<TEntity>`.

```cs
public class BlogEntityTypeConfiguration : IEntityTypeConfiguration<Blog>
{
    public void Configure(EntityTypeBuilder<Blog> builder)
    {
        builder
            .Property(b => b.Url)
            .IsRequired();
    }
}
```

Then just invoke the Configure method from `OnModelCreating`.

```cs
new BlogEntityTypeConfiguration().Configure(modelBuilder.Entity<Blog>());
```

#### Applying All Configurations in an Assembly

It is possible to apply all configuration specified in types implementing `IEntityTypeConfiguration` in a given assembly.

```cs
modelBuilder.ApplyConfigurationsFromAssembly(typeof(BlogEntityTypeConfiguration).Assembly);
```

:::note
The order in which the configurations will be applied is undefined,  
Therefore this method should only be used when the order doesn't matter.
:::

### Data Annotations

You can also apply certain attributes (known as Data Annotations) to your classes and properties.

```cs
public class MyContext : DbContext
{
    public DbSet<Blog> Blogs { get; set; }
}

[Table("Blogs")]
public class Blog
{
    public int BlogId { get; set; }

    [Required]
    public string Url { get; set; }
}
```

Data annotations will override conventions,  
But will be overridden by Fluent API configuration.

## References

- https://learn.microsoft.com/en-us/ef/core/modeling/
