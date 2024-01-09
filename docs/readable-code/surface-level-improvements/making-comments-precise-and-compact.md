# Making Comments Precise and Compact

The previous chapter was about realizing what you should be commenting.  
This chapter is about how to write comments that are precise and compact.

If you're going to write a comment at all,  
It might as well be precise and as specific and detailed as possible.

On the other hand, comments take up extra space on the screen, and take extra time to read.  
So comments should also be compact.

:::tip KEY IDEA
Comments should have a high information-to-space ratio.
:::

The rest of the chapter shows examples of how to do this.

## Keep Comments Compact

Here’s an example of a comment for a C++ type definition:

```c++
// The int is the CategoryType.
// The first float in the inner pair is the 'score',
// the second is the 'weight'.
typedef hash_map<int, pair<float, float> > ScoreMap;
```

But why use three lines to explain it, when you can illustrate it in just one line?

```c++
// CategoryType -> (score, weight)
typedef hash_map<int, pair<float, float> > ScoreMap;
```

Some comments need three lines of space, but this is not one of them.

## Avoid Ambiguous Pronouns

Pronouns can make things very confusing.  
It takes extra work for the reader to _“resolve”_ a pronoun.  
And in some cases, it’s unclear what _“it”_ or _“this”_ is referring to.  
Here’s an example:

```cs
// Insert the data into the cache, but check if it's too big first.
```

In this comment, _“it”_ might refer to the data or the cache.  
You could probably figure that out by reading the rest of the code.  
But if you have to do that, what’s the point of the comment?

The safest thing is to _“fill in”_ pronouns if there’s any chance of confusion.  
In the previous example, let’s assume _“it”_ was _“the data”_:

```cs
// Insert the data into the cache, but check if the data is too big first.
```

This is the simplest change to make.

You could also have restructured the sentence to make _“it”_ perfectly clear:

```cs
// If the data is small enough, insert it into the cache.
```

## Polish Sloppy Sentences

In many cases, making a comment more precise goes hand-in-hand with making it more compact.

Here is an example from a web crawler:

```cs
// Depending on whether we've already crawled this URL before, give it a different priority.
```

This sentence might seem okay, but compare it to this version:

```cs
// Give higher priority to URLs we've never crawled before.
```

This sentence is simpler, smaller, and more direct.  
It also explains that higher priority is given to uncrawled URLs,  
The previous comment didn’t contain that information.

## Describe Function Behavior Precisely

Imagine you just wrote a function that counts the number of lines in a file:

```cs
// Return the number of lines in this file.
int CountLines(string filename)
{
    ...
}
```

This comment isn’t very precise.  
There are a lot of ways to define a _“line”_.  
Here are some corner cases to think about:

- "" (an empty file)—0 or 1 line?
- "hello"—0 or 1 line?
- "hello\n"—1 or 2 lines?
- "hello\n world"—1 or 2 lines?
- "hello\n\r cruel\n world\r"—2, 3, or 4 lines?

The simplest implementation is to count the number of newline (\n) characters.  
(This is the way the Unix command wc works)

Here’s a better comment to match this implementation:

```cs
// Count how many newline bytes ('\n') are in the file.
int CountLines(string filename)
{
    ...
}
```

This comment isn’t much longer than the first version, but contains much more information.  
It tells the reader that the function might return 0 if there are no newlines.  
It also tells the reader that carriage returns (\r) are ignored.
