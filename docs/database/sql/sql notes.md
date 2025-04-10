# SQL Notes

## What is SQL?

SQL was initially created to be the language for generating, manipulating, and retrieving data from relational databases,  
which have been around for more than 40 years.

Over the past decade or so, however,  
Other data platforms such as Hadoop, Spark, and NoSQL have gained a great deal of traction,  
Eating away at the relational database market.

however, the SQL language has been evolving to facilitate the retrieval of data from various platforms,  
Regardless of whether the data is stored in tables, documents, or flat files.

## Why Learn SQL?

Whether you will be using a relational database or not,  
If you are working in data science, business intelligence, or some other facet of data analysis,  
You will likely need to know SQL.

Data is everywhere, in huge quantities, and arriving at a rapid pace,  
And people who can extract meaningful information from all this data are in big demand.

## Chapter 1. A Little Background

Before we roll up our sleeves and get to work,  
It would be helpful to survey the history of database technology,  
In order to better understand how relational databases and the SQL language evolved.

Therefore, I’d like to start by introducing some basic database concepts,  
And looking at the history of computerized data storage and retrieval.

## Introduction to Databases

A database is nothing more than a set of related information.

A telephone book, for example,  
Is a database of the names, phone numbers, and addresses of all people living in a particular region.

While a telephone book is certainly a ubiquitous and frequently used database,  
It suffers from the following:

- Finding a person’s telephone number can be time consuming, especially if the telephone book contains a large number of entries.

- A telephone book is indexed only by last/first names,  
  So finding the names of the people living at a particular address,  
  While possible in theory,  
  Is not a practical use for this database.

- From the moment the telephone book is printed,  
  The information becomes less and less accurate as people move into or out of a region,  
  Change their telephone numbers,  
  Or move to another location within the same region.

The same drawbacks attributed to telephone books can also apply to any manual data storage system,  
Such as patient records stored in a filing cabinet.

Because of the cumbersome nature of paper databases,  
Some of the first computer applications developed were database systems,  
Which are computerized data storage and retrieval mechanisms.

Because a database system stores data electronically rather than on paper,  
A database system is able to retrieve data more quickly,  
Index data in multiple ways,  
And deliver up-to-the-minute information to its user community.

Early database systems managed data stored on magnetic tapes.  
Because there were generally far more tapes than tape readers,  
Technicians were tasked with loading and unloading tapes as specific data was requested.

Because the computers of that era had very little memory,  
Multiple requests for the same data generally required the data to be read from the tape multiple times.

While these database systems were a significant improvement over paper databases,  
They are a far cry from what is possible with today’s technology.

(Modern database systems can manage petabytes of data,  
Accessed by clusters of servers each caching tens of gigabytes of that data in high-speed memory,  
But I’m getting a bit ahead of myself.)

### Nonrelational Database Systems

Over the first several decades of computerized database systems,  
Data was stored and represented to users in various ways.

In a hierarchical database system, for example,  
Data is represented as one or more tree structures.

### The Relational Model

In 1970, Dr. E. F. Codd of IBM’s research laboratory published
a paper titled “A Relational Model of Data for Large Shared
Data Banks” that proposed that data be represented as sets of
tables. Rather than using pointers to navigate between related
entities, redundant data is used to link records in different
tables.

## Terminology

- Entity
  Something of interest to the database user community.  
  Examples include customers, parts, geographic locations, etc.

- Column
  An individual piece of data stored in a table.

- Row
  A set of columns that together completely describe an entity or some action on an entity.  
  Also called a record.

- Table
  A set of rows, held either in memory (nonpersistent) or on permanent storage (persistent).

- Result set
  Another name for a nonpersistent table, generally the result of an SQL query.

- Primary key
  One or more columns that can be used as a unique identifier for each row in a table.

- Foreign key
  One or more columns that can be used together to identify a single row in another table.

## What Is SQL?

Along with Codd’s definition of the relational model,  
He proposed a language called DSL/Alpha for manipulating the data in relational tables.

Shortly after Codd’s paper was released,  
IBM commissioned a group to build a prototype based on Codd’s ideas.

This group created a simplified version of DSL/Alpha that they called SQUARE.

Refinements to SQUARE led to a language called SEQUEL,  
Which was finally shortened to SQL.

While SQL began as a language used to manipulate data in relational databases,  
It has evolved to be a language for manipulating data across various database technologies.

SQL is now more than 40 years old,  
And it has undergone a great deal of change along the way.

In the mid-1980s,  
The American National Standards Institute (ANSI),  
Began working on the first standard for the SQL language,  
Which was published in 1986.

Subsequent refinements led to new releases of the SQL standard in 1989, 1992, 1999, 2003, 2006, 2008, 2011, and 2016.

Along with refinements to the core language,  
New features have been added to the SQL language,  
To incorporate object-oriented functionality, among other things.

The later standards focus on the integration of related technologies,  
Such as extensible markup language (XML) and JavaScript object notation (JSON).

SQL goes hand in hand with the relational model,  
Because the result of an SQL query is a table (also called, in this context, a result set).

Thus, a new permanent table can be created in a relational database,  
Simply by storing the result set of a query.

Similarly, a query can use both permanent tables and the result sets from other queries as inputs.

One final note:  
SQL is not an acronym for anything.  
Although many people will insist it stands for “Structured Query Language”.

When referring to the language,  
It is equally acceptable to say the letters individually (i.e., S. Q. L.) or to use the word _sequel_.
