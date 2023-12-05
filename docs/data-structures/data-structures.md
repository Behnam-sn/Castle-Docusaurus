# Data Structures

## What is a Data Structure?

A **data structure** is a data organization, management, and storage format.  
It is a way of arranging data on a computer so that it can be accessed and updated efficiently.

More precisely, a data structure is a collection of data values, the relationships among them, and the functions or operations that can be applied to the data, that is an algebraic structure about data.

## Why

There are different basic and advanced types of data structures that are used in almost every program or software system that has been developed.  
So we must have good knowledge about data structures.

## Usage

Data structures serve as the basis for abstract data types (ADT).  
The ADT defines the logical form of the data type.  
The data structure implements the physical form of the data type.

Different types of data structures are suited to different kinds of applications,  
And some are highly specialized to specific tasks.  
For example, relational databases commonly use B-tree indexes for data retrieval,  
While compiler implementations usually use hash tables to look up identifiers.

Data structures provide a means to manage large amounts of data efficiently for uses such as large databases and internet indexing services.  
Usually, efficient data structures are key to designing efficient algorithms.

Some formal design methods and programming languages emphasize data structures, rather than algorithms, as the key organizing factor in software design.  
Data structures can be used to organize the storage and retrieval of information stored in both main memory and secondary memory.

## Implementation

Data structures can be implemented using a variety of programming languages and techniques,  
But they all share the common goal of efficiently organizing and storing data.
Data structures are generally based on the ability of a computer to fetch and store data at any place in its memory, specified by a pointer—a bit string, representing a memory address, that can be itself stored in memory and manipulated by the program.  
Thus, the array and record data structures are based on computing the addresses of data items with arithmetic operations, while the linked data structures are based on storing addresses of data items within the structure itself.  
This approach to data structuring has profound implications for the efficiency and scalability of algorithms.  
For instance, the contiguous memory allocation in arrays facilitates rapid access and modification operations, leading to optimized performance in sequential data processing scenarios.

The implementation of a data structure usually requires writing a set of procedures that create and manipulate instances of that structure.  
The efficiency of a data structure cannot be analyzed separately from those operations.
This observation motivates the theoretical concept of an abstract data type,  
A data structure that is defined indirectly by the operations that may be performed on it,  
And the mathematical properties of those operations (including their space and time cost).

## Types of Data Structures

There are numerous types of data structures,  
Generally built upon simpler primitive data types.  
Well known examples are:

### Array

An array is a number of elements in a specific order,  
Typically all of the same type (depending on the language, individual elements may either all be forced to be the same type, or may be of almost any type).  
Elements are accessed using an integer index to specify which element is required.  
Typical implementations allocate contiguous memory words for the elements of arrays (but this is not always a necessity).  
Arrays may be fixed-length or resizable.

### Linked list

## Language Support

Most assembly languages and some low-level languages, such as BCPL (Basic Combined Programming Language), lack built-in support for data structures. On the other hand, many high-level programming languages and some higher-level assembly languages, such as MASM, have special syntax or other built-in support for certain data structures, such as records and arrays. For example, the C (a direct descendant of BCPL) and Pascal languages support structs and records, respectively, in addition to vectors (one-dimensional arrays) and multi-dimensional arrays.[14][15]

Most programming languages feature some sort of library mechanism that allows data structure implementations to be reused by different programs. Modern languages usually come with standard libraries that implement the most common data structures. Examples are the C++ Standard Template Library, the Java Collections Framework, and the Microsoft .NET Framework.

Modern languages also generally support modular programming, the separation between the interface of a library module and its implementation. Some provide opaque data types that allow clients to hide implementation details. Object-oriented programming languages, such as C++, Java, and Smalltalk, typically use classes for this purpose.

Many known data structures have concurrent versions which allow multiple computing threads to access a single concrete instance of a data structure simultaneously.[16]

## References

- https://en.wikipedia.org/wiki/Data_structure
- https://www.geeksforgeeks.org/data-structures/
- https://www.simplilearn.com/tutorials/data-structure-tutorial/what-is-data-structure
