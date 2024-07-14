# Dynamic Programming

## What is Dynamic Programming?

Dynamic programming is an optimization technique,  
Used to efficiently solve problems that are computationally complex.

The key characteristic is the way dynamic programming breaks the overall problem into smaller, overlapping sub-problems.

Often the solutions to sub-problems are stored and reused to avoid repeated work.

In comparison with other approaches,  
This greatly improves the efficiency of the solution.

which usually has to do with finding the maximum and minimum range of the algorithmic query.

## Using Dynamic Programming in Interviews

Before getting to the more formal concepts that determine whether dynamic programming can be applied,  
let's look at some basic heuristics to use in an interview to determine whether to even consider dynamic programming.

### Heuristics for Identifying Dynamic Programming Problems

The first heuristic comes from considering the problem statement.

Does it ask for the min/max out of a set of possible options,  
The best/worst of a set of possible options,  
Or perhaps the total number of options?

This isn't confirmation that dynamic programming is suitable,  
Or even that's the best approach.

But it is a good signal that DP is worth exploring.

As always in a technical interview,  
It's good practice to discuss and work through one or two simple-ish examples.

Doing so helps to clarify the interviewer's requirements and expectations,  
Plus it provides test cases for later.

While working through the examples,  
You likely identified a brute-force approach.

And in explaining how the brute force work leads to the result,  
Did you find yourself mentioning that the more complex example "follows on from" or "makes use of" the simpler example?

This is a second heuristic,  
And it's a great indication that there are sub-problems and repeated work,  
Which means a dynamic programming approach could work well.

Does a programmatic solution involving recursion become apparent?  
Where does the recursion lead?  
Eventually it must "bottom out" and this is likely to be the base case.

What are the branches or conditional paths that trigger recursive calls?  
They will likely form part of the recurrence relation.

The availability of a recursive solution is a third heuristic you can look for.

With one or more of these heuristics present,  
You can be confident spending time and looking hard for a dynamic programming solution.

### Optimal Sub-structure and Overlapping Sub-problems

More formally,  
In order to apply dynamic programming to a problem two conditions must be present:

- #### Optimal sub-structure

Optimal sub-structure requires that you can solve a problem based on the solutions of sub-problems.

For example, if you want to calculate the 5th Fibonacci number,  
It can be solved by computing fib(5) = fib(4) + fib(3).

It is not necessary to know any more information other than the solutions of those two sub-problems in order to determine the solution.

A useful way to think about optimal sub-structure is whether a problem can be easily solved recursively.  
Recursive solutions inherently solve a problem by breaking it down into smaller sub-problems.

If you can solve a problem recursively,  
It most likely has an optimal sub-structure.

- #### Overlapping sub-problems

Overlapping sub-problems means that when you split your problem into sub-problems,  
You sometimes get the same subproblem multiple times.

With the Fibonacci example,  
If we want to compute fib(5), we need to compute fib(4) and fib(3).

However, to compute fib(4), we need to compute fib(3) again.

This is a wasted effort, since we’ve already computed the value of fib(3).

Dynamic programming relies on overlapping sub-problems,  
And it uses memory to save the values that have already been computed to avoid computing them again.

The more overlap there is, the more computational time is saved.

## References

- [interviewing.io/dynamic-programming-interview-questions](https://interviewing.io/dynamic-programming-interview-questions)
