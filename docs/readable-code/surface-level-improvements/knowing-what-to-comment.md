---
sidebar_position: 4
---

# Knowing What to Comment

## What is the Purpose of Commenting?

The goal of this chapter is to help you realize what you should be commenting.  
You might think the purpose of commenting is to “explain what the code does” but that is just a small part of it.

**The purpose of commenting is to help the reader know as much as the writer did.**

When you’re writing code, you have a lot of valuable information in your head.  
When other people read your code, that information is lost.  
And all they have is the code in front of them.

In this chapter, we’ll show you many examples of when to write down that information in your head.  
We’ve left out the more mundane points about commenting.  
Instead, we’ve focused on the more interesting and _“underserved”_ aspects of commenting.  
This whole chapter is about realizing all the not-so-obvious nuggets of information you have about the code and writing those down.

We’ve organized the chapter into the following areas:

- Knowing what not to comment  
  What not to comment:

  - Facts that can be quickly derived from the code itself.
  - “Crutch comments” that make up for bad code (such as a bad function name)—fix the code instead.

- Recording your thoughts as you code  
  Thoughts you should be recording include:

  - Insights about why code is one way and not another (“director commentary”).
  - Flaws in your code, by using markers like TODO: or XXX:.
  - The “story” for how a constant got its value.

- Putting yourself in the readers’ shoes, to imagine what they’ll need to know  
  Put yourself in the reader’s shoes:

  - Anticipate which parts of your code will make readers say “Huh?” and comment those.
  - Document any surprising behavior an average reader wouldn’t expect.
  - Use “big picture” comments at the file/class level to explain how all the pieces fit together.
  - Summarize blocks of code with comments so that the reader doesn’t get lost in the details.

## What Not to Comment

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

### Don’t Comment Just for the Sake of Commenting

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

### Don’t Comment Bad Names, Fix the Names Instead

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

## Recording Your Thoughts

Now that you know what not to comment, let’s discuss what should be commented (but often isn’t).

A lot of good comments can come out of simply _“recording your thoughts”_,  
That is, the important thoughts you had as you were writing the code.

### Include Director Commentary

Movies often have a _“director commentary”_ track,  
where the filmmakers give their insights and tell stories to help you understand how the film was made.  
Similarly, you should include comments to record valuable insights about the code.

Here’s an example:

```cs
// Surprisingly, a binary tree was 40% faster than a hash table for this data.
// The cost of computing a hash was more than the left/right comparisons.
```

This comment teaches the reader something and stops any would-be optimizer from wasting their time.

Here’s another example:

```cs
// This heuristic might miss a few words. That's OK; solving this 100% is hard
```

Without this comment the reader might think there’s a bug,  
And might waste time trying to come up with test cases that make it fail, or go off and try to fix the bug.

A comment can also explain why the code isn’t in great shape:

```cs
// This class is getting messy. Maybe we should create a 'ResourceNode' subclass to
// help organize things.
```

This comment acknowledges that the code is messy but also encourages the next person to fix it (with specifics on how to get started).  
Without the comment, many readers would be intimidated by the messy code and afraid to touch it.

### Comment the Flaws in Your Code

Code is constantly evolving and is bound to have flaws along the way.  
Don’t be embarrassed to document those flaws.

For example, noting when improvements should be made:

```cs
// TODO: use a faster algorithm
```

or when code is incomplete:

```cs
// TODO(dustin): handle other image formats besides JPEG
```

There are a number of markers that have become popular among programmers:

| Marker | Typical meaning                            |
| ------ | ------------------------------------------ |
| TODO:  | Stuff I haven’t gotten around to yet       |
| FIXME: | Known-broken code here                     |
| HACK:  | Admittedly inelegant solution to a problem |
| XXX:   | Danger! major problem here                 |

Your team might have specific conventions for when/if to use these markers.  
For example, `TODO:` might be reserved for show-stopping issues.  
If so, then for more minor flaws you could use something like `todo:` (lower case) or `maybe-later:` instead.

