# Notes

<!-- out of place -->

<!-- also page 112 of the book is out of place -->

## Aggregate Pattern & Databases

### Concurrency

It’s vital to protect the consistency of an aggregate’s state.

If multiple processes are concurrently updating the same aggregate,  
We have to prevent the latter transaction from blindly overwriting the changes committed by the first one.

In such a case,  
The second process has to be notified,  
That the state on which it had based its decisions is out of date,  
And it has to retry the operation.

Hence, the database used for storing aggregates has to support concurrency management.

In its simplest form,  
An aggregate should hold a version field that will be incremented after each update:

```cs
class Ticket
{
    private TicketId _id;
    private int _version;
}
```

When committing a change to the database,  
We have to ensure that the version that is being overwritten matches the one that was originally read.

For example, in SQL:

```sql
UPDATE tickets
SET ticket_status = @new_status,
agg_version = agg_version + 1
WHERE ticket_id = @id AND agg_version = @expected_version;
```

This SQL statement,  
Applies changes made to the aggregate instance’s state (line 2),  
And increases its version counter (line 3),  
but only if the current version equals the one that was read prior to applying changes to the aggregate’s state (line 4).

:::note
Of course, concurrency management can be implemented elsewhere besides a relational database.  
Furthermore, document databases lend themselves more toward working with aggregates.

**It’s crucial to ensure that the database used for storing an aggregate’s data supports concurrency management.**
:::

### Transaction Boundary

Since an aggregate’s state can only be modified by its own business logic,  
The aggregate also acts as a transactional boundary.

All changes to the aggregate’s state should be committed transactionally as one atomic operation.  
If an aggregate’s state is modified, either all the changes are committed or none of them is.

Furthermore, no system operation can assume a multi-aggregate transaction.  
A change to an aggregate’s state can only be committed individually, one aggregate per database transaction.

The one aggregate instance per transaction forces us to carefully design an aggregate’s boundaries,  
Ensuring that the design addresses the business domain’s invariants and rules.

The need to commit changes in multiple aggregates signals a wrong transaction boundary,  
And hence, wrong aggregate boundaries.

This seems to impose a modeling limitation.  
What if we need to modify multiple objects in the same transaction?  
Let’s see how the pattern addresses such situations.

## Hierarchy of Entities

As we discussed earlier,  
We don’t use entities as an independent pattern,  
Only as part of an aggregate.

Let’s see the fundamental difference between entities and aggregates,  
And why entities are a building block of an aggregate rather than of the overarching domain model.

There are business scenarios in which multiple objects should share a transactional boundary;  
For example, when both can be modified simultaneously,  
Or the business rules of one object depend on the state of another object.

DDD prescribes that a system’s design should be driven by its business domain.  
Aggregates are no exception.

To support changes to multiple objects that have to be applied in one atomic transaction,  
The aggregate pattern resembles a hierarchy of entities, all sharing transactional consistency.

```cs
ticket
message
attachment
```

The hierarchy contains both entities and value objects,  
And all of them belong to the same aggregate,  
If they are bound by the domain’s business logic.

That’s why the pattern is named **Aggregate**:  
It aggregates business entities and value objects that belong to the same transaction boundary.

The following code sample demonstrates a business rule that spans multiple entities belonging to the aggregate’s boundary:

“If an agent didn’t open an escalated ticket within 50% of the response time limit,  
it is automatically reassigned to a different agent”

```cs
public class Ticket
{
    private List<Message> _messages;

    public void Execute(EvaluateAutomaticActions cmd)
    {
        if (this.IsEscalated && this.RemainingTimePercentage < 0.5 && GetUnreadMessagesCount(for: AssignedAgent) > 0)
        {
            _agent = AssignNewAgent();
        }
    }

    public int GetUnreadMessagesCount(UserId id)
    {
        return _messages.Where(x => x.To == id && !x.WasRead).Count();
    }
}
```
