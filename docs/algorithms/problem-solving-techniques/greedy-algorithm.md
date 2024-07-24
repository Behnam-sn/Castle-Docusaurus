# Greedy Algorithm

## What is a Greedy Algorithm?

A greedy algorithm is a simple, intuitive algorithm that is used in optimization problems.

The algorithm makes the optimal choice at each step as it attempts to find the overall optimal way to solve the entire problem.

Greedy algorithms are quite successful in some problems,  
Such as Huffman encoding which is used to compress data,  
Or Dijkstra's algorithm, which is used to find the shortest path through a graph.

However, in many problems, a greedy strategy does not produce an optimal solution.  
Because it makes decisions based only on the information it has at any one step,  
Without regard to the overall problem.

## When to Use Greedy Algorithms?

If both of the properties below are true,  
A greedy algorithm can be used to solve the problem.

- Greedy Choice Property  
  A global (overall) optimal solution can be reached by choosing the optimal choice at each step.

- Optimal Sub-Structure  
  A problem has an optimal sub-structure if an optimal solution to the entire problem contains the optimal solutions to the sub-problems.

In other words, greedy algorithms work on problems for which it is true that, at every step, there is a choice that is optimal for the problem up to that step, and after the last step, the algorithm produces the optimal solution of the complete problem.

To make a greedy algorithm,  
Identify an optimal substructure or subproblem in the problem.

Then, determine what the solution will include (for example, the largest sum, the shortest path, etc.).

Create some sort of iterative way to go through all of the subproblems and build a solution.

## Limitations of Greedy Algorithms

Sometimes greedy algorithms fail to find the globally optimal solution,  
Because they do not consider all the data.

The choice made by a greedy algorithm may depend on choices it has made so far,  
But it is not aware of future choices it could make.

In problems where greedy algorithms fail, dynamic programming might be a better approach.

## References

- [brilliant.org/wiki/greedy-algorithm/](https://brilliant.org/wiki/greedy-algorithm/)
