# Dynamic Programming

## What is Dynamic Programming?

Dynamic programming is an optimization technique,  
Used to efficiently solve problems that are computationally complex,  
Which usually has to do with finding the maximum and minimum range of the algorithmic query.

Dynamic programming key characteristic,  
Is the way it breaks the overall problem,  
Into smaller, overlapping sub-problems.

Often the solutions to sub-problems are stored and reused to avoid repeated work.

In comparison with other approaches,  
This greatly improves the efficiency of the solution.

Richard Bellman was the one who came up with the idea for dynamic programming in the 1950s.

It is a method of mathematical optimization as well as a methodology for computer programming.

It applies to issues one can break down into either overlapping subproblems or optimum substructures.

Dynamic Programming is a tool that will help make your recursive code more efficient.

## How to Use Dynamic Programming?

### The FAST Method

FAST is an acronym that stands for:

- Find the first solution,
- Analyze the solution,
- identify the Sub-problems,
- and Turn around the solution.

It isn’t the only way to work through problems to reach a dynamic programming solution,  
But aims to be easy to remember and apply while being broadly applicable.

Let’s break down each of these steps.

#### Find the First Solution

The first step to solving any dynamic programming problem using The FAST Method,  
Is to find an initial brute force recursive solution.

Solve the problem without concern for efficiency, just as a starting point.

Though there are a couple of constraints on how this brute force solution should look:

- Recursive functions should be self-contained.

  Storing results by updating global variables may make it impossible to introduce memoization later on.

  Craft a function that is solely dependent on its parameters and not affected by outside factors.

- Avoid unnecessary recursive function arguments.

  Subproblem results will eventually be memoized based on the arguments;

  The fewer the better.

#### Analyze the First Solution

Analyze the initial brute force solution.

This involves determining the time and space complexity and determining if there are any obvious areas for improvement.

As part of the analytical process,  
Confirm that the first solution fits the rules for problems with Dynamic programming solutions:

- Does it have an optimal substructure?
- Are there overlapping sub-problems?

#### Subproblem Identification

If there is indeed a Dynamic programming solution,  
The appropriate sub-problems can now be identified and coded.

Apply memoization to avoid unnecessary repeated work.

At this point the problem is solved with a top-down solution that likely exhibits optimal complexity and no does not repeat any work.

#### Turn the Solution Around

Since we understand the problem well, we can go further.

This involves coding the alternate bottom-up approach that iteratively computes and uses tabulation to store the results of successive sub-problems, until the overall solution is reached.

Turning the solution to bottom-up is generally desired as it avoids pitfalls associated with recursion and the call stack.

### Deciding on Top-down/Memoization vs. Bottom-up/Tabulation

In an interview,  
The choice of top-down or bottom-up approaches should be balanced with other factors beyond performance:

How easily can the bottom-up solution be coded,  
Is it as easily reasoned about and discussed with the interviewer?

Which approach are you most comfortable with? That may be the most important factor of all!

## When to Use Dynamic Programming?

let's look at some basic heuristics to determine whether to even consider dynamic programming.

### Heuristics for Identifying Dynamic Programming Problems

#### 1

The first heuristic comes from considering the problem statement.

Does it ask for the min/max out of a set of possible options,  
The best/worst of a set of possible options,  
Or perhaps the total number of options?

This isn't confirmation that dynamic programming is suitable,  
Or even that's the best approach.

But it is a good signal that DP is worth exploring.

#### 2

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

#### 3

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

## Common Mistakes in Interviews Featuring Dynamic Programming

- Jumping too quickly to conclude dynamic programming is necessary.

When you have a hammer, everything starts to look like a nail.

If the problem doesn’t require an optimal solution but rather any correct solution,  
A greedy approach will likely be simpler to identify and implement.

- Conversely, looking too hard for a greedy solution and failing to recognize a dynamic programming problem.

A way to determine which solution is more appropriate is to know whether a sub-solution helps lead to the final solution.

If a sub-solution (a solution with a part of the input) helps,  
Then dynamic programming is probably the way to go!

- Failing to identify how to break the problem into sub-problems so that the recurrence relation and base case(s) become clear.

When you have a strong intuition (or have been told) that a problem needs a Dynamic programming solution,  
This is the major challenge.

Reviewing plenty of questions and gaining practice is essential.

- Struggling to define and work with a suitable result matrix.

Many problems (such as Longest Common Subsequence) involve two- or multi-dimensional arrays to store sub-problem results.

These can be difficult to conceive and may be tricky to work with in code.

Again it’s all about practice.

- Lack of clarity in communicating your dynamic programming logic.

Visualizations can help a great deal here.

As we’ve seen in this article,

Sketching a recursive tree or a matrix table can be helpful tools to gain shared understanding with your interviewer.

## What to Say in Interviews to Show Mastery Over Dynamic Programming

Articulate why dynamic programming is applicable (overlapping sub-problems and optimal substructure) for a given problem
Refer to the recurrence relation and base case(s). Reason about and justify that the subproblem dependencies are acyclic.
Discuss and ask the interviewer if they have a preference when it comes to the tradeoffs between top-down (recursive) and bottom-up approaches.

## notes

When a more extensive set of equations is broken down into smaller groups of equations, overlapping subproblems are referred to as equations that reuse portions of the smaller equations several times to arrive at a solution.

On the other hand, optimum substructures locate the best solution to an issue, then build the solution that provides the best results overall. This is how they solve problems. When a vast issue is split down into its constituent parts, a computer will apply a mathematical algorithm to determine which elements have the most desirable solution. Then, it takes the solutions to the more minor problems and utilizes them to get the optimal solution to the initial, more involved issue.

This technique solves problems by breaking them into smaller, overlapping subproblems. The results are then stored in a table to be reused so the same problem will not have to be computed again.

The dynamic programming algorithm tries to find the shortest way to a solution when solving a problem. It does this by going from the top down or the bottom up. The top-down method solves equations by breaking them into smaller ones and reusing the answers when needed. The bottom-up approach solves equations by breaking them up into smaller ones, then tries to solve the equation with the smallest mathematical value, and then works its way up to the equation with the biggest value.

Using dynamic programming to solve problems is more effective than just trying things until they work. But it only helps with problems that one can break up into smaller equations that will be used again at some point.

## References

- [interviewing.io/dynamic-programming-interview-questions](https://interviewing.io/dynamic-programming-interview-questions)
- [medium.com/@al.eks/the-ultimate-guide-to-dynamic-programming-65865ef7ec5b](https://medium.com/@al.eks/the-ultimate-guide-to-dynamic-programming-65865ef7ec5b)
