---
sidebar_position: 1
---

# Outbox

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

## Fetching unpublished events

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

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
