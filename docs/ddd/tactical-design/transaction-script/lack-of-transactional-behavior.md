---
sidebar_position: 1
---

# Lack of Transactional Behavior

A trivial example of failing to implement transactional behavior is to issue multiple updates without an overarching transaction.

Consider the following method that updates a record in the Users table and inserts a record into the VisitsLog table:

```cs
public class LogVisit
{
    ...
    public void Execute(Guid userId, DataTime visitedOn)
    {
        _db.Execute("UPDATE Users SET last_visit=@p1 WHERE user_id=@p2", visitedOn, userId);
        _db.Execute(@"INSERT INTO VisitsLog(user_id, visit_date) VALUES(@p1, @p2)", userId, visitedOn);
    }
}
```

If any issue occurs after the record in the Users table was updated (line 7),  
But before appending the log record on line 9 succeeds, the system will end up in an inconsistent state.

The Users table will be updated but no corresponding record will be written to the VisitsLog table.

The issue can be due to anything from a network outage to a database timeout or deadlock, or even a crash of the server executing the process.

This can be fixed by introducing a proper transaction encompassing both data changes:

```cs
public class LogVisit
{
    ...
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
Things get more complicated when you have to issue multiple updates in a database that doesn’t support multi-record transactions, or when you are working with multiple storage mechanisms that are impossible to unite in a distributed transaction.
