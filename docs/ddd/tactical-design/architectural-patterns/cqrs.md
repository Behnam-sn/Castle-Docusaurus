---
sidebar_position: 3
---

# CQRS

## What is CQRS Pattern?

The command-query responsibility segregation (CQRS) pattern,  
Is based on the same organizational principles,  
For business logic and infrastructural concerns as ports & adapters.

It differs however,  
In the way the system’s data is managed.

This pattern enables representation of the system’s data in multiple persistent models.

<!-- CQRS allows the use of multiple storage mechanisms for representing different models of the system’s data. -->

## What Problem CQRS Pattern is Trying to Solve?

### Polyglot Modeling

In many cases,  
It may be difficult,  
If not impossible,  
To use a single model of the system’s business domain,  
To address all of the system’s needs.

For example, as discussed previously,  
Online transaction processing (OLTP) and online analytical processing (OLAP),  
May require different representations of the system’s data.

Another reason for working with multiple models may have to do with the notion of polyglot persistence.

There is no perfect database.  
Or as Greg Young says:  
All databases are flawed, each in its own way.

We often have to balance the needs for scale, consistency, or supported querying models.

An alternative to finding a perfect database is the polyglot persistence model.  
That is using multiple databases,  
To implement different data-related requirements.

For example:

- A single system might use a document store as its operational database
- A column store for analytics/reporting
- And a search engine for implementing robust search capabilities

### Event Sourcing

The CQRS pattern is closely related to event sourcing.

Originally, CQRS was defined to address the limited querying possibilities of an event-sourced model.  
Which is, it is only possible to query events of one aggregate instance at a time.

The CQRS pattern provides the possibility of materializing projected models into physical databases,  
That can be used for flexible querying options.

<!-- In the CQRS architecture,
The responsibilities of the system’s models are segregated according to their type:

- A command can only operate on the strongly consistent command execution model.
- A query cannot directly modify any of the system’s persisted state,
  Neither the read models nor the command execution model. -->

## What is CQRS Pattern Solution?

As the name suggests,  
The pattern segregates the responsibilities of the system’s models:

### Command Execution Model

CQRS devotes a single model to executing operations,  
That modify the system’s state.

This model is used to:

- Implement the business logic
- Validate rules
- And enforce invariants

The command execution model,  
Is also the only model representing strongly consistent data.  
(The system’s source of truth)

It should be possible to read the strongly consistent state of a business entity,  
And have optimistic concurrency support when updating it.

### Read Models (Projections)

The system can define as many models as needed,  
To present data to users,  
Or supply information to other systems.

A read model is a pre-cached projection.  
It can reside in a durable database, flat file, or in-memory cache.

Proper implementation of CQRS,  
Allows for wiping out all data of a projection and regenerating it from scratch.

This also enables extending the system with additional projections in the future;  
For models that couldn’t have been foreseen originally.

Finally, read models are read-only.  
None of the system’s operations can directly modify the read models’ data.

## How to Project Read Models?

For the read models to work,  
The system has to project changes from the command execution model,  
To all its read models.

The projection of read models,  
Is similar to the notion of a materialized view in relational databases:  
Whenever source tables are updated,  
The changes have to be reflected in the pre-cached views.

Let’s see two ways to generate projections:

### Synchronous Projections

Synchronous projections fetch changes to the OLTP data through the catch-up subscription model:

- The projection engine queries the OLTP database for added or updated records after the last processed checkpoint.

- The projection engine uses the updated data to regenerate/update the system’s read models.

- The projection engine stores the checkpoint of the last processed record.  
  This value will be used during the next iteration for getting records added or modified after the last processed record.

For the catch-up subscription to work,  
The command execution model has to checkpoint all the appended or updated database records.

The storage mechanism should also support the querying of records based on the checkpoint:

- The checkpoint can be implemented using the databases’ features.  
  For example, SQL Server’s “rowversion” column can be used to generate unique,  
  Incrementing numbers upon inserting or updating a row.

- In databases that lack such functionality,  
  A custom solution can be implemented that increments a running counter and appends it to each modified record.

<!-- It’s important to ensure that the checkpoint-based query returns consistent results.
Otherwise, these records will be skipped by the projection engine,
Which will result in inconsistent models. -->

The synchronous projection method makes it trivial,  
To add new projections and regenerate existing ones from scratch.

For regenerating projections,  
All you have to do is reset the checkpoint to 0;  
The projection engine will scan the records and rebuild the projections from the ground up.

### Asynchronous Projections

In the asynchronous projection scenario,  
The command execution model publishes all committed changes to a message bus.

The system’s projection engines can subscribe to the published messages and use them to update the read models.

#### Challenges

Despite the apparent scaling and performance advantages of the asynchronous projection method,  
It is more prone to the challenges of distributed computing.

If the messages are processed out of order or duplicated,  
Inconsistent data will be projected into the read models.

This method also makes it more challenging to add new projections or regenerate existing ones.

For these reasons,  
It’s advisable to always implement synchronous projection,  
And optionally, an additional asynchronous projection on top of it.

## Can Command Execution Models Return Any Data?

A common misconception about CQRS-based systems is,  
That a command can only modify data,  
And data can be fetched for display only through a read model.

In other words, the command executing the methods should never return any data.

This is wrong.  
This approach produces accidental complexities and leads to a bad user experience.

A command should always let the caller know whether it has succeeded or failed.  
If it has failed, why did it fail?  
Was there a validation or technical issue?  
The caller has to know how to fix the command.

Therefore, a command can (and in many cases should) return data;  
For example, if the system’s user interface has to reflect the modifications resulting from the command.

This make it easier for consumers to work with the system,  
Since they immediately receive feedback for their actions,

Also the returned values can be used further in the consumers workflows,  
Eliminating the need for unnecessary data round trips.

The only limitation here is that the returned data,  
Should originate from the strongly consistent model (the command execution model),  
As we cannot expect the projections (which will eventually be consistent) to be refreshed immediately.

## When to Use CQRS Pattern?

The CQRS pattern can be useful for applications that need to work with the same data in multiple models,  
Potentially stored in different kinds of databases.

From an operational perspective,  
The pattern supports domain-driven design’s core value of working with the most effective models for the task at hand,  
And continuously improving the model of the business domain.

From an infrastructural perspective,  
CQRS allows for leveraging the strength of the different kinds of databases;  
For example:

- Using a relational database to store the command execution model
- A search index for full text search
- And pre-rendered flat files for fast data retrieval

With all the storage mechanisms reliably synchronized.

Moreover, CQRS naturally lends itself to event-sourced domain models.

The event sourcing model makes it impossible to query records based on the aggregates’ states,  
But CQRS enables this by projecting the states into queryable databases.

## References

- Learning Domain-Driven Design - Vladik Khononov - O'Reilly
