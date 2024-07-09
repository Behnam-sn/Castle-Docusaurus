---
sidebar_position: 1
---

# Optimistic Concurrency

## What is Optimistic Concurrency?

Optimistic concurrency is a concurrency management approach.

Optimistic concurrency,  
Assumes multiple operations can frequently complete,  
Without interfering with each other.

Optimistic concurrency is used in transactional systems, such as:

- Relational database management systems
- Software transactional memory

## How does Optimistic Concurrency Work?

We can easily achieve optimistic concurrency,  
By using a timestamp or a version number.

:::warning
Todo: timestamp

Todo: version number
:::

In optimistic concurrency:

- Operations use data resources without acquiring locks on those resources.

- But before committing,  
  Each operation verifies that no other operation has modified the version number or the timestamp it has read.

- If the check reveals conflict,  
  The committing operation rolls back and can be restarted.

## When to Use Optimistic Concurrency?

Optimistic concurrency approach is generally used in environments with low data confliction.

When conflicts are rare,
The number of rollbacks required and the total cost of rollbacks is low.

Operations can complete without the expense of managing locks,  
And without having operations wait for other operations' locks to clear.

This leads to higher output than other concurrency control methods.

However,  
If confliction for data resources is frequent,  
The cost of repeatedly restarting operations hurts performance significantly.

In which case other concurrency control methods may be better suited.

Keep in mind,  
Locking-based (pessimistic) methods also can deliver poor performance,  
Because locking can drastically limit effective concurrency.

## References

- [en.wikipedia.org/wiki/Optimistic_concurrency_control](https://en.wikipedia.org/wiki/Optimistic_concurrency_control)
- [cult.honeypot.io/reads/optimistic-vs-pessimistic-concurrency/](https://cult.honeypot.io/reads/optimistic-vs-pessimistic-concurrency/)
