# Readable Code

code should be easy to understand.
your goal should be to minimize the time it takes someone else to understand your code.

Over the past five years, we have collected hundreds of examples of “bad code” (much of it
our own), and analyzed what made it bad, and what principles/techniques were used to make
it better. What we noticed is that all of the principles stem from a single theme.
K E Y I D E A
Code should be easy to understand.

We believe this is the most important guiding principle you can use when deciding how to
write your code.

The Fundamental Theorem of Readability
After studying many code examples like this, we came to the conclusion that there is one metric
for readability that is more important than any other. It’s so important that we call it “The
Fundamental Theorem of Readability.”
K E Y I D E A
Code should be written to minimize the time it would take for someone else to
understand it.

What do we mean by this? Quite literally, if you were to take a typical colleague of yours, and
measure how much time it took him to read through your code and understand it, this “time-
till-understanding” is the theoretical metric you want to minimize.

And when we say “understand,” we have a very high bar for this word. For someone to fully
understand your code, they should be able to make changes to it, spot bugs, and understand
how it interacts with the rest of your code

Now, you might be thinking, Who cares if someone else can understand it? I'm the only one using the
code! Even if you’re on a one-man project, it’s worth pursuing this goal. That “someone else”
might be you six months later, when your own code looks unfamiliar to you. And you never
know—someone might join your project, or your “throwaway code” might get reused for
another project.

<!-- Is Smaller Always Better?
Generally speaking, the less code you write to solve a problem, the better (see Chapter 13,
Writing Less Code). It probably takes less time to understand a 2000-line class than a 5000-line
class.
But fewer lines isn’t always better! There are plenty of times when a one-line expression like:
assert((!(bucket = FindBucket(key))) || !bucket->IsOccupied());
takes more time to understand than if it were two lines:
bucket = FindBucket(key);
if (bucket != NULL) assert(!bucket->IsOccupied());
Similarly, a comment can make you understand the code more quickly, even though it “adds
code” to the file:
// Fast version of "hash = (65599 \* hash) + c"
hash = (hash << 6) + (hash << 16) - hash + c;
So even though having fewer lines of code is a good goal, minimizing the time-till-
understanding is an even better goal.

Does Time-Till-Understanding Conflict with Other Goals?
You might be thinking, What about other constraints, like making code efficient, or well-architected, or
easy to test, and so on? Don’t these sometimes conflict with wanting to make code easy to understand?
We’ve found that these other goals don't interfere much at all. Even in the realm of highly
optimized code, there are still ways to make it highly readable as well. And making your code
easy to understand often leads to code that is well architected and easy to test.

Also, some programmers have a compulsive need to fix any code that
isn’t perfectly factored. It’s always important to step back and ask, Is this code easy to
understand? If so, it’s probably fine to move on to other code. -->
