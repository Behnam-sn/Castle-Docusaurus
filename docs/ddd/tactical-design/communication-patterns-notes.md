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
