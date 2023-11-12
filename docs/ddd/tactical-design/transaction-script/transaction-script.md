---
sidebar_position: 1
---

# Transaction Script

This pattern organizes the system’s operations as simple, straightforward procedural scripts.  
The procedures ensure that each operation is transactional (either it succeeds or it fails).

The transaction script pattern lends itself to supporting subdomains, with business logic resembling simple, ETL-like operations.

## What Is Transaction Script Pattern?

> Organizes business logic by procedures where each procedure handles a single request from the presentation.  
> — Martin Fowler

A system’s public interface can be seen as a collection of business transactions that consumers can execute.  
These transactions can retrieve information managed by the system, modify it, or both.

The pattern organizes the system’s business logic based on procedures,  
where each procedure implements an operation that is executed by the system’s consumer via its public interface.

In effect, the system’s public operations are used as encapsulation boundaries.

## How to Implement Transaction Script Pattern?

Each procedure is implemented as a simple, straightforward procedural script.  
The only requirement procedures have to fulfill is transactional behavior:

_Each operation should either succeed or fail but can never result in an invalid state._

Even if execution of a transaction script fails at the most inconvenient moment,  
The system should remain consistent.  
Either by rolling back any changes it has made up until the failure or by executing compensating actions.

The transactional behavior is reflected in the pattern’s name:  
Transaction Script

It can use a thin abstraction layer for integrating with storage mechanisms,  
But it is also free to access the databases directly.

Here is an example of a transaction script that converts batches of JSON files into XML files:

```cs
DB.StartTransaction();
var job = DB.LoadNextJob();
var json = LoadFile(job.Source);
var xml = ConvertJsonToXml(json);
WriteFile(job.Destination, xml.ToString();
DB.MarkJobAsCompleted(job);
DB.Commit()
```

## What are Challenges Transaction Script Pattern?

The transaction script pattern is a foundation for the more advanced business logic implementation patterns.  
Furthermore, despite its apparent simplicity, it is the easiest pattern to get wrong.

A considerable number of production issues I have helped to debug and fix, in one way or another, often boiled down to a misimplementation of the transactional behavior of the system’s business logic.

Let’s take a look at three common, real-life examples of data corruption that results from failing to correctly implement a transaction script:

- Lack of Transactional Behavior
- Distributed Transactions
- Implicit Distributed Transactions

## When to Use Transaction Script Pattern?

The transaction script pattern is well adapted to the most straightforward problem domains in which the business logic resembles simple procedural operations.

For example, in extract-transform-load (ETL) operations, each operation extracts data from a source, applies transformation logic to convert it into another form, and loads the result into the destination store.

The transaction script pattern naturally fits supporting subdomains where, by definition, the business logic is simple.  
It can also be used as an adapter for integration with external systems.  
For example, generic subdomains, or as a part of an anticorruption layer.

The main advantage of the transaction script pattern is its simplicity.  
It introduces minimal abstractions and minimizes the overhead both in runtime performance and in understanding the business logic.

That said, this simplicity is also the pattern’s disadvantage.  
The more complex the business logic gets, the more it’s prone to duplicate business logic across transactions, and consequently, to result in inconsistent behavior—when the duplicated code goes out of sync.  
As a result, transaction script should never be used for core subdomains, as this pattern won’t cope with the high complexity of a core subdomain’s business logic.

This simplicity earned the transaction script a dubious reputation.  
Sometimes the pattern is even treated as an antipattern.  
After all, if complex business logic is implemented as a transaction script, sooner rather than later it’s going to turn into an unmaintainable, big ball of mud.

It should be noted, however, that despite the simplicity, the transaction script pattern is ubiquitous in software development.  
All the business logic implementation patterns that we will discuss in this and the following chapters, in one way or another, are based on the transaction script pattern.
