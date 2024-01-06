# Readable Code

We’ve worked at highly successful software companies,  
With outstanding engineers,  
And the code we encounter still has plenty of room for improvement.

In fact, we’ve seen some really ugly code, and you probably have too.

But when we see beautifully written code, it’s inspiring.  
Good code can teach you what’s going on very quickly.  
It’s fun to use, and it motivates you to make your own code better.

The goal of this book is help you make your code better.  
And when we say “code,” we literally mean the lines of code you are staring at in your editor.

We’re not talking about the overall architecture of your project, or your choice of design patterns.  
Those are certainly important, but in our experience most of our day-to-day lives as programmers are spent on the “basic” stuff,  
Like naming variables, writing loops, and attacking problems down at the function level.  
And a big part of this is reading and editing the code that’s already there.  
We hope you’ll find this book so helpful to your day-to-day programming that you’ll recommend it to everyone on your team.

This book is about how to write code that’s highly readable. The key idea in this book is that
code should be easy to understand. Specifically, your goal should be to minimize the time
it takes someone else to understand your code.

Each chapter dives into a different aspect of coding and how to make it “easy to understand.”
The book is divided into four parts:
Surface-level improvements
Naming, commenting, and aesthetics—simple tips that apply to every line of your
codebase
Simplifying loops and logic
Ways to refine the loops, logic, and variables in your program to make them easier to
understand
Reorganizing your code
Higher-level ways to organize large blocks of code and attack problems at the function level
Selected topics
Applying “easy to understand” to testing and to a larger data structure coding exampl

code should be easy to understand.  
your goal should be to minimize the time it takes someone else to understand your code.

Over the past five years, we have collected hundreds of examples of “bad code” (much of it our own),  
and analyzed what made it bad, and what principles/techniques were used to make it better.  
What we noticed is that all of the principles stem from a single theme.

:::tip KEY IDEA
Code should be easy to understand.
:::

We believe this is the most important guiding principle you can use when deciding how to write your code.

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
