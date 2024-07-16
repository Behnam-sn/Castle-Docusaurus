# Recursion

## What is Recursion?

Recursion is a strategy used in computer science where a function invokes itself to solve a problem.

This self-referential nature of recursion helps to solve problems that can be broken down into simpler, similar problems.

In other words, recursion is a strategy where the solution to a problem depends on solutions to smaller instances of the same problem.

Recursion is a potent tool when dealing with problems related to data structures,  
Such as traversing trees or graphs, sorting arrays, or exploring permutations and combinations.

Functional languages like Haskell, Scala, and Erlang, among others,  
Tend to favor recursion for control flow,  
Since they lack traditional looping constructs present in imperative languages.

Most looping operations can be expressed recursively,  
which is part of the reason why functional programming languages often favor recursion.

## How Recursion Works?

Base Case + Recursive Case = Recursive Function

### Base Case

The condition that stops the recursion.

It a simple, solvable case of the problem,
That does not require further recursion.

### Recursive Case

The part of the recursion,  
That breaks the problem down into smaller sub-problems,  
Leading closer to the base case.

It involves a function calling itself.

### Example

Let's understand recursion with an analogy.

Suppose you're standing at the bottom of a staircase and want to reach the top.

The staircase has many steps,  
And your task is to climb them all.

A non-recursive way of thinking would be to count each step as you climb, one after the other, until you reach the top.

However, a recursive approach would be different.

Instead of thinking about all the steps you need to climb,  
In a recursive way, you wouldn't consider each step separately.

Instead, you would break down the problem.

How do you reach the top?  
You climb one step,  
And then you are left with a staircase that is shorter by one step.

This is your recursive step:  
Climbing to the top of a staircase is the same as climbing one step,  
And then climbing to the top of a smaller staircase.

But we're missing an important part,  
What if there's only one step?  
Or what if there are no steps at all?

This brings us to the concept of a base case.  
In recursion, a base case acts as a stopping signal,  
Telling the function when to stop calling itself and start returning.

In our analogy,  
The base case is when there are no more steps to climb.

If there's only one step, you climb it, and you're done.  
If there are no steps, you're already at the top!

```cs
void ClimbSteps(int n)
{
    // Base case: if there are no more steps, stop recursion
    if (n == 0):
    {
        Console.WriteLine("You're at the top! All steps climbed.")
        return;
    }

    // Recursive step: climb one step
    Console.WriteLine("Climb one step. Remaining steps: " + (n - 1))
    // Recursive call: continue climbing the remaining steps
    ClimbSteps(n - 1)
}
```

Let's see what the output will look like when we call `ClimbSteps(3)`:

```console
Climb one step. Remaining steps: 2
Climb one step. Remaining steps: 1
Climb one step. Remaining steps: 0
You're at the top! All steps climbed.
```

These principles can be applied to a wide range of problems in computer science,  
Which we'll explore further in the following sections.

### Call Stack

Before we move on,  
Let's take a moment to understand how recursion works under the hood.

Think of each recursive call to `ClimbSteps`,  
As sending a climber to ascend the staircase.

When the function calls itself,  
It's like it's sending another climber to ascend a slightly smaller staircase.

The original climber waits at his step until the climber he sent finishes his climb.

In terms of a call stack,  
Each climber represents a function call placed on the stack.

The call at the top of the stack is the current step being climbed,  
And the calls below it are the steps waiting to be completed.

Each call waits for the calls above it (the steps yet to be climbed) to complete before it can finish.

So, when you call `ClimbSteps(n)`,  
You place n calls (climbers) on the stack.

As each call completes (each climber reaches the top of their staircase),  
It's removed from the stack.

The process continues until the stack is empty—all steps are climbed,  
And all climbers have finished.

In essence,  
The call stack is crucial to managing the flow of execution in recursive calls,  
Ensuring that each function call is addressed correctly and executed in the correct order,  
No matter how many recursive calls are made.

It is also important to note that the call stack is finite,  
And every recursive call takes up space on the stack.

If you have too many recursive calls,  
You will eventually run out of space on the stack,  
Resulting in a **stack overflow** error.

### Tail Call Optimization

While we did tell you that recursion takes space on the call stack,  
Some modern compilers are smart,  
And can use a cheeky trick called tail call optimization (TCO),  
To reduce the space used by recursion.

In essence, if the very last act of a function is to call itself,  
The compiler can skip adding a new climber and simply let the current one climb further.

In other words,  
The compiler can reuse the current stack frame for the next recursive call instead of adding a new one.

However, not all programming languages support this optimization,  
But when they do, it's like having a single,  
Tireless climber that efficiently completes the climb without causing a queue on the staircase.

Scheme, Erland, and Scala are some of the languages that support TCO, while Python and Java do not.  
JavaScript also supports TCO in the spec, starting with ES6, but it's not yet implemented in most browsers.

So what’s the point?  
Recursive implementations are often more concise and readable when compared with iterative alternatives.  
But they may be undesirable in production workloads because of the potential for stack overflows.  
Tail call recursion unlocks the benefits and avoids the downsides.

## When to Use Recursion?

The beauty of recursion lies in its ability to express complex problems in a few lines of code.

While iterating with loops can achieve the same results,  
The ability to decompose a problem into smaller instances of itself makes recursion a favorite technique in problem-solving.

You may use recursion when the problem fits into one of the following patterns.

### Divide and Conquer