The important thing is that you should always feel free to comment on your thoughts about how the code should change in the future.  
Comments like these give readers valuable insight into the quality and state of the code and might even give them some direction on how to improve it.

### Comment on Your Constants

When defining a constant, there is often a _“story”_ for what that constant does or why it has that specific value.

For example, you might see this constant in your code:

```cs
const int NUM_THREADS = 8;
```

It may not seem like this line needs a comment,  
But it’s likely that the programmer who chose it knows more about it:

```cs
const int NUM_THREADS = 8 // as long as it's >= 2 * num_processors, that's good enough.
```

Now the person reading the code has some guidance on how to adjust that value.  
(e.g., setting it to 1 is probably too low, and setting it to 50 is overkill)

Or sometimes the exact value of a constant isn’t important at all. A comment to this effect is still useful:

```cs
// Impose a reasonable limit - no human can read that much anyway.
const int MAX_RSS_SUBSCRIPTIONS = 1000;
```

Sometimes it’s a value that’s been highly tuned, and probably shouldn’t be adjusted much:

```cs
const int IMAGE_QUALITY = 0.72; // users thought 0.72 gave the best size/quality tradeoff
```

In all these examples, you might not have thought to add comments, but they’re quite helpful.

There are some constants that don’t need a comment,  
Because their name is clear enough (e.g., SECONDS_PER_DAY).

But in our experience, most constants could be improved by adding a comment.  
It’s just a matter of jotting down what you were thinking about when you decided on that constant’s value.

## Put Yourself in the Reader’s Shoes

A general technique is to imagine what your code looks like to an outsider,  
Someone who isn’t as intimately familiar with your project as you are.  
This technique is especially useful to help you recognize what needs commenting.

### Anticipating Likely Questions

When someone else reads your code,  
there are parts likely to make them think,  
_Huh? What’s this all about?_

Your job is to comment those parts.

For example, take a look at the definition of `Clear()`:

```c++
struct Recorder {
 vector<float> data;
 ...
 void Clear() {
 vector<float>().swap(data); // Huh? Why not just data.clear()?
 }
};
```

When most C++ programmers see this code, they think,  
Why didn’t he just do `data.clear()` instead of swapping with an empty vector?  
Well, it turns out that this is the only way to force a vector to truly relinquish its memory to the memory allocator.  
It’s a C++ detail that isn’t well known.  
The bottom line is that it should be commented:

```c++
// Force vector to relinquish its memory (look up "STL swap trick")
vector<float>().swap(data);
```

### Advertising Likely Pitfalls

When documenting a function or class,  
A good question to ask yourself is,  
_What is surprising about this code? How might it be misused?_  
Basically, you want to _“think ahead”_ and anticipate the problems that people might run into when using your code.

For example, suppose you wrote a function that sends an email to a given user:

```cs
void SendEmail(string to, string subject, string body)
{
    ...
}
```

The implementation of this function involves connecting to an external email service,  
Which might take up to a whole second, or possibly longer.  
Someone who is writing a web application might not realize this and mistakenly call this function while handling an HTTP request.  
(Doing this would cause their web application to “hang” if the email service is down.)

To prevent this likely mishap, you should comment on this _“implementation detail”_:

```cs
// Calls an external service to deliver email. (Times out after 1 minute.)
void SendEmail(string to, string subject, string body)
{
    ...
}
```

Here is another example:  
Suppose you have a `FixBrokenHtml()` function that attempts to rewrite broken HTML by inserting missing closing tags and the like:

```cs
void FixBrokenHtml(string html)
{
    ...
}
```

The function works great, except for the caveat that its running time blows up when there are deeply nested and unmatched tags.  
For nasty HTML inputs, this function could take minutes to execute.

Rather than let the user discover this later on his own, it’s better to announce this upfront:

