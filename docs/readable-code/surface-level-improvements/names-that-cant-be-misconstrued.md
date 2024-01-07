---
sidebar_position: 2
---

# Names That Can’t Be Misconstrued

## Naming Booleans

When picking a name for a boolean variable or a function that returns a boolean,  
Be sure it’s clear what `true` and `false` really mean.

Here’s a dangerous example:

```cs
bool readPassword = true;
```

Depending on how you read it (no pun intended), there are two very different interpretations:

- We need to read the password
- The password has already been read

In this case, it’s best to avoid the word “read”,  
and name it `needPassword` or `userIsAuthenticated` instead.

In general, adding words like is, has, can, or should can make booleans more clear.

For example, a function named `SpaceLeft()` sounds like it might return a number.  
If it were meant to return a boolean, a better name would be `HasSpaceLeft()`.

Finally, it’s best to avoid negated terms in a name.  
For example, instead of:

```cs
bool disableSSL = false;
```

it would be easier to read (and more compact) to say:

```cs
bool useSSL = true;
```
