---
sidebar_position: 3
---

# Concurrency Management

## What

Concurrency management ensures,  
Correct results for concurrent operations are generated,  
While getting those results as quickly as possible.

## Problem

If operations are executed sequentially,  
With no overlap in time, no concurrency exists.

But high-performance systems need to run operations concurrently to meet their performance requirements.

Concurrency is quite easy if all operations are just reading data.  
There is no way operations can interfere with one another.

However,  
Any system has a mix of READ and WRITE operations.

If concurrency is allowed in an uncontrolled manner,  
Some unexpected, undesirable results may occur, such as:

- ### The Lost Update Problem

  An update done to a data by an operation is lost,
  As it is overwritten by the update done by another operation.

- ### The Dirty Read Problem

  Operations read a value written by an operation that has been later aborted.

  This value disappears upon abort,  
  And should not have been read by any operation.

- ### The Incorrect Summary Problem

- ### Race Condition

  When two operations are updating the same data,  
  At the same time.

:::warning
Race condition needs more research.
:::

Example:

Two people try to buy the movie ticket for the same movie and for the same seat at the same time online.

Without concurrency control,  
It is possible that both people will end up purchasing the ticket.

maybe: Wikipedia bank example?

## Solution

Concurrency management provides,  
Rules, methods, design methodologies, and theories,  
To maintain the consistency of components operating concurrently, while interacting.

And thus keeping the consistency and correctness of the whole system.

There are two main types of concurrency management:

- ### Optimistic

  Optimistic concurrency,  
  Assumes multiple operations can frequently complete,  
  Without interfering with each other.

- ### Pessimistic

  Pessimistic concurrency,  
  Assumes conflicts between operations can happen often.

:::note
Applying concurrency management into a system typically result in some performance reduction.
:::

## References

- [en.wikipedia.org/wiki/Concurrency_control](https://en.wikipedia.org/wiki/Concurrency_control)
- [ibm.com/docs/en/was/8.5.5?topic=beans-concurrency-control](https://www.ibm.com/docs/en/was/8.5.5?topic=beans-concurrency-control)
- [tutorialspoint.com/what-is-concurrency-control-in-dbms](https://www.tutorialspoint.com/what-is-concurrency-control-in-dbms)
- [geeksforgeeks.org/concurrency-problems-in-dbms-transactions/](https://www.geeksforgeeks.org/concurrency-problems-in-dbms-transactions/)
- [ibm.com/docs/en/db2/11.1?topic=design-concurrency-issues](https://www.ibm.com/docs/en/db2/11.1?topic=design-concurrency-issues)
- [gatevidyalay.com/concurrency-problems-in-transaction/](https://www.gatevidyalay.com/concurrency-problems-in-transaction/)
