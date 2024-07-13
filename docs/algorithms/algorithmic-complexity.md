# Algorithmic Complexity

you will explore computational complexity (space and time complexity),

An algorithm's complexity is a measure of the amount of data that it must process in order to be efficient.

Domain and range of this function are generally expressed in natural units.

## What is Time Complexity?

Time complexity is defined in terms of how many times it takes to run a given algorithm,  
Based on the length of the input.

Time complexity is not a measurement of how much time it takes to execute a particular algorithm because such factors as programming language, operating system, and processing power are also considered.

Time complexity is a type of computational complexity that describes the time required to execute an algorithm.

The time complexity of an algorithm is the amount of time it takes for each statement to complete.

As a result, it is highly dependent on the size of the processed data.

It also aids in defining an algorithm's effectiveness and evaluating its performance.

Time complexity is defined as the amount of time taken by an algorithm to run, as a function of the length of the input. It measures the time taken to execute each statement of code in an algorithm. It is not going to examine the total execution time of an algorithm. Rather, it is going to give information about the variation (increase or decrease) in execution time when the number of operations (increase or decrease) in an algorithm.

## What is Space Complexity?

When an algorithm is run on a computer, it necessitates a certain amount of memory space.

The amount of memory used by a program to execute it is represented by its space complexity.

Because a program requires memory to store input data and temporal values while running, the space complexity is auxiliary and input space.

## What Does It Take To Develop a Good Algorithm?

A good algorithm executes quickly and saves space in the process.

You should find a happy medium of space and time (space and time complexity), but you can do with the average.

## What Are Asymptotic Notations?

Asymptotic Notations are programming languages that allow you to analyze an algorithm's running time by identifying its behavior as its input size grows.

This is also referred to as an algorithm's growth rate.

When the input size increases,  
Does the algorithm become incredibly slow?

Is it able to maintain its fast run time as the input size grows?

You can answer these questions thanks to Asymptotic Notation.

You can't compare two algorithms head to head.

It is heavily influenced by the tools and hardware you use for comparisons,  
Such as the operating system, CPU model, processor generation, and so on.

Even if you calculate time and space complexity for two algorithms running on the same system,  
The subtle changes in the system environment may affect their time and space complexity.

As a result,  
You compare space and time complexity using asymptotic analysis.

It compares two algorithms based on changes in their performance as the input size is increased or decreased.

Asymptotic notations are classified into three types:

- ### Big-O (O) notation

  Paul Bachmann invented the big-O notation in 1894.

  He inadvertently introduced this notation in his discussion of function approximation.

  It is the most widely used notation for Asymptotic analysis.

  It specifies the upper bound of a function, i.e., the maximum time required by an algorithm or the worst-case time complexity.

  In other words, it returns the highest possible output value (big-O) for a given input.

- ### Big Omega ( Ω ) notation

  Big-Omega is an Asymptotic Notation for the best case or a floor growth rate for a given function.

  It gives you an asymptotic lower bound on the growth rate of an algorithm's runtime.

- ### Big Theta ( Θ ) notation

  Big theta defines a function's lower and upper bounds, i.e., it exists as both, most, and least boundaries for a given input value.

Asymptotic Analysis Cases:

Best Case:

It is defined as the condition that allows an algorithm to complete statement execution in the shortest amount of time.

In this case, the execution time serves as a lower bound on the algorithm's time complexity.

Average Case:

You add the running times for each possible input combination and take the average in the average case.

Here, the execution time serves as both a lower and upper bound on the algorithm's time complexity.

Worst Case:

It is defined as the condition that allows an algorithm to complete statement execution in the longest amount of time possible.

In this case, the execution time serves as an upper bound on the algorithm's time complexity.

## Significant in Terms of Space Complexity

Space complexity refers to the total amount of memory space used by an algorithm/program,  
Including the space of input values for execution.

Calculate the space occupied by variables in an algorithm/program to determine space complexity.

However, people frequently confuse Space-complexity with auxiliary space.

Auxiliary space is simply extra or temporary space, and it is not the same as space complexity.

To put it another way,

Auxiliary space + space use by input values = Space Complexity

The best algorithm/program should have a low level of space complexity.

The less space required, the faster it executes.

## Time Complexity vs. Space Complexity

|                    Time Complexity                    |                        Space Complexity                        |
| :---------------------------------------------------: | :------------------------------------------------------------: |
|             Calculates the time required              |              Estimates the space memory required               |
|          Time is counted for all statements           | Memory space is counted for all variables, inputs, and outputs |
| The size of the input data is the primary determinant |      Primarily determined by the auxiliary variable size       |

## References

- [simplilearn.com/tutorials/data-structure-tutorial/time-and-space-complexity](https://www.simplilearn.com/tutorials/data-structure-tutorial/time-and-space-complexity)
- https://medium.com/@akshayroy21/what-is-time-complexity-and-why-is-it-essential-93d696e6cf65
- https://www.mygreatlearning.com/blog/why-is-time-complexity-essential/
- https://en.wikipedia.org/wiki/Time_complexity
- https://www.britannica.com/science/time-complexity
- https://www.geeksforgeeks.org/time-complexity-and-space-complexity/
- https://www.geeksforgeeks.org/understanding-time-complexity-simple-examples/
