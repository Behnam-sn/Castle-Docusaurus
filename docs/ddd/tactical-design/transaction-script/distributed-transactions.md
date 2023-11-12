---
sidebar_position: 2
---

# Distributed Transactions

In modern distributed systems, it’s a common practice to make changes to the data in a database and then notify other components of the system about the changes by publishing messages into a message bus.

Consider that in the previous example, instead of logging a visit in a table, we have to publish it to a message bus:

```cs
public class LogVisit
{
    ...
    public void Execute(Guid userId, DataTime visitedOn)
    {
        _db.Execute("UPDATE Users SET last_visit=@p1 WHERE user_id=@p2", visitedOn,userId);
        _messageBus.Publish("VISITS_TOPIC", new { UserId = userId, VisitDate = visitedOn });
    }
}
```

Any failure occurring after line 7 but before line 9 succeeds will corrupt the system’s state.  
The Users table will be updated but the other components won’t be notified as publishing to the message bus has failed.

Unfortunately, fixing the issue is not as easy as in the previous example.  
Distributed transactions spanning multiple storage mechanisms are complex, hard to scale, error prone, and therefore are usually avoided.

You can learn how to use the CQRS architectural pattern to populate multiple storage mechanisms.  
In addition, You can learn the outbox pattern, which enables reliable publishing of messages after committing changes to another database.
