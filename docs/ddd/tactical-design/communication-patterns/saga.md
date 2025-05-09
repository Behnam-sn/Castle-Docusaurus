---
sidebar_position: 3
---

# Saga

One of the core aggregate design principles,  
Is to limit each transaction to a single instance of an aggregate.

This ensures that an aggregate’s boundaries are carefully considered,  
And encapsulate a coherent set of business functionality.

But there are cases when you have to implement a business process that spans multiple aggregates.  
Consider the following example:

when an advertising campaign is activated,  
It should automatically submit the campaign’s advertising materials to its publisher.  
Upon receiving the confirmation from the publisher,  
The campaign’s publishing state should change to `Published`.  
In the case of rejection by the publisher, the campaign should be marked as `Rejected`.

This flow spans two business entities:  
advertising campaign and publisher.

Co-locating the entities in the same aggregate boundary would definitely be overkill,  
as these are clearly different business entities that have different responsibilities  
And may belong to different bounded contexts.  
Instead, this flow can be implemented as a **Saga**.

A saga is a long-running business process.
It’s long running not necessarily in terms of time,  
As sagas can run from seconds to years,  
But rather in terms of transactions:  
A business process that spans multiple transactions.

The transactions can be handled not only by aggregates,  
But by any component emitting domain events and responding to commands.

The saga listens to the events emitted by the relevant components  
And issues subsequent commands to the other components.

If one of the execution steps fails,  
The saga is in charge of issuing relevant compensating actions to ensure the system state remains consistent.

Let’s see how the advertising campaign publishing flow from the preceding example can be implemented as a saga.

To implement the publishing process,  
The saga has to listen to,  
The `CampaignActivated` event from the Campaign aggregate,  
And the `PublishingConfirmed` and `PublishingRejected` events from the `AdPublishing` bounded context.

The saga has to execute the `SubmitAdvertisement` command on `AdPublishing`,  
And the Track `PublishingConfirmation` and `TrackPublishingRejection` commands on the `Campaign` aggregate.

In this example,  
The `TrackPublishingRejection` command acts as a compensation action,  
That will ensure that the advertising campaign is not listed as active.

Here is the code:

```cs
public class CampaignPublishingSaga
{
    private readonly ICampaignRepository _repository;
    private readonly IPublishingServiceClient _publishingService;

    public void Process(CampaignActivated @event)
    {
        var campaign = _repository.Load(@event.CampaignId);
        var advertisingMaterials = campaign.GenerateAdvertisingMaterials();
        _publishingService.SubmitAdvertisement(@event.CampaignId, advertisingMaterials);
    }

    public void Process(PublishingConfirmed @event)
    {
        var campaign = _repository.Load(@event.CampaignId);
        campaign.TrackPublishingConfirmation(@event.ConfirmationId);
        _repository.CommitChanges(campaign);
    }

    public void Process(PublishingRejected @event)
    {
        var campaign = _repository.Load(@event.CampaignId);
        campaign.TrackPublishingRejection(@event.RejectionReason);
        _repository.CommitChanges(campaign);
    }
}
```

The preceding example relies on the messaging infrastructure to deliver the relevant events,  
And it reacts to the events by executing the relevant commands.

This is an example of a relatively simple saga: it has no state.

You will encounter sagas that do require state management;  
For example, to track the executed operations so that relevant compensating actions can be issued in case of a failure.

In such a situation, the saga can be implemented as an event-sourced aggregate,  
Persisting the complete history of received events and issued commands.

However, the command execution logic should be moved out of the saga itself,  
And executed asynchronously,  
Similar to the way domain events are dispatched in the outbox pattern:

```cs
public class CampaignPublishingSaga
{
    private readonly ICampaignRepository _repository;
    private readonly IList<IDomainEvent> _events;

    public void Process(CampaignActivated activated)
    {
        var campaign = _repository.Load(activated.CampaignId);
        var advertisingMaterials = campaign.GenerateAdvertisingMaterials);
        var commandIssuedEvent = new CommandIssuedEvent(
            target: Target.PublishingService,
            command: new SubmitAdvertisementCommand(activated.CampaignId, advertisingMaterials));

        _events.Append(activated);
        _events.Append(commandIssuedEvent);
    }

    public void Process(PublishingConfirmed confirmed)
    {
        var commandIssuedEvent = new CommandIssuedEvent(
            target: Target.CampaignAggregate,
            command: new TrackConfirmation(confirmed.CampaignId, confirmed.ConfirmationId));

        _events.Append(confirmed);
        _events.Append(commandIssuedEvent);
    }

    public void Process(PublishingRejected rejected)
    {
        var commandIssuedEvent = new CommandIssuedEvent(
            target: Target.CampaignAggregate,
            command: new TrackRejection(rejected.CampaignId, rejected.RejectionReason));

        _events.Append(rejected);
        _events.Append(commandIssuedEvent);
    }
}
```

In this example,  
The outbox relay will have to execute the commands on relevant endpoints for each instance of `CommandIssuedEvent`.

As in the case of publishing domain events,  
separating the transition of the saga’s state from the execution of commands,  
Ensures that the commands will be executed reliably,  
Even if the process fails at any stage.

## Consistency

Although the saga pattern orchestrates a multi-component transaction,  
The states of the involved components are eventually consistent.  
And although the saga will eventually execute the relevant commands,  
No two transactions can be considered atomic.

This correlates with another aggregate design principle:  
_Only the data within an aggregate’s boundaries can be considered strongly consistent._  
_Everything outside is eventually consistent._

Use this as a guiding principle to make sure you are not abusing sagas to compensate for improper aggregate boundaries.

Business operations that have to belong to the same aggregate require strongly consistent data.

The saga pattern is often confused with another pattern: process manager.  
Although the implementation is similar, these are different patterns.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
