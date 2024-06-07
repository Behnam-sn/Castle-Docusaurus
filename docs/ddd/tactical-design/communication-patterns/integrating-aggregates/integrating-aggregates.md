---
sidebar_position: 2
---

# Integrating Aggregates

One of the ways aggregates communicate with the rest of the system is by publishing domain events.  
External components can subscribe to these domain events and execute their logic.

But how are domain events published to a message bus?

Before we get to the solution,  
Let’s examine a few common mistakes in the event publishing process and the consequences of each approach.

Consider the following code:

```cs
public class Campaign
{
    private readonly List<DomainEvent> _events;
    private readonly IMessageBus _messageBus;

    public void Deactivate(string reason)
    {
        for (l in _locations.Values())
        {
            l.Deactivate();
        }

        IsActive = false;

        var newEvent = new CampaignDeactivated(_id, reason);
        _events.Append(newEvent);
        _messageBus.Publish(newEvent);
    }
}
```

On line 17, a new event is instantiated.  
On the following two lines, it is appended to the aggregate’s internal list of domain events (line 18),  
And the event is published to the message bus (line 19).

This implementation of publishing domain events is simple but wrong.

Publishing the domain event right from the aggregate is bad for two reasons.

First, the event will be dispatched before the aggregate’s new state is committed to the database.  
A subscriber may receive the notification that the campaign was deactivated, but it would contradict the campaign’s state.

Second, what if the database transaction fails to commit because of a race condition, subsequent aggregate logic rendering the operation invalid, or simply a technical issue in the database?

Even though the database transaction is rolled back, the event is already published and pushed to subscribers, and there is no way to retract it.

Let’s try something else:

```cs
public class ManagementAPI
{
    private readonly IMessageBus _messageBus;
    private readonly ICampaignRepository _repository;

    public ExecutionResult DeactivateCampaign(CampaignId id, string reason)
    {
        try
        {
            var campaign = repository.Load(id);
            campaign.Deactivate(reason);
            _repository.CommitChanges(campaign);

            var events = campaign.GetUnpublishedEvents();
            for (IDomainEvent e in events)
            {
                _messageBus.publish(e);
            }
            campaign.ClearUnpublishedEvents();
        }
        catch(Exception ex)
        {
        }
    }
}
```

In the preceding listing,  
The responsibility of publishing new domain events is shifted to the application layer.

On lines 11 through 13, the relevant instance of the Campaign
aggregate is loaded, its Deactivate command is executed, and only after the updated
state is successfully committed to the database, on lines 15 through 20, are the new
domain events published to the message bus. Can we trust this code? No.

In this case,  
The process running the logic for some reason fails to publish the domain events.  
Perhaps the message bus is down.  
Or the server running the code fails right after committing the database transaction,  
But before publishing the events the system will still end in an inconsistent state,  
Which means that the database transaction is committed,  
But the domain events will never be published.

These edge cases can be addressed using the outbox pattern.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
