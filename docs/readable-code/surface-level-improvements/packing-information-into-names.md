# Packing Information into Names

Whether you’re naming a variable, a function, or a class, a lot of the same principles apply.  
We like to think of a name as a tiny comment.  
Even though there isn’t much room, you can convey a lot of information by choosing a good name.

KEY IDEA
Pack information into your names.

A lot of the names we see in programs are vague, like `tmp`.  
Even words that may seem reasonable, such as `size` or `get`, don’t pack much information.  
This chapter shows you how to pick names that do.

This chapter is organized into six specific topics:

- Choosing specific words
- Avoiding generic names (or knowing when to use them)
- Using concrete names instead of abstract names
- Attaching extra information to a name, by using a suffix or prefix
- Deciding how long a name should be
- Using name formatting to pack extra information

## Choose Specific Words

Part of **packing information into names** is choosing words that are very specific and avoiding **empty** words.

For example, the word “get” is very unspecific, as in this example:

```cs
public Page GetPage(string url)
{
    ...
}
```

The word “get” doesn’t really say much.

Does this method get a page from a local cache, from a database, or from the Internet?  
If it’s from the Internet, a more specific name might be `FetchPage()` or `DownloadPage()`.

Here’s an example of a `BinaryTree` class:

```cs
public class BinaryTree
{
    public int Size { get; set; }
}
```

What would you expect the `Size` property to return?  
The height of the tree, the number of nodes, or the memory footprint of the tree?

The problem is that `Size` doesn’t convey much information.  
A more specific name would be `Height`, `NumNodes`, or `MemoryBytes`.

As another example, suppose you have some sort of Thread class:

```cs
class Thread {
void Stop();
...
};
```

The name Stop() is okay, but depending on what exactly it does, there might be a more specific
name. For instance, you might call it Kill() instead, if it’s a heavyweight operation that can’t
be undone. Or you might call it Pause(), if there is a way to Resume() it.

Don’t be afraid to use a thesaurus or ask a friend for better name suggestions. English is a rich
language, and there are a lot of words to choose from.
Here are some examples of a word, as well as more “colorful” versions that might apply to your
situation:

| Word  | Alternatives                                       |
| ----- | -------------------------------------------------- |
| send  | deliver, dispatch, announce, distribute, route     |
| find  | search, extract, locate, recover                   |
| start | launch, create, begin, open                        |
| make  | create, set up, build, generate, compose, add, new |

Don’t get carried away, though. In PHP, there is a function to explode() a string. That’s a colorful
name, and it paints a good picture of breaking something into pieces, but how is it any different
from split()? (The two functions are different, but it’s hard to guess their differences based on
the name.)

KEY IDEA
It’s better to be clear and precise than to be cute.
