---
sidebar_position: 1
---

# Transaction Script

## What is Transaction Script Pattern?

> Transaction script organizes business logic by procedures,  
> Where each procedure handles a single request from the presentation.  
> — Martin Fowler

A system’s public interface can be seen as a collection of business transactions that consumers can execute.  
These transactions can retrieve information managed by the system, modify it, or both.

<!-- The pattern organizes the system’s business logic based on procedures,
Where each procedure implements an operation that is executed by the system’s consumer via its public interface. -->

In effect, the system’s public operations are used as encapsulation boundaries.

```cs
public interface BackLogService
{
    int AddItem(string item);
    void SetPriority(int itemId, int priority);
    string[] ListItems();
    void Assign(int itemId, int sprintId);
}
```

## How to Implement Transaction Script Pattern?

Each procedure is implemented as a simple, straightforward procedural script.

The only requirement procedures have to fulfill is transactional behavior:  
_Each operation should either succeed or fail but can never result in an invalid state._

Even if execution of a transaction script fails at the most inconvenient moment, the system should remain consistent.  
Either by rolling back any changes it has made up until the failure, or by executing compensating actions.

The transactional behavior is reflected in the pattern’s name: Transaction Script

Here is an example of a transaction script that converts batches of JSON files into XML files:

```cs
DB.StartTransaction();
var job = DB.LoadNextJob();
var json = LoadFile(job.Source);
var xml = ConvertJsonToXml(json);
WriteFile(job.Destination, xml.ToString();
DB.MarkJobAsCompleted(job);
DB.Commit()
```

:::tip
Transaction scripts can use a thin abstraction layer for integrating with storage mechanisms,  
But it is also free to access the databases directly.
:::

## What are The Challenges of Transaction Script Pattern?

The transaction script pattern is a foundation for the more advanced business logic implementation patterns.  
Furthermore, despite its apparent simplicity, it is the easiest pattern to get wrong.

A considerable number of production issues in one way or another,  
Often boiled down to a misimplementation of the transactional behavior of the system’s business logic.

Let’s take a look at 3 common, real-life examples of data corruption,  
That results from failing to correctly implement a transaction script:

### Lack of Transactional Behavior

A trivial example of failing to implement transactional behavior is to issue multiple updates without an overarching transaction.

Consider the following method that updates a record in the `Users` table and inserts a record into the `VisitsLog` table:

```cs
public class LogVisit
{
    public void Execute(Guid userId, DataTime visitedOn)
    {
        _db.Execute("UPDATE Users SET last_visit=@p1 WHERE user_id=@p2", visitedOn, userId);
        _db.Execute(@"INSERT INTO VisitsLog(user_id, visit_date) VALUES(@p1, @p2)", userId, visitedOn);
    }
}
```

If any issue occurs after the record in the `Users` table was updated,  
But before appending the log record succeeds,  
The system will end up in an inconsistent state.

The `Users` table will be updated but no corresponding record will be written to the `VisitsLog` table.

The issue can be due to anything from a network outage to a database timeout or deadlock, or even a crash of the server executing the process.

This can be fixed by introducing a proper transaction encompassing both data changes:

```cs
public class LogVisit
{
    public void Execute(Guid userId, DataTime visitedOn)
    {
        try
        {
            _db.StartTransaction();
            _db.Execute(@"UPDATE Users SET last_visit=@p1 WHERE user_id=@p2", visitedOn, userId);
            _db.Execute(@"INSERT INTO VisitsLog(user_id, visit_date) VALUES(@p1, @p2)", userId, visitedOn);
            _db.Commit();
        } catch {
            _db.Rollback();
            throw;
        }
    }
}
```

The fix is easy to implement due to relational databases’ native support of transactions spanning multiple records.

Things get more complicated when you have to issue multiple updates in a database that doesn’t support multi-record transactions,  
Or when you are working with multiple storage mechanisms that are impossible to unite in a distributed transaction.

### Distributed Transactions

In modern distributed systems, it’s a common practice to make changes to the data in a database and then notify other components of the system about the changes by publishing messages into a message bus.

Consider that in the previous example, instead of logging a visit in a table, we have to publish it to a message bus:

```cs
public class LogVisit
{
    public void Execute(Guid userId, DataTime visitedOn)
    {
        _db.Execute("UPDATE Users SET last_visit=@p1 WHERE user_id=@p2", visitedOn,userId);
        _messageBus.Publish("VISITS_TOPIC", new { UserId = userId, VisitDate = visitedOn });
    }
}
```

Any failure occurring after executing the query but before publishing the message will corrupt the system’s state.  
The `Users` table will be updated but the other components won’t be notified as publishing to the message bus has failed.

