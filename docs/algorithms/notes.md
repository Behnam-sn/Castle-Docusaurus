# Notes

## Algorithms Task

- Write Binary Search in C#
- Write Simple Search in C#
- Write Breadth-First Search in C#
- Write Depth-First Search in C#
- Implement AVL trees
- Implement Dijkstra Algorithm

## Algorithms

- Simple Search
- Binary Search
- Selection Sort
- Quick Sort
- Merge Sort
- Breadth-First Search  
  Breadth-first search is a traversal algorithm.  
  That means it is an algorithm that visits every node in a tree—that is, it traverses or walks the tree.
- Depth-First Search
- Dijkstra Algorithm  
  Breadth-first search is used to calculate the shortest path for an unweighted graph.  
  Dijkstra’s algorithm is used to calculate the shortest path for a weighted graph.  
  Dijkstra’s algorithm works when all the weights are nonnegative.  
  If you have negative weights, use the Bellman–Ford algorithm.
- Bellman–Ford Algorithm
- k-nearest neighbors algorithm
  KNN is used for classification and regression and involves looking at the k-nearest neighbors.
  Classification: categorization into a group
  Normalization
  Regression: predicting a response (like a number)
  Feature extraction means converting an item (like a fruit or a user) into a list of numbers that can be compared.
  Cosine similarity

## Extra Algorithms

- Linear regression
- Inverted indexes
- The Fourier transform
- Parallel algorithms
- distributed algorithm (map/reduce)
- probabilistic algorithms (Bloom filters and HyperLogLog)
- HTTPS and the Diffie–Hellman key exchange
- Min heaps and priority queues
- heap sort
- Simplex algorithm (Linear programming)

## Data Structures

- Array
- linked List
- Stack  
  Last In First Out  
  Push & Pop
- Queue  
  First In First Out  
  Enqueue & Dequeue
- Set
- Hash Tables
  - Hash functions
  - They’re also known as hash maps, maps, dictionaries, and associative arrays.
  - hashes are good for:
  - Modeling relationships from one thing to another thing
  - Filtering out duplicates
  - Caching/memoizing data instead of making your server do work
- Graphs
- Tree
  Trees are a subset of graphs.
  A tree is a special type of graph where no edges ever point back.
  Nodes can have children, and child nodes can have a parent.
  In a tree, nodes have at most one parent.
  The only node with no parents is the root.
  Nodes with no children are called leaf nodes.
  trees don’t have cycles.
  A tree is a connected, acyclic graph.
  Rooted trees have one node that leads to all the other nodes.
  root
  leaf
  parent
  child
  - Binary Trees
  - B-tree
  - Balanced Trees
  - Balanced Binary Search Tree
    - AVL trees
      Rotations
    - Splay trees
    - B-trees
- vectors

## Math

- Algebra
- Factorial

## Concepts

- Recursion
  Recursion is used when it makes the solution clearer.  
  There’s no performance benefit to using recursion; in fact, loops are sometimes better for performance.
- Functional Programming
- Cryptography
  - Euclid’s algorithm
- Pseudo Code
  Pseudo Code is a high-level description in code of the problem you’re trying to solve.
  It’s written like code, but it’s meant to be closer to human speech.
- compression algorithm
- Huffman coding
- topological sort
- NP-hard problems
- power set
- approximation algorithms
- dynamic programming  
  Dynamic programming starts by solving sub-problems and builds up to solving the big problem.  
  Every dynamic programming algorithm starts with a grid.
  Dynamic programming is powerful because it can solve.
  sub-problems and use those answers to solve the big problem.
  Dynamic programming only works when each subproblem is discrete—when it doesn’t depend on other sub-problems.
  Dynamic programming is useful when you’re trying to optimize something given a constraint.
  You can use dynamic programming when the problem can be broken into discrete sub-problems.
  Every dynamic programming solution involves a grid.
  The values in the cells are usually what you’re trying to optimize.
  Each cell is a subproblem, so think about how you can divide your problem into sub-problems.
  There’s no single formula for calculating a dynamic programming solution.

## Strategy

- Divide and Conquer
- Greedy Strategy

## Running Time

## Binary Search

## the main takeaways are as follows

- Algorithm speed isn’t measured in seconds, but in growth of the number of operations.
- Instead, we talk about how quickly the run time of an algorithm increases as the size of the input increases.
- Run time of algorithms is expressed in Big O notation.
- O(log n) is faster than O(n), but it gets a lot faster as the list of items you’re searching grows.

## The traveling salesperson

## Math

- Algebra
- Logarithms
- Factorial

Recap

- Binary search is a lot faster than simple search.
- O(log n) is faster than O(n), but it gets a lot faster once the list of items you’re searching through grows.
- Algorithm speed isn’t measured in seconds.
- Algorithm times are measured in terms of growth of an algorithm.
- Algorithm times are written in Big O notation.

There are two different types of access: random access and sequential access.