```cs
// Runtime is O(number_tags * average_tag_depth), so watch out for badly nested inputs.
void FixBrokenHtml(string html)
{
    ...
}
```

### Big Picture Comments

One of the hardest things for a new team member to understand is the _“big picture”_.  
How classes interact, how data flows through the whole system, and where the entry points are.

The person who designed the system often forgets to comment about this stuff because he’s so intimately involved with it.

Consider this thought experiment:  
Someone new just joined your team, she’s sitting next to you, and you need to get her familiar with the codebase.

As you’re giving her a tour of the codebase,  
You might point out certain files or classes and say things like:

- “This is the glue code between our business logic and the database.  
  None of the application code should use this directly.”
- “This class looks complicated, but it’s really just a smart cache.  
  It doesn’t know anything about the rest of the system.”

After a minute of casual conversation,  
Your new team member will know much more than she would from reading the source by herself.

**This is exactly the type of information that should be included as high-level comments.**

Here’s a simple example of a file-level comment:

```cs
// This file contains helper functions that provide a more convenient interface to our
// file system. It handles file permissions and other nitty-gritty details.
```

Don’t get overwhelmed by the thought that you have to write extensive, formal documentation.  
**A few well-chosen sentences are better than nothing at all.**

### Summary Comments

Even deep inside a function, it’s a good idea to comment on the _“bigger picture”_.  
Here’s an example of a comment that neatly summarizes the low-level code below it:

```cs
// Find all the items that customers purchased for themselves.
foreach(var customerId in allCustomers)
{
    foreach(var sale in allSales[customerId].Sales)
    {
        if(sale.Recipient == customerId)
        {
            ...
        }
    }
}
```

Without this comment, reading each line of code is a bit of a mystery.  
(_“I see we’re iterating through allCustomers … but what for?”_)

It’s especially helpful to have these summary comments in longer functions where there are a few large _“chunks”_ inside:

```cs
void GenerateUserReport()
{
    // Acquire a lock for this user
    ...
    // Read user's info from the database
    ...
    // Write info to a file
    ...
    // Release the lock for this user
}
```

These comments also act as a bulleted summary of what the function does,  
So the reader can get the gist of what the function does before diving into details.

If these chunks are easily separable, you might just make them functions of their own.  
As we mentioned before, good code is better than bad code with good comments.

## Getting Over Writer’s Block

A lot of coders don’t like to write comments because it feels like a lot of work to write a good one.  
When writers have this sort of _“writer’s block”_, the best solution is to just start writing.

So the next time you’re hesitating to write a comment,  
Just go ahead and comment what you’re thinking, however half-baked it may be.

For example, suppose you’re working on a function and think to yourself,  
_Oh crap, this stuff will get tricky if there are ever duplicates in this list._  
Just write that down:

```cs
// Oh crap, this stuff will get tricky if there are ever duplicates in this list.
```

See, was that so hard? It’s actually not that bad of a comment—certainly better than nothing.

The language is a little vague though.  
To fix it, we can just go through each phrase and replace it with something more specific:

- By _“oh crap”_, you really mean _“Careful: this is something to watch out for”_.
- By _“this stuff”_, you mean _“the code that’s handling this input”_.
- By _“will get tricky”_, you mean _“will be hard to implement”_.

The new comment might be:

```cs
// Careful: this code doesn't handle duplicates in the list (because that's hard to do)
```

Notice that we’ve broken down the task of writing a comment into these simpler steps:

1. Write down whatever comment is on your mind.
1. Read the comment, and see what (if anything) needs to be improved.
1. Make improvements.

As you comment more often,  
You’ll find that the quality of comments from step 1 gets better and better and eventually might not need fixing at all.

And by commenting early and often,  
You avoid the unpleasant situation of needing to write a bunch of comments at the end.

## References

- The Art of Readable Code - Dustin Boswell, Trevor Foucher - O'Reilly
