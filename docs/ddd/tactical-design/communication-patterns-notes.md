# Communication Patterns Notes

## What are Communication Patterns?

Up this point you learn about,  
Tactical design patterns that define the different ways to implement a system’s components:

- How to model the business logic
- And how to organize the internals of a bounded context architecturally

In this chapter,  
We will step beyond the boundaries of a single component,  
And discuss the patterns for organizing the flow of communication across a system’s elements.

The patterns you will learn about in this chapter facilitate cross-bounded context communication,  
Address the limitations imposed by aggregate design principles,  
And orchestrate business processes spanning multiple system components.

## Model Translation

A bounded context is the boundary of a model (and it's ubiquitous language).

As you learned previously,  
There are different patterns for designing communication across different bounded contexts.

Suppose the teams implementing two bounded contexts are communicating effectively and willing to collaborate.  
In this case, the bounded contexts can be integrated in a partnership:  
The protocols can be coordinated in an ad hoc manner,  
And any integration issues can be effectively addressed through communication between the teams.

Another cooperation-driven integration method is shared kernel:  
The teams extract and co-evolve a limited portion of a model;  
For example, extracting the bounded contexts’ integration contracts into a co-owned repository.

In a customer–supplier relationship,  
The balance of power tips toward either the upstream (supplier) or the downstream (consumer) bounded context.

Suppose the downstream bounded context cannot conform to the upstream bounded context’s model.  
In this case,  
A more elaborate technical solution is required,  
That can facilitate communication,  
By translating the bounded contexts’ models.

This translation can be handled by one, or sometimes both, sides:

- The downstream bounded context can adapt the upstream bounded context’s model to its needs using an anticorruption layer (ACL),
- While the upstream bounded context can act as an open-host service (OHS)  
  And protect its consumers from changes to its implementation model by using an integration-specific published language.

Since the translation logic is similar for both the anticorruption layer and the open-host service,  
This chapter covers the implementation options without differentiating between the patterns and mentions the differences only in exceptional cases.

The model’s translation logic can be either stateless or stateful.  
Stateless translation happens on the fly, as incoming (OHS) or outgoing (ACL) requests are issued,  
While stateful translation involves a more complicated translation logic that requires a database.

Let’s see design patterns for implementing both types of model translation.

### Stateless Model Translation

For stateless model translation,  
The bounded context that owns the translation (OHS for upstream, ACL for downstream)  
Implements the proxy design pattern to interject the incoming and outgoing requests and map the source model to the bounded context’s target model.

Implementation of the proxy depends on whether the bounded contexts are communicating synchronously or asynchronously.

#### Synchronous

The typical way to translate models used in synchronous communication,  
Is to embed the transformation logic in the bounded context’s codebase.

In an open-host service,  
Translation to the public language takes place when processing incoming requests,  
And in an anticorruption layer,  
It occurs when calling the upstream bounded context.

In some cases,  
It can be more cost-effective and convenient,  
To offload the translation logic,  
To an external component such as an API gateway pattern.

The API gateway component can be an open source software-based solution,  
such as Kong or KrakenD,  
Or it can be a cloud vendor’s managed service such as AWS API Gateway, Google Api, gee or Azure API Management.

For bounded contexts implementing the open-host pattern,  
The API gateway is responsible for converting the internal model into the integration-optimized published language.

Moreover, having an explicit API gateway can alleviate the process of managing and serving multiple versions of the bounded context’s API.

Anticorruption layers implemented using an API gateway can be consumed by multiple downstream bounded contexts.  
In such cases, the anticorruption layer acts as an integration-specific bounded context.

Such bounded contexts,  
Which are mainly in charge of transforming models for more convenient consumption by other components,  
Are often referred to as _interchange contexts_.

#### Asynchronous

To translate models used in asynchronous communication you can implement a _message proxy_:  
An intermediary component subscribing to messages coming from the source bounded context.

The proxy will apply the required model transformations and forward the resultant messages to the target subscriber.

In addition to translating the messages’ model,  
The intercepting component can also reduce the noise on the target bounded context by filtering out irrelevant messages.

Asynchronous model translation is essential when implementing an open host service.

It’s a common mistake to design and expose a published language for the model’s objects,  
And allow domain events to be published as they are,  
Thereby exposing the bounded context’s implementation model.

Asynchronous translation can be used to intercept the domain events and convert them into a published language,  
Thus providing better encapsulation of the bounded context’s implementation details.

Moreover, translating messages to the published language,  
Enables differentiating between,  
Private events that are intended for the bounded context’s internal needs,  
And public events that are designed for integration with other bounded contexts.

### Stateful Model Translation

For more significant model transformations—for example,  
When the translation mechanism has to aggregate the source data,  
Or unify data from multiple sources into a single model,  
A stateful translation may be required.

Let’s discuss each of these use cases in detail.

#### Aggregating incoming data

Let’s say a bounded context is interested in aggregating incoming requests,  
And processing them in batches for performance optimization.

In this case,  
Aggregation may be required both for synchronous and asynchronous requests.

Another common use case for aggregation of source data is combining multiple fine-grained messages into a single message containing the unified data.

Model transformation that aggregates incoming data cannot be implemented using an API gateway,  
And thus requires more elaborate, stateful processing.

To track the incoming data and process it accordingly,  
The translation logic requires its own persistent storage.

In some use cases,  
You can avoid implementing a custom solution for a stateful translation,  
By using off-the-shelf products;  
For example,  
A stream-process platform (Kafka, AWS Kinesis, etc.),  
Or a batching solution (Apache NiFi, AWS Glue, Spark, etc.).

#### Unifying multiple sources

A bounded context may need to process data aggregates from multiple sources,  
Including other bounded contexts.

A typical example for this is the backend-for-frontend pattern,  
In which the user interface has to combine data originating from multiple services.

Another example is a bounded context that must process data from multiple other contexts,  
And implement complex business logic to process all the data.

In this case,  
It can be beneficial to decouple the integration and business logic complexities,  
By fronting the bounded context with an anticorruption layer,  
That aggregates data from all other bounded contexts.

## Integrating Aggregates

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

### Outbox

The outbox pattern ensures reliable publishing of domain events using the following algorithm:

- Both the updated aggregate’s state and the new domain events are committed in the same atomic transaction.
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

#### Fetching unpublished events

The publishing relay can fetch the new domain events in either a pull-based or push-based manner:

- Pull: polling publisher  
  The relay can continuously query the database for unpublished events.  
  Proper indexes have to be in place to minimize the load on the database induced by the constant polling.

- Push: transaction log tailing  
  Here we can leverage the database’s feature set to proactively call the publishing relay when new events are appended.  
  For example, some relational databases enable getting notifications about updated/inserted records by tailing the database’s transaction log.  
  Some NoSQL databases expose committed changes as streams of events (e.g., AWS DynamoDB Streams).

It’s important to note that the outbox pattern guarantees delivery of the messages at least once:  
If the relay fails right after publishing a message but before marking it as published in the database,  
The same message will be published again in the next iteration.

Next, we’ll take a look at how we can leverage the reliable publishing of domain events to overcome some of the limitations imposed by aggregate design principles.

### Saga

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

#### Consistency

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

### Process Manager

The saga pattern manages simple, linear flow.  
Strictly speaking, a saga matches events to the corresponding commands.

In the examples we used to demonstrate saga implementations,  
We actually implemented simple matching of events to commands:

- `CampaignActivated` event to `PublishingService.SubmitAdvertisement` command
- `PublishingConfirmed` event to `Campaign.TrackConfirmation` command
- `PublishingRejected` event to `Campaign.TrackRejection` command

The process manager pattern,  
Is intended to implement a business-logic-based process.

It is defined as a central processing unit,  
That maintains the state of the sequence and determines the next processing steps.

As a simple rule of thumb,  
If a saga contains if-else statements to choose the correct course of action,  
It is probably a process manager.

Another difference between a process manager and a saga is,  
That a saga is instantiated implicitly when a particular event is observed,
As in `CampaignActivated` in the preceding examples.

A process manager, on the other hand, cannot be bound to a single source event.  
Instead, it’s a coherent business process consisting of multiple steps.

Hence, a process manager has to be instantiated explicitly.  
Consider the following example:

- Booking a business trip starts with the routing algorithm choosing the most cost effective flight route,  
  And asking the employee to approve it.
- In case the employee prefers a different route,  
  Their direct manager needs to approve it.
- After the flight is booked,  
  One of the pre-approved hotels has to be booked for the appropriate dates.
- If no hotels are available,  
  The flight tickets have to be canceled.

In this example, there is no central entity to trigger the trip booking process.  
The trip booking is the process and it has to be implemented as a process manager.

From an implementation perspective,  
Process managers are often implemented as aggregates,  
Either state based or event sourced.  
For example:

```cs
public class BookingProcessManager
{
    private readonly IList<IDomainEvent> _events;
    private BookingId _id;
    private Destination _destination;
    private TripDefinition _parameters;
    private EmployeeId _traveler;
    private Route _route;
    private IList<Route> _rejectedRoutes;
    private IRoutingService _routing;

    public void Initialize(Destination destination, TripDefinition parameters, EmployeeId traveler)
    {
        _destination = destination;
        _parameters = parameters;
        _traveler = traveler;
        _route = _routing.Calculate(destination, parameters);

        var routeGenerated = new RouteGeneratedEvent(
            BookingId: _id,
            Route: _route);

        var commandIssuedEvent = new CommandIssuedEvent(
            command: new RequestEmployeeApproval(_traveler, _route)
        );

        _events.Append(routeGenerated);
        _events.Append(commandIssuedEvent);
    }

    public void Process(RouteConfirmed confirmed)
    {
        var commandIssuedEvent = new CommandIssuedEvent(
            command: new BookFlights(_route, _parameters)
        );

        _events.Append(confirmed);
        _events.Append(commandIssuedEvent);
    }

    public void Process(RouteRejected rejected)
    {
        var commandIssuedEvent = new CommandIssuedEvent(
            command: new RequestRerouting(_traveler, _route)
        );

        _events.Append(rejected);
        _events.Append(commandIssuedEvent);
    }

    public void Process(ReroutingConfirmed confirmed)
    {
        _rejectedRoutes.Append(route);
        _route = _routing.CalculateAltRoute(destination,
                                            parameters, rejectedRoutes);
        var routeGenerated = new RouteGeneratedEvent(
            BookingId: _id,
            Route: _route);

        var commandIssuedEvent = new CommandIssuedEvent(
            command: new RequestEmployeeApproval(_traveler, _route)
        );

        _events.Append(confirmed);
        _events.Append(routeGenerated);
        _events.Append(commandIssuedEvent);
    }

    public void Process(FlightBooked booked)
    {
        var commandIssuedEvent = new CommandIssuedEvent(
            command: new BookHotel(_destination, _parameters)
        );

        _events.Append(booked);
        _events.Append(commandIssuedEvent);
    }
}
```

In this example, the process manager has its explicit ID and persistent state,
describing the trip that has to be booked.

As in the earlier example of a saga pattern,  
The process manager subscribes to events that control the workflow,
(RouteConfirmed, RouteRejected, ReroutingConfirmed, etc.),

and it instantiates events of type `CommandIssuedEvent` that will be processed by an outbox relay to execute the actual commands.

## Conclusion

In this chapter, you learned the different patterns for integrating a system’s components.

The chapter began by exploring patterns for model translations that can be used to implement anticorruption layers or open-host services.

We saw that translations can be handled on the fly or can follow a more complex logic, requiring state tracking.

The outbox pattern is a reliable way to publish aggregates’ domain events.
It ensures that domain events are always going to be published, even in the face of different process failures.

The saga pattern can be used to implement simple cross-component business pro‐
cesses. More complex business processes can be implemented using the process man‐
ager pattern. Both patterns rely on asynchronous reactions to domain events and the
issuing of commands.