Unfortunately, fixing the issue is not as easy as in the previous example.  
Distributed transactions spanning multiple storage mechanisms are complex, hard to scale, error prone, and therefore are usually avoided.

You can learn how to use the CQRS architectural pattern to populate multiple storage mechanisms.  
In addition, You can learn the outbox pattern, which enables reliable publishing of messages after committing changes to another database.

### Implicit Distributed Transactions

Let’s see a more intricate example of improper implementation of transactional behavior.  
Consider the following deceptively simple method:

```cs
public class LogVisit
{
    public void Execute(Guid userId)
    {
        _db.Execute("UPDATE Users SET visits=visits+1 WHERE user_id=@p1", userId);
    }
}
```

Instead of tracking the last visit date as in the previous examples,  
This method maintains a counter of visits for each user.

Calling the method increases the corresponding counter’s value by 1.  
All the method does is update one value, in one table, residing in one database.  
Yet this is still a distributed transaction that can potentially lead to inconsistent state.

This example constitutes a distributed transaction,  
Because it communicates information to the databases and the external process that called the method.

Although the execute method is of type `void`, and it doesn’t return any data,  
It still communicates whether the operation has succeeded or failed:  
If it failed, the caller will get an exception.

What if the method succeeds, but the communication of the result to the caller fails? For example:

If `LogVisit` is part of a REST service and there is a network outage;

Or if both `LogVisit` and the caller are running in the same process,  
But the process fails before the caller gets to track successful execution of the `LogVisit` action?

In both cases, the consumer will assume failure and try calling `LogVisit` again.

Executing the `LogVisit` logic again will result in an incorrect increase of the counter’s value.  
Overall, it will be increased by 2 instead of 1.

As in the previous two examples,  
The code fails to implement the transaction script pattern correctly,  
And inadvertently leads to corrupting the system’s state.

There is no simple fix for this issue.  
It all depends on the business domain and its needs.

In this specific example,  
One way to ensure transactional behavior is to make the operation idempotent;  
That is, leading to the same result even if the operation repeated multiple times.

For example, we can ask the consumer to pass the value of the counter.  
To supply the counter’s value,  
The caller will have to read the current value first,  
Increase it locally,  
And then provide the updated value as a parameter.

Even if the operation will be executed multiple times,  
It won’t change the end result.

```cs
public class LogVisit
{
    public void Execute(Guid userId, long visits)
    {
        _db.Execute("UPDATE Users SET visits = @p1 WHERE user_id=@p2", visits, userId);
    }
}
```

Another way to address such an issue is to use _optimistic concurrency control_:  
Prior to calling the `LogVisit` operation,  
The caller has read the counter’s current value and passed it to `LogVisit` as a parameter.  
`LogVisit` will update the counter’s value only if it equals the one initially read by the caller:

```cs
public class LogVisit
{
    public void Execute(Guid userId, long expectedVisits)
    {
        _db.Execute(@"UPDATE Users SET visits=visits+1 WHERE user_id=@p1 and visits=@p2", userId, visits);
    }
}
```

Subsequent executions of `LogVisit` with the same input parameters won’t change the data,  
As the `WHERE...visits = @prm2` condition won’t be fulfilled.

## When to Use Transaction Script Pattern?

The transaction script pattern is well adapted to the most straightforward problem domains,  
In which the business logic resembles simple procedural operations.

For example, in extract-transform-load (ETL) operations,  
Each operation extracts data from a source,  
Applies transformation logic to convert it into another form,  
And loads the result into the destination store.

The transaction script pattern naturally fits supporting subdomains where, by definition, the business logic is simple.  
It can also be used as an adapter for integration with external systems.  
For example, generic subdomains, or as a part of an anticorruption layer.

The main advantage of the transaction script pattern is its simplicity.  
It introduces minimal abstractions and minimizes the overhead both in runtime performance and in understanding the business logic.

That said, this simplicity is also the pattern’s disadvantage.  
The more complex the business logic gets,  
The more it’s prone to duplicate business logic across transactions,  
And consequently, to result in inconsistent behavior—when the duplicated code goes out of sync.

As a result, transaction script should never be used for core subdomains,  
As this pattern won’t cope with the high complexity of a core subdomain’s business logic.

This simplicity earned the transaction script a dubious reputation.  
Sometimes the pattern is even treated as an antipattern.  
After all, if complex business logic is implemented as a transaction script,  
Sooner rather than later it’s going to turn into an unmaintainable, big ball of mud.

It should be noted, however, that despite the simplicity, the transaction script pattern is ubiquitous in software development.  
All the business logic implementation patterns that we will discuss in this and the following chapters, in one way or another, are based on the transaction script pattern.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
