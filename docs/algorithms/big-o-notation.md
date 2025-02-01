# Big O Notation

## What is the Big O Notation?

Big O notation is special notation that tells you how fast an algorithm is.

## How Does Big O Notation Works?

Big O establishes a worst-case run time.

Suppose you’re using simple search to look for a person in a phone book.  
You know that simple search takes O(n) time to run.

Which means in the worst case,  
You’ll have to look through every single entry in your phone book.

In this case, you’re looking for Adit.  
This guy is the first entry in your phone book.  
So you didn’t have to look at every entry and you found it on the first try.

Did this algorithm take O(n) time?  
Or did it take O(1) time because you found the person on the first try?  
Simple search still takes O(n) time.

In this case, you found what you were looking for instantly.  
That’s the best-case scenario.

But Big O notation is about the worst-case scenario.  
So you can say in the worst case,  
You’ll have to look at every entry in the phone book once.

That’s O(n) time.  
It’s a reassurance,  
Because you know that simple search will never be slower than O(n) time.

## Some Common Big O Run Times

Here are five Big O run times that you’ll encounter a lot,  
Sorted from fastest to slowest:

- ### O(log n)

  Also known as log time.  
  Example: Binary search.

- ### O(n)

  Also known as linear time.  
  Example: Simple search.

- ### O(n \* log n)

  Example: A fast sorting algorithm, like quicksort.

- ### O(n2)

  Example: A slow sorting algorithm, like selection sort.

- ### O(n!)

  Example: A really slow algorithm, like the traveling salesperson.

## References

- Grokking Algorithms - Aditya Bhargava - Manning
