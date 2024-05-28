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
