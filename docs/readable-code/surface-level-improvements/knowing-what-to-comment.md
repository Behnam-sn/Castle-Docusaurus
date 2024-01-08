# Knowing What to Comment

The goal of this chapter is to help you realize what you should be commenting.  
You might think the purpose of commenting is to “explain what the code does” but that is just a small part of it.

:::tip KEY IDEA
The purpose of commenting is to help the reader know as much as the writer did.
:::

When you’re writing code, you have a lot of valuable information in your head.  
When other people read your code, that information is lost.  
And all they have is the code in front of them.

In this chapter, we’ll show you many examples of when to write down that information in your head.  
We’ve left out the more mundane points about commenting;  
Instead, we’ve focused on the more interesting and “underserved” aspects of commenting.

We’ve organized the chapter into the following areas:

- Knowing what not to comment
- Recording your thoughts as you code
- Putting yourself in the readers’ shoes, to imagine what they’ll need to know

## What NOT to Comment

Reading a comment takes time away from reading the actual code,
And each comment takes up space on the screen.  
That is, it better be worth it.  
So where do you draw the line between a worthless comment and a good one?

All of the comments in this code are worthless:

```cs
// The class definition for Account
class Account {

    // Constructor
    public Account()
    {
        ...
    }

    // Set the profit member to a new value
    void SetProfit(double profit)
    {
        ...
    }

    // Return the profit from this Account
    double GetProfit()
    {
        ...
    }
}
```

These comments are worthless because they don’t provide any new information or help the reader understand the code better.

:::tip KEY IDEA
Don’t comment on facts that can be derived quickly from the code itself.
:::

The word “quickly” is an important distinction, though. Consider the comment for this Python code:

```python
# remove everything after the second '*'
name = '*'.join(line.split('*')[:2])
```

Technically, this comment doesn’t present any “new information” either.  
If you look at the code itself, you’ll eventually figure out what it’s doing.

But for most programmers,  
Reading the commented code is much faster than understanding the code without it.

## Don’t Comment Just for the Sake of Commenting

Some professors require their students to have a comment for each function in their homework code.  
As a result, some programmers feel guilty about leaving a function naked without comments,  
And end up rewriting the function’s name and arguments in sentence form:

```cs
// Find the Node in the given subtree, with the given name, using the given depth.
Node FindNodeInSubtree(Node subtree, string name, int depth);
```

This one falls into the “worthless comments” category.  
The function’s declaration and the comment are virtually the same.  
This comment should be either removed or improved.

If you want to have a comment here,  
It might as well elaborate on more important details:

```cs
// Find a Node with the given 'name' or return NULL.
// If depth <= 0, only 'subtree' is inspected.
// If depth == N, only 'subtree' and N levels below are inspected.
Node FindNodeInSubtree(Node subtree, string name, int depth);
```

## Don’t Comment Bad Names, Fix the Names Instead

A comment shouldn’t have to make up for a bad name.  
For example, here’s an innocent-looking comment for a function named `CleanReply()`:

```cs
// Enforce limits on the Reply as stated in the Request,
// such as the number of items returned, or total byte size, etc.
void CleanReply(Request request, Reply reply);
```

Most of the comment is simply explaining what “clean” means.  
Instead, the phrase “enforce limits” should be moved into the function name:

```cs
// Make sure 'reply' meets the count/byte/etc. limits from the 'request'
void EnforceLimitsFromRequest(Request request, Reply reply)
```

This function name is more _“self-documenting”_.  
A good name is better than a good comment because it will be seen everywhere the function is used.

Here is another example of a comment for a poorly named function:

```cs
// Releases the handle for this key. This doesn't modify the actual registry.
void DeleteRegistry(RegistryKey key);
```

The name `DeleteRegistry()` sounds like a dangerous function (it deletes the registry?!).  
The comment _“This doesn’t modify the actual registry”_ is trying to clear up the confusion.

Instead, we could use a more self-documenting name like:

```cs
void ReleaseRegistryHandle(RegistryKey key);
```

In general, you don’t want _“crutch comments”_.  
Comments that are trying to make up for the unreadability of the code.  
Coders often state this rule as **good code > bad code + good comments**.
