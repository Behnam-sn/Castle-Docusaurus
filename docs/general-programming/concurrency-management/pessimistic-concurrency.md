---
sidebar_position: 2
---

# Pessimistic Concurrency

## What is Pessimistic Concurrency?

Pessimistic concurrency is a concurrency management approach.

Pessimistic concurrency assumes conflicts between operations can happen often.

## How does Pessimistic Concurrency Work?

In pessimistic concurrency,  
We lock the data when we want to change them.

In order to prevent other operations from changing them simultaneously.

After our changes are over, we will release the lock.  
And then other operations can use the data.

The pessimistic concurrency approach has Two lock modes:

- ### Shared

  Allows other operations to read the data, but they can't change it.

- ### Exclusive

  Only the operations who applied the lock can read or change the data.

No other locks can be applied until the user releases the lock.

## When to Use Pessimistic Concurrency?

The pessimistic concurrency approach is suitable for applications with heavy data conflicts.

Because it will block conflicts before processing operations,  
Meaning you won't need to roll back operations later.

On the other hand,  
The pessimistic concurrency approach is not a good option for applications with scaling requirements.

## References

- [cult.honeypot.io/reads/optimistic-vs-pessimistic-concurrency/](https://cult.honeypot.io/reads/optimistic-vs-pessimistic-concurrency/)
- [en.wikipedia.org/wiki/Record_locking](https://en.wikipedia.org/wiki/Record_locking)
