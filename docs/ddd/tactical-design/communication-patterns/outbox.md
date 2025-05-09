---
sidebar_position: 2
---

# Outbox

## What is Outbox Pattern?

## What Problem Outbox Pattern is Trying to Solve?

One of the ways aggregates communicate with the rest of the system is by publishing domain events.

External components can subscribe to these domain events and execute their logic.

But how are domain events published to a message bus?

Before we get to the solution,  
Let’s examine a few common mistakes in the event publishing process,  
And the consequences of each approach.

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
On the following two lines,  
It is appended to the aggregate’s internal list of domain events (line 18),  
And the event is published to the message bus (line 19).

This implementation of publishing domain events is simple but wrong.

Publishing the domain event right from the aggregate is bad for two reasons:

- First, the event will be dispatched before the aggregate’s new state is committed to the database.  
  A subscriber may receive the notification that the campaign was deactivated,  
  But it would contradict the campaign’s state.

- Second, what if the database transaction fails to commit,  
  Because of a race condition,  
  Subsequent aggregate logic rendering the operation invalid,  
  Or simply a technical issue in the database?

  Even though the database transaction is rolled back,  
  The event is already published and pushed to subscribers,  
  And there is no way to retract it.

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

On lines 11 through 13,  
The relevant instance of the Campaign aggregate is loaded,  
Its Deactivate command is executed,  
And only after the updated state is successfully committed to the database,  
On lines 15 through 20,  
Are the new domain events published to the message bus.

Can we trust this code? No.

In this case,  
The process running the logic for some reason fails to publish the domain events.

Perhaps the message bus is down.  
Or the server running the code fails right after committing the database transaction.

But before publishing the events the system will still end in an inconsistent state.

Which means that the database transaction is committed,  
But the domain events will never be published.

These edge cases can be addressed using the outbox pattern.

## What is Outbox Pattern Solution?

The outbox pattern ensures reliable publishing of domain events using the following algorithm:

- Both the updated aggregate’s state,  
  And the new domain events,  
  Are committed in the same atomic transaction.

- A message relay fetches newly committed domain events from the database.

- The relay publishes the domain events to the message bus.

- Upon successful publishing,  
  The relay either marks the events as published in the database,  
  Or deletes them completely.

When using a relational database,  
It’s convenient to leverage the database’s ability to commit to two tables atomically,  
And use a dedicated table for storing the messages.

When using a NoSQL database that doesn’t support multi-document transactions,  
The outgoing domain events have to be embedded in the aggregate’s record.  
For example:

```json
{
  "campaign-id": "364b33c3-2171-446d-b652-8e5a7b2be1af",
  "state": {
    "name": "Autumn 2017",
    "publishing-state": "DEACTIVATED",
    "ad-locations": []
  },
  "outbox": [
    {
      "campaign-id": "364b33c3-2171-446d-b652-8e5a7b2be1af",
      "type": "campaign-deactivated",
      "reason": "Goals met",
      "published": false
    }
  ]
}
```

In this sample,  
You can see the JSON document’s additional property,  
Outbox, containing a list of domain events that have to be published.

## Fetching unpublished events

The publishing relay can fetch the new domain events in either a pull-based or push-based manner:

- Pull: polling publisher  
  The relay can continuously query the database for unpublished events.

  Proper indexes have to be in place to minimize the load on the database induced by the constant polling.

- Push: transaction log tailing  
  Here we can leverage the database’s feature set to proactively call the publishing relay when new events are appended.

  For example,  
  Some relational databases enable getting notifications about updated/inserted records,  
  By tailing the database’s transaction log.  
  Some NoSQL databases expose committed changes as streams of events (e.g., AWS DynamoDB Streams).

It’s important to note that the outbox pattern guarantees delivery of the messages at least once:  
If the relay fails right after publishing a message,  
But before marking it as published in the database,  
The same message will be published again in the next iteration.

Next we’ll take a look at how we can leverage the reliable publishing of domain events,  
To overcome some of the limitations imposed by aggregate design principles.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
