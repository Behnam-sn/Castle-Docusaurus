# Data Orientation

## What is a columnar database?

A columnar database, also known as a column-oriented database, is a type of database management system (DBMS) that stores data in columns together on disk. This enables faster queries for data analytics, which generally involves filtering and aggregating table columns.

Compare columnar databases to row-oriented databases, in which the contents of a single row are stored together on disk. These types of databases are optimized for transactional, single-entity lookup instead of analytics over many entities.

Columnar databases are particularly advantageous for analytics queries that frequently scan or aggregate over large datasets but only need a few columns. Because only the necessary columns are read from storage, I/O costs and time are minimized, providing an edge over traditional row-based databases in analytics scenarios. For these use cases, columnar databases use system resources more efficiently and yield quicker insights.

Columnar databases are great for data analytics. They scan fewer rows and process less data than row-oriented databases.

Beyond just the way they store data, columnar databases also provide some features that can be quite useful for real-time analytics or time series data, such as…

- Probabilistic data structures
- Fast write throughput with log-structured merge tree (LSMT)
- Incremental rollups and materializations
- Specialized SQL functions for statistics, analytics, and time series data

## When should I use a columnar database?

You should use columnar databases when you intend to filter and aggregate data logically stored in columns. For example, consider a generic data table that looks like this:

| user_id | user_name            | current_balance | number_of_transactions |
| ------- | -------------------- | --------------- | ---------------------- |
| 1       | 'freddie@gmail.com'  | 1059298         | 1224                   |
| 2       | 'lindsey@gmail.com'  | 254             | 1045                   |
| 3       | 'tabby@yahoo.com'    | 3910            | 194                    |
| 4       | 'philip@hotmail.com' | 234028          | 130                    |
| 5       | 'elon@x.com'         | -44000000000    | 1                      |

A query like…

this is Better for column-oriented databases

```sql
SELECT sum(current_balance) AS total_transactions
FROM table
WHERE user_id > 2
```

… would benefit from columnar data storage, as it needs to access only data in the `current_balance` column and can utilize indexing to filter by the `user_id` column and minimize rows read.

Conversely, a query like…

Better for row-oriented databases

```sql
SELECT user_id, user_name, current_balance
FROM table
WHERE user_id = 1
```

…would benefit from row-oriented data storage, as it seeks to access and look up a single row of data indexed by a primary key, `user_id`.

Of course, this is an oversimplification. Even a minimally resourced row-oriented database could easily handle a column aggregation on a table with only five rows. The amount of data stored has a huge influence on whether a column-oriented database will be more performant than a row-oriented database. With big data, column-oriented databases become especially useful.

The amount of data stored has a huge influence on the performance gap between columnar databases and row-oriented databases.

### Use columnar databases for real-time analytics

Columnar databases generally excel at real-time analytics, where high write throughput and low latency on complex, analytical queries are required.

Or consider event-driven architectures or event sourcing approaches, where state is maintained by aggregating a long history of timestamped events, rather than in a table using upserts or replaces. Storing and aggregating time series data can be very difficult for row-oriented, relational databases, but columnar databases handle time-series analytics very well.

Ultimately, it comes down to basic physics. Data in most databases is stored on disk and accessed from disk, and column-oriented databases store data differently than row-oriented databases. An analytical, columnar database provides distinct advantages when you want to access data in columns very quickly while eschewing some of the benefits that make transactional, row-oriented databases useful.

## When should I avoid columnar databases?

You should avoid columnar databases when you don't intend to do complex analytics and you want to retain the benefits of transactional, row-oriented databases. For example, columnar databases are generally not optimized for frequent single-row updates or deletes, both of which are important functions of traditional databases used for online transaction processing.

The benefits of columnar databases become much more pronounced when working with large amounts of data, but you might want a columnar database even for small datasets (especially if you expect that data to grow).

Similarly, you may not need to use a columnar database if you are working with smaller amounts of data. While there's nothing technically "wrong" with using a columnar database with smaller data sets, these databases generally have a steeper learning curve, and you can likely achieve what you need with more comfortable and broadly supported relational databases like Postgres or MySQL.

USE COLUMNAR DATABASES WHEN... - USE ROW-ORIENTED DATABASES WHEN...
Your primary use case is analytics - Your primary use case is transactions
You need low query latency - You don't need low query latency (for analytics)
You have large amounts of data - You're working with smaller data (for analytics)
You don't need strict ACID compliance - You need strict ACID compliance
You're using event sourcing principles - You need to do frequent, small replaces and deletes
You need to store and analyze lots of time series data - You need to store and access records with unique IDs

## References

- [https://www.tinybird.co/blog-posts/what-is-a-columnar-database](https://www.tinybird.co/blog-posts/what-is-a-columnar-database)

## Read More

- [https://www.tinybird.co/blog-posts/when-to-use-columnar-database](https://www.tinybird.co/blog-posts/when-to-use-columnar-database)
