---
sidebar_position: 3
---

# Implicit Distributed Transactions

Let’s see a more intricate example of improper implementation of transactional behavior.  
Consider the following deceptively simple method:

```cs
public class LogVisit
{
    ...
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

This example constitutes a distributed transaction because it communicates information to the databases and the external process that called the method.

Although the execute method is of type void, and it doesn’t return any data,  
It still communicates whether the operation has succeeded or failed:  
If it failed, the caller will get an exception.

What if the method succeeds, but the communication of the result to the caller fails? For example:

- If LogVisit is part of a REST service and there is a network outage; or
- If both LogVisit and the caller are running in the same process, but the process fails before the caller gets to track successful execution of the LogVisit action?

In both cases, the consumer will assume failure and try calling LogVisit again.

Executing the LogVisit logic again will result in an incorrect increase of the counter’s value.  
Overall, it will be increased by 2 instead of 1.

As in the previous two examples, the code fails to implement the transaction script pattern correctly, and inadvertently leads to corrupting the system’s state.

There is no simple fix for this issue.  
It all depends on the business domain and its needs.

In this specific example, one way to ensure transactional behavior is to make the operation idempotent:  
That is, leading to the same result even if the operation repeated multiple times.

For example, we can ask the consumer to pass the value of the counter.  
To supply the counter’s value, the caller will have to read the current value first, increase it locally, and then provide the updated value as a parameter.  
Even if the operation will be executed multiple times, it won’t change the end result:

```cs
public class LogVisit
{
    ...
    public void Execute(Guid userId, long visits)
    {
        _db.Execute("UPDATE Users SET visits = @p1 WHERE user_id=@p2", visits, userId);
    }
}
```

Another way to address such an issue is to use optimistic concurrency control:  
prior to calling the LogVisit operation, the caller has read the counter’s current value and passed it to LogVisit as a parameter.  
LogVisit will update the counter’s value only if it equals the one initially read by the caller:

```cs
public class LogVisit
{
    ...
    public void Execute(Guid userId, long expectedVisits)
    {
        _db.Execute(@"UPDATE Users SET visits=visits+1 WHERE user_id=@p1 and visits = @p2", userId, visits);
    }
}
```

Subsequent executions of LogVisit with the same input parameters won’t change the data,  
As the `WHERE...visits = @prm2` condition won’t be fulfilled.
