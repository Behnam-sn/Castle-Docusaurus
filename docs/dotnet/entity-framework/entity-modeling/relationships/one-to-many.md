---
sidebar_position: 1
---

# One to Many

One-to-many relationships are used when a single entity is associated with any number of other entities.  
For example, a `Blog` can have many associated `Posts`, But each `Post` is associated with only one `Blog`.

This document is structured around lots of examples.  
The examples start with common cases, which also introduce concepts.  
Later examples cover less common kinds of configuration.  
A good approach here is to understand the first few examples and concepts,  
And then go to the later examples based on your specific needs.  
Based on this approach, we will start with simple "required" and "optional" one-to-many relationships.

## Required one-to-many

```cs
// Principal (parent)
public class Blog
{
    public int Id { get; set; }
    public ICollection<Post> Posts { get; } = new List<Post>(); // Collection navigation containing dependents
}
```

```cs
// Dependent (child)
public class Post
{
    public int Id { get; set; }
    public int BlogId { get; set; } // Required foreign key property
    public Blog Blog { get; set; } = null!; // Required reference navigation to principal
}
```

A one-to-many relationship is made up from:

- One or more **primary or alternate key** properties on the principal entity;  
  That is the "one" end of the relationship.  
  For example, `Blog.Id`.

- One or more **foreign key** properties on the dependent entity;  
  That is the "many" end of the relationship.  
  For example, `Post.BlogId`.

- Optionally, a collection navigation on the principal entity referencing the dependent entities.  
  For example, `Blog.Posts`.

- Optionally, a reference navigation on the dependent entity referencing the principal entity.  
  For example, `Post.Blog`.

So, for the relationship in this example:

- The foreign key property `Post.BlogId` is not nullable.  
  This makes the relationship "required",  
  Because every dependent (`Post`) must be related to some principal (`Blog`),  
  Since its foreign key property must be set to some value.

- Both entities have navigations pointing to the related entity or entities on the other side of the relationship.
