---
sidebar_position: 3
---

# Active Record

## What Is Active Record?

> An object that wraps a row in a database table or view,  
> Encapsulates the database access, and adds domain logic on that data.  
> — Martin Fowler

Like the transaction script pattern, active record supports cases where the business logic is simple.  
Here, however, the business logic may operate on more complex data structures.  
For example, instead of flat records, we can have more complicated object trees and hierarchies.

Operating on such data structures via a simple transaction script would result in lots of repetitive code.  
The mapping of the data to an in-memory representation would be duplicated all over.

## How to Implementation Active Record?

Consequently, this pattern uses dedicated objects, known as active records, to represent complicated data structures.

Apart from the data structure, these objects also implement data access methods for creating, reading, updating, and deleting records (the so-called CRUD operations).

As a result, the active record objects are coupled to an object-relational mapping (ORM) or some other data access framework.

The pattern’s name is derived from the fact that each data structure is “active”;  
That is, it implements data access logic.

The system’s business logic is organized in a transaction script.  
The difference between the two patterns is that in this case, instead of accessing the database directly, the transaction script manipulates active record objects.  
When it completes, the operation has to either complete or fail as an atomic transaction:

```cs
public class CreateUser
{
    ...
    public void Execute(userDetails)
    {
        try
        {
            _db.StartTransaction();
            var user = new User();
            user.Name = userDetails.Name;
            user.Email = userDetails.Email;
            user.Save();
            _db.Commit();
        } catch {
            _db.Rollback();
            throw;
        }
    }

}
```

The pattern’s goal is to encapsulate the complexity of mapping the in-memory object to the database’s schema.

In addition to being responsible for persistence, the active record objects can contain business logic;  
For example, validating new values assigned to the fields, or even implementing business-related procedures that manipulate an object’s data.

That said, the distinctive feature of an active record object is the separation of data structures and behavior (business logic).  
Usually, an active record’s fields have public getters and setters that allow external procedures to modify its state.

## When to Use Active Record?

Because an active record is essentially a transaction script that optimizes access to databases,  
This pattern can only support relatively simple business logic, such as CRUD operations, which, at most, validate the user’s input.

Accordingly, as in the case of the transaction script pattern, the active record pattern lends itself to supporting subdomains, integration of external solutions for generic subdomains, or model transformation tasks.  
The difference between the patterns is that active record addresses the complexity of mapping complicated data structures to a database’s schema.

The active record pattern is also known as an _anemic domain model antipattern_;  
in other words, an improperly designed domain model.

I prefer to restrain from the negative connotation of the words anemic and antipattern.

This pattern is a tool.  
Like any tool, it can solve problems, but it can potentially introduce more harm than good when applied in the wrong context.

There is nothing wrong with using active records when the business logic is simple.

Furthermore, using a more elaborate pattern when implementing simple business logic will also result in harm by introducing accidental
complexity.

## Be Pragmatic

Although business data is important and the code we design and build should protect
its integrity, there are cases in which a pragmatic approach is more desirable.
Especially at high levels of scale, there are cases when data consistency guarantees can
be relaxed. Check whether corrupting the state of one record out of 1 million is really
a showstopper for the business and whether it can negatively affect the performance
and profitability of the business. For example, let’s assume you are building a system
that ingests billions of events per day from IoT devices. Is it a big deal if 0.001% of the
events will be duplicated or lost?
As always, there are no universal laws. It all depends on the business domain you are
working in. It’s OK to “cut corners” where possible; just make sure you evaluate the
risks and business implications.
