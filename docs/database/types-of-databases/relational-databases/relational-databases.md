# Relational Databases

## What is a Relational Database?

A relational database organizes data into rows and columns, which collectively form a table.

Data is typically structured across multiple tables,
which can be joined together via a primary key or a foreign key.

These unique identifiers
demonstrate the different relationships which exist between tables,
and these relationships are usually illustrated through different types of data models.

## SQL

The most common way of interacting with relational database systems is
using SQL (Structured Query Language).

Developers can write SQL queries to perform CRUD (Create, Read, Update, Delete) operations.

## Relational Database Example

Imagine you run an online business.

You have a variety of information that you store,
like customer information, order information, and products.

In a relational database,
this would be stored in different tables with a key to join the tables when needed.

The customer table stores the basic customer information, order id and address id.
If someone needs more information on the order or address,
they can query the matching order and address tables
using an INNER JOIN operator with the id field.

The order table in turn has product ids of the product items in the order.
The details of the product are in a separate product table.

This makes information organized and more structured.

## Some relational databases Implementations:

- Microsoft SQL Server
- PostgreSQL
- MySQL
- Oracle Database
- SQLite
- MariaDB
- IBM Db2

Advantages of relational databases:

- ACID compliance

  Atomicity, Consistency, Isolation, and Durability (ACID)
  is a standard that guarantees the reliability of database transactions.
  The general principle is if one change fails,
  the whole transaction will fail,
  and the database will remain in the state it was in before the transaction was attempted.

  This is important
  because some transactions will have real consequences if not completed fully,
  for example, banking.

- Data accuracy

  Using primary and foreign keys
  allows you to ensure there is no duplicate information.

  This helps enforce data accuracy because there will never be repeated information.

- Normalization

  The process of normalization involves
  ensuring the data is organized in such a way that data anomalies are reduced or eliminated.
  This, in turn, reduces storage costs.

- Simplicity
  RDMS, or SQL databases, have been around for so long
  that a wide variety of tools and resources have been developed to
  help you get started and interact with relational databases.

## Disadvantages of relational databases:

- Scalability

  RDMSs are historically intended to be run on a single machine.
  This means that if the requirements of the machine are insufficient,
  due to data size or an increase in the frequency of access,
  you will have to improve the hardware in the machine, also known as vertical scaling.

  This can be incredibly expensive and has a ceiling,
  as eventually the costs outweigh the benefits.
  Plus, there will potentially come a stage where you simply
  cannot get hardware capable of hosting the database.

  The only solution would be to
  buy a machine that supports better hardware, but none of that is cheap.

- Flexibility

  In relational databases, the schema is rigid.
  You define the columns and data types for those columns,
  including any restraints such as format or length.

  Although this means you can interpret the data more easily
  and identify the relationships between tables.

  Also it means that making changes to the structure of the data is very complex.
  You have to decide at the start what the data will look like,
  which isn’t always possible.

  If you want to make changes later,
  you have to change all the data,
  which involves the database being offline temporarily.

- Performance
  The performance of the database is tightly linked to the complexity of the tables,
  the number of them, as well as the amount of data in each table.
  As this increases, the time taken to perform queries increases too.

## References

[www.ibm.com/topics/relational-databases](https://www.ibm.com/topics/relational-databases)
[www.mongodb.com/compare/relational-vs-non-relational-databases](https://www.mongodb.com/compare/relational-vs-non-relational-databases)
