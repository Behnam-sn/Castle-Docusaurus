# Big O notation

## What is the Big O notation?

Big O notation is special notation that tells you how fast an algorithm is.

## Big O establishes a worst-case run time

Suppose you’re using simple search to look for a person in the phone
book. You know that simple search takes O(n) time to run, which
means in the worst case, you’ll have to look through every single entry
in your phone book. In this case, you’re looking for Adit. This guy is
the first entry in your phone book. So you didn’t have to look at every
entry—you found it on the first try. Did this algorithm take O(n) time?
Or did it take O(1) time because you found the person on the first try?
Simple search still takes O(n) time. In this case, you found what you
were looking for instantly. That’s the best-case scenario. But Big O
notation is about the worst-case scenario. So you can say that, in the
worst case, you’ll have to look at every entry in the phone book once.
That’s O(n) time. It’s a reassurance—you know that simple search will
never be slower than O(n) time.

## Some common Big O run times

Here are five Big O run times that you’ll encounter a lot, sorted from fastest to slowest:

- O(log n), also known as log time.  
  Example: Binary search.

- O(n), also known as linear time.  
  Example: Simple search.

- O(n \* log n)  
  Example: A fast sorting algorithm, like quicksort

- O(n2)  
  Example: A slow sorting algorithm, like selection sort

- O(n!)  
  Example: A really slow algorithm, like the traveling salesperson.

## References

- Grokking Algorithms - Aditya Bhargava - Manning
