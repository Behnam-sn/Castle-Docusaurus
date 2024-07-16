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
