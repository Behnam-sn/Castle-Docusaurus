# Greedy Algorithm

## What is a Greedy Algorithm?

A greedy algorithm is a simple and intuitive algorithm that is used in optimization problems.

The algorithm makes the optimal choice at each step,  
As it attempts to find the overall optimal way to solve the entire problem.

## When to Use a Greedy Algorithm?

Greedy algorithms are quite successful in some problems,  
Such as Huffman encoding which is used to compress data,  
Or Dijkstra's algorithm which is used to find the shortest path through a graph.

If both of the properties below are true,  
A greedy algorithm can be used to solve the problem.

- ### Greedy Choice Property

  A global (overall) optimal solution can be reached by choosing the optimal choice at each step.

- ### Optimal Sub-Structure

  A problem has an optimal sub-structure,  
  If an optimal solution to the entire problem,  
  Contains the optimal solutions to the sub-problems.

## How to Use a Greedy Algorithm?

To make a greedy algorithm:

1. Identify an optimal sub-structure or sub-problem in the problem.

1. Then, determine what the solution will include.  
   For example, the largest sum, the shortest path, etc.

1. Create some sort of iterative way to go through all of the sub-problems and build a solution.

## Limitations of Greedy Algorithms

Sometimes greedy algorithms fail to find the globally optimal solution,  
Because they do not consider all the data.

The choice made by a greedy algorithm may depend on choices it has made so far,  
But it is not aware of future choices it could make.

In problems where greedy algorithms fail,  
Dynamic programming might be a better approach.

## References

- [brilliant.org/wiki/greedy-algorithm/](https://brilliant.org/wiki/greedy-algorithm/)
