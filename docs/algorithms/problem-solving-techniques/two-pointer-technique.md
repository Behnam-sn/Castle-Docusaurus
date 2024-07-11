# Two Pointer Technique

## What is The Two Pointer Technique?

Two pointer problems are among the most common types you will encounter during coding interviews.

This technique involves using two pointers,  
Which move through linear data structures,  
Such as arrays, linked lists, or strings,  
In a synchronized or independent manner to solve a problem.

## What are Types of Two Pointer Usage?

### Polynomial Pointers

This pointer variety is generally considered the least beneficial,  
As it often necessitates the use of nested loops and for brute force combinations.

In this setup, each pointer travels independently across each index of the input.

This pattern typically results in a polynomial (commonly quadratic – O(N^2)) time complexity,  
Due to the fact that it computes all potential combinations of two pointers within a single linear input.

The bubble sort algorithm exemplifies this kind of pointer usage.

### Pointer Chasing For Cycle Detection

This variant of the two-pointer technique,  
Is notably applied in identifying cycles in linked lists and graphs,  
As demonstrated in Floyd's algorithm.

In this setup, both pointers initiate their journey from the beginning of the input (typically index 0),  
But progress at varied speeds.

Generally, the "tortoise" pointer advances by just one index in each step,  
Whereas the "hare" pointer leaps forward by two indices at a time.

### Rivaling Pointers

In this variant of the two-pointer technique,  
One pointer commences at the start of the input,  
While the other initiates from the input's end.

These pointers subsequently shift inwardly (toward each other) alternately,  
Adhering to a predefined logic.

The binary search algorithm or Palindrome problem both serve as textbook examples of this type of problem.

### Multiple Pointers

While traditionally two-pointer problems involve exactly two pointers,  
It's not uncommon to encounter problems where more than two pointers can be beneficial.

In this setup, pointers move independently or in a correlated manner based on specific logic.

This type of problem often shows up in more complex array or string problems,  
Where the interaction between multiple elements at different positions needs to be considered.

For instance, a problem might require you to sort an array of zeros, ones, and twos as in the Dutch Flag problem.

A polynomial pointer approach can solve the problem in quadratic time.  
However, by cleverly segregating the array with three pointers,  
You can reduce the time complexity to linear time.

### Double Input Pointers

This pointer type is interesting,  
Since it involves two linear inputs, with a single pointer on each,  
Rather than a single input with two pointers.

A common example of this would be the “merge” part of the Merge Sort algorithm,  
In which we merge two sorted lists into a single list,  
By carefully comparing and updating pointers in each list based on their relative values.

## When to Use Two Pointer Technique?

Two pointer problems usually surface,  
When dealing with ordered data or,  
When there is a need to eliminate redundant computations.

Here are a few scenarios when this technique can be particularly handy:

- ### Searching pairs in a sorted array

  The pointers can start at both ends of the array and move inward until they meet,  
  Eliminating possible pairs along the way.

  This method is faster than using a nested loop to check all pairs.

- ### Finding a cycle in a linked list

  One pointer can move faster (2 steps at a time),  
  And the other slower (1 step at a time).

  If there is a cycle, the faster pointer will eventually meet the slower one.

- ### Checking for palindromes

  The pointers can start at both ends and move inward,  
  Checking if the mirrored characters are the same.

- ### Applying a sliding window

  One pointer marks the start of the window, the other the end.  
  The window can then be 'slid' through the array to check for conditions.

## References

- [interviewing.io/two-pointers-interview-questions](https://interviewing.io/two-pointers-interview-questions)
