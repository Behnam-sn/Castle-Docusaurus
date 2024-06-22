# Notes

<!-- out of place -->

<!-- also page 112 of the book is out of place -->

## Aggregate

The data fields are read-only for external components,  
For the sake of ensuring that all the business logic related to the aggregate resides in its boundaries.

The aggregate acts as a transactional boundary.  
All of its data, including all of its internal objects,  
Has to be committed to the database as one atomic transaction.

## Referencing Other Aggregates

Since all objects contained by an aggregate share the same transactional boundary,  
Performance and scalability issues may arise if an aggregate grows too large.

The consistency of the data can be a convenient guiding principle for designing an aggregate’s boundaries.

Only the information that is required by the aggregate’s business logic to be strongly consistent should be a part of the aggregate.  
All information that can be eventually consistent should reside outside of the aggregate’s boundary;

The rule of thumb is to keep the aggregates as small as possible,  
And include only objects that are required to be in a strongly consistent state by the aggregate’s business logic:

```cs
public class Ticket
{
    private UserId _customer;
    private List<ProductId> _products;
    private UserId _assignedAgent;
    private List<Message> _messages;
}
```

In the preceding example,  
The `Ticket` aggregate references a collection of messages,  
Which belong to the aggregate’s boundary.

On the other hand, the customer, the collection of products that are relevant to the ticket,  
And the assigned agent do not belong to the aggregate and therefore are referenced by its ID.

The reasoning behind referencing external aggregates by ID is to reify that these objects do not belong to the aggregate’s boundary,  
And to ensure that each aggregate has its own transactional boundary.

To decide whether an entity belongs to an aggregate or not,  
Examine whether the aggregate contains business logic that can lead to an invalid system state if it will work on eventually consistent data.

Let’s go back to the previous example of reassigning the ticket,  
If the current agent didn’t read the new messages within 50% of the response time limit.

What if the information about read/unread messages would be eventually consistent?  
In other words, it would be reasonable to receive reading acknowledgment after a certain delay.  
In that case, it’s safe to expect a considerable number of tickets to be unnecessarily reassigned.  
That, of course, would corrupt the system’s state.  
Therefore, the data in the messages belongs to the aggregate’s boundary.

## The aggregate root

We saw earlier that an aggregate’s state can only be modified by executing one of its commands.  
Since an aggregate represents a hierarchy of entities,  
Only one of them should be designated as the aggregate’s public interface—the aggregate root.

Consider the following excerpt of the `Ticket` aggregate:

```cs
public class Ticket
{
    private List<Message> _messages;

    public void Execute(AcknowledgeMessage cmd)
    {
        var message = _messages.Where(x => x.Id == cmd.id).First();
        message.WasRead = true;
    }
}
```

In this example, the aggregate exposes a command that allows marking a specific message as read.  
Although the operation modifies an instance of the Message entity, it is accessible only through its aggregate root: Ticket.

In addition to the aggregate root’s public interface,  
There is another mechanism through which the outer world can communicate with aggregates: domain events.

## Ubiquitous language

Last but not least, aggregates should reflect the ubiquitous language.  
The terminology that is used for the aggregate’s name, its data members, its actions, and its domain events all should be formulated in the bounded context’s ubiquitous language.

As Eric Evans put it, the code must be based on the same language the developers use when they speak with one another and with domain experts.

This is especially important for implementing complex business logic.  
Now let’s take a look at the third and final building block of a domain model.
