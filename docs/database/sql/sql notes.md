# SQL Notes

## What is SQL?

SQL was initially created to be the language for generating,
manipulating, and retrieving data from relational databases,
which have been around for more than 40 years. Over the past
decade or so, however, other data platforms such as Hadoop,
Spark, and NoSQL have gained a great deal of traction, eating
away at the relational database market.

however, the SQL language
has been evolving to facilitate the retrieval of data from various
platforms, regardless of whether the data is stored in tables,
documents, or flat files.

## Why Learn SQL?

Whether you will be using a relational database or not, if you
are working in data science, business intelligence, or some
other facet of data analysis, you will likely need to know SQL.
Data is everywhere, in huge quantities, and arriving at a rapid
pace, and people who can extract meaningful information from
all this data are in big demand.

## Chapter 1. A Little Background

Before we roll up our sleeves and get to work, it would be
helpful to survey the history of database technology in order to
better understand how relational databases and the SQL
language evolved. Therefore, I’d like to start by introducing
some basic database concepts and looking at the history of
computerized data storage and retrieval.

## Introduction to Databases

A database is nothing more than a set of related information. A
telephone book, for example, is a database of the names,
phone numbers, and addresses of all people living in a
particular region. While a telephone book is certainly a
ubiquitous and frequently used database, it suffers from the
following:

- Finding a person’s telephone number can be time
  consuming, especially if the telephone book contains a
  large number of entries.

- A telephone book is indexed only by last/first names,
  so finding the names of the people living at a particular
  address, while possible in theory, is not a practical use
  for this database.

- From the moment the telephone book is printed, the
  information becomes less and less accurate as people
  move into or out of a region, change their telephone
  numbers, or move to another location within the same
  region.

The same drawbacks attributed to telephone books can also
apply to any manual data storage system, such as patient
records stored in a filing cabinet. Because of the cumbersome
nature of paper databases, some of the first computer
applications developed were database systems, which are
computerized data storage and retrieval mechanisms. Because
a database system stores data electronically rather than on
paper, a database system is able to retrieve data more quickly,
index data in multiple ways, and deliver up-to-the-minute
information to its user community.

Early database systems managed data stored on magnetic
tapes. Because there were generally far more tapes than tape
readers, technicians were tasked with loading and unloading
tapes as specific data was requested. Because the computers
of that era had very little memory, multiple requests for the
same data generally required the data to be read from the tape
multiple times. While these database systems were a
significant improvement over paper databases, they are a far
cry from what is possible with today’s technology. (Modern
database systems can manage petabytes of data, accessed by
clusters of servers each caching tens of gigabytes of that data
in high-speed memory, but I’m getting a bit ahead of myself.)

### Nonrelational Database Systems

Over the first several decades of computerized database
systems, data was stored and represented to users in various
ways. In a hierarchical database system, for example, data is
represented as one or more tree structures.
