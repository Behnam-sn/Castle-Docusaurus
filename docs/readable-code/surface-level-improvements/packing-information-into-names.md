# Packing Information into Names

We like to think of a name as a tiny comment.

Even though there isn’t much room,  
You can convey a lot of information by choosing a good name.

Whether you’re naming a variable, a function, or a class, a lot of the same principles apply.

:::tip KEY IDEA
Pack information into your names.
:::

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

For example, the word `get` is very unspecific, as in this example:

```cs
public Page GetPage(string url)
{
    ...
}
```

The word `get` doesn’t really say much.

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

As another example, suppose you have some sort of `Thread` class:

```cs
public class Thread
{
    public void Stop()
    {
        ...
    }
}
```

The name `Stop()` is okay,  
But depending on what exactly it does,  
There might be a more specific name.

For instance, you might call it `Kill()` instead,  
If it’s a heavyweight operation that can’t be undone.

Or you might call it `Pause()`, if there is a way to `Resume()` it.

Don’t be afraid to use a thesaurus or ask a friend for better name suggestions.  
English is a rich language, and there are a lot of words to choose from.

Here are some examples of a word, as well as more “colorful” versions that might apply to your situation:

| Word  | Alternatives                                       |
| ----- | -------------------------------------------------- |
| send  | deliver, dispatch, announce, distribute, route     |
| find  | search, extract, locate, recover                   |
| start | launch, create, begin, open                        |
| make  | create, set up, build, generate, compose, add, new |

Don’t get carried away, though.

In PHP, there is a function to `explode()` a string.  
That’s a colorful name, and it paints a good picture of breaking something into pieces,  
But how is it any different from `split()`?  
The two functions are different, but it’s hard to guess their differences based on the name.

:::tip KEY IDEA
It’s better to be clear and precise than to be cute.
:::

## Avoid Generic Names Like tmp and retval

Names like `tmp`, `retval`, and `foo` are usually cop-outs that mean “I can’t think of a name.”  
Instead of using an empty name like this,  
**Pick a name that describes the entity’s value or purpose.**

For example, here’s a JavaScript function that uses retval:

```js
var euclidean_norm = function (v) {
  var retval = 0.0;
  for (var i = 0; i < v.length; i += 1) retval += v[i] * v[i];
  return Math.sqrt(retval);
};
```

It’s tempting to use `retval` when you can’t think of a better name for your return value.  
But retval doesn’t contain much information other than “I am a return value” (which is usually obvious anyway).

A better name would describe the purpose of the variable or the value it contains.  
In this case, the variable is accumulating the sum of the squares of `v`.  
So a better name is `sum_squares`.  
This would announce the purpose of the variable upfront and might help catch a bug.

For instance, imagine if the inside of the loop were accidentally:

```js
retval += v[i];
```

This bug would be more obvious if the name were sum_squares:

```js
sum_squares += v[i];
// Where's the "square" that we're summing? Bug!
```

:::info ADVICE
The name retval doesn’t pack much information.  
Instead, use a name that describes the variable’s value.
:::

There are, however, some cases where generic names do carry meaning.  
Let’s take a look at when it makes sense to use them.

## tmp

Consider the classic case of swapping two variables:

```js
if (right < left) {
  tmp = right;
  right = left;
  left = tmp;
}
```

In cases like these, the name `tmp` is perfectly fine.  
The variable’s sole purpose is temporary storage, with a lifetime of only a few lines.  
The name `tmp` conveys specific meaning to the reader—that this variable has no other duties.  
It’s not being passed around to other functions or being reset or reused multiple times.

But here’s a case where tmp is just used out of laziness:

```js
String tmp = user.name();
tmp += " " + user.phone_number();
tmp += " " + user.email();
...
template.set("user_info", tmp);
```

Even though this variable has a short lifespan,  
Being temporary storage isn’t the most important thing about this variable.  
Instead, a name like `user_info` would be more descriptive.

In the following case, `tmp` should be in the name, but just as a part of it:

```js
tmp_file = tempfile.NamedTemporaryFile()
...
SaveData(tmp_file, ...)
```

Notice that we named the variable `tmp_file` and not just `tmp`,  
Because it is a file object.  
Imagine if we just called it `tmp`:

```js
SaveData(tmp, ...)
```

Looking at just this one line of code, it isn’t clear if tmp is a file, a filename, or maybe even the data being written.

:::info ADVICE
The name `tmp` should be used only in cases when being short-lived and temporary is the most important fact about that variable.
:::

## Loop Iterators

Names like `i`, `j`, `iter`, and `it` are commonly used as indices and loop iterators.

Even though these names are generic,  
They’re understood to mean “I am an iterator”.  
In fact, if you used one of these names for some other purpose, it would be confusing, so don’t do that!

```cpp
for (int i = 0; i < clubs.size(); i++)
    for (int j = 0; j < clubs[i].members.size(); j++)
        for (int k = 0; k < users.size(); k++)
            if (clubs[i].members[k] == users[j])
                cout << "user[" << j << "] is in club[" << i << "]" << endl;
```

In the if statement, `members[]` and `users[]` are using the wrong index.  
Bugs like these are hard to spot because that line of code seems fine in isolation:

```cpp
if (clubs[i].members[k] == users[j])
```

In this case, using more precise names may have helped.  
Instead of naming the loop indexes (`i,j,k`), another choice would be (club_index, members_index, users_index)

This approach would help the bug stand out more:

```cpp
if (clubs[ci].members[ui] == users[mi])
# Bug! First letters don't match up.
```

When used correctly,  
The first letter of the index would match the first letter of the array:

```cpp
if (clubs[ci].members[mi] == users[ui])
# OK. First letters match.
```

## The Verdict on Generic Names

As you’ve seen, there are some situations where generic names are useful.

:::info ADVICE
If you’re going to use a generic name like tmp, it, or retval, have a good reason for doing so.
:::

A lot of the time, they’re overused out of pure laziness.

This is understandable,  
When nothing better comes to mind,  
It’s easier to just use a meaningless name like foo and move on.

But if you get in the habit of taking an extra few seconds to come up with a good name,  
You’ll find your “naming muscle” builds quickly.
