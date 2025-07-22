# Data Orientation Notes

## What Is A Columnar Database?

A columnar database,  
Also known as a column-oriented database,  
Is a type of database management system (DBMS) that stores data in columns together on disk.

This enables faster queries for data analytics,  
Which generally involves filtering and aggregating table columns.

Compare columnar databases to row-oriented databases,  
In which the contents of a single row are stored together on disk.  
These types of databases are optimized for transactional,  
Single-entity lookup instead of analytics over many entities.

Columnar databases are particularly advantageous for analytics queries that frequently scan or aggregate over large datasets,  
But only need a few columns.

Because only the necessary columns are read from storage,  
I/O costs and time are minimized,  
Providing an edge over traditional row-based databases in analytics scenarios.

For these use cases,  
Columnar databases use system resources more efficiently and yield quicker insights.

Columnar databases are great for data analytics.  
They scan fewer rows and process less data than row-oriented databases.

Beyond just the way they store data,  
Columnar databases also provide some features that can be quite useful for real-time analytics or time series data,  
Such as:

- Probabilistic data structures
- Fast write throughput with log-structured merge tree (LSMT)
- Incremental rollups and materializations
- Specialized SQL functions for statistics, analytics, and time series data

## When Should I Use A Columnar Database?

You should use columnar databases,  
When you intend to filter and aggregate data logically stored in columns.

For example,  
Consider a generic data table that looks like this:

| user_id | user_name            | current_balance | number_of_transactions |
| ------- | -------------------- | --------------- | ---------------------- |
| 1       | 'freddie@gmail.com'  | 1059298         | 1224                   |
| 2       | 'lindsey@gmail.com'  | 254             | 1045                   |
| 3       | 'tabby@yahoo.com'    | 3910            | 194                    |
| 4       | 'philip@hotmail.com' | 234028          | 130                    |
| 5       | 'elon@x.com'         | -44000000000    | 1                      |

A query like this:

```sql
SELECT sum(current_balance) AS total_transactions
FROM table
WHERE user_id > 2
```

Would benefit from columnar data storage,  
As it needs to access only data in the `current_balance` column,  
And can utilize indexing to filter by the `user_id` column and minimize rows read.

Conversely, a query like this:

```sql
SELECT user_id, user_name, current_balance
FROM table
WHERE user_id = 1
```

Would benefit from row-oriented data storage,  
As it seeks to access and look up a single row of data indexed by a primary key, `user_id`.

Of course, this is an oversimplification.

Even a minimally resourced row-oriented database,  
Could easily handle a column aggregation on a table with only five rows.

The amount of data stored has a huge influence on whether a column-oriented database will be more performant than a row-oriented database.

### Use Columnar Databases For Real-Time Analytics

Columnar databases generally excel at real-time analytics,  
Where high write throughput and low latency on complex, analytical queries are required.

Or consider event-driven architectures or event sourcing approaches,  
Where state is maintained by aggregating a long history of timestamped events,  
Rather than in a table using upserts or replaces.

Storing and aggregating time series data can be very difficult for row-oriented, relational databases,  
But columnar databases handle time-series analytics very well.

Ultimately, it comes down to basic physics.

Data in most databases is stored on disk and accessed from disk,  
And column-oriented databases store data differently than row-oriented databases.

An analytical, columnar database provides distinct advantages,  
When you want to access data in columns very quickly,  
While eschewing some of the benefits that make transactional, row-oriented databases useful.

## When Should I Avoid Columnar Databases?

You should avoid columnar databases,  
When you don't intend to do complex analytics,  
And you want to retain the benefits of transactional, row-oriented databases.

For example,  
Columnar databases are generally not optimized for frequent single-row updates or deletes,  
Both of which are important functions of traditional databases used for online transaction processing.

The benefits of columnar databases become much more pronounced when working with large amounts of data,  
But you might want a columnar database even for small datasets.  
Especially if you expect that data to grow.

Similarly, you may not need to use a columnar database if you are working with smaller amounts of data.

While there's nothing technically "wrong" with using a columnar database with smaller data sets,  
These databases generally have a steeper learning curve,  
And you can likely achieve what you need with more comfortable and broadly supported relational databases like Postgres or MySQL.

| USE COLUMNAR DATABASES WHEN...                         | USE ROW-ORIENTED DATABASES WHEN...                   |
| ------------------------------------------------------ | ---------------------------------------------------- |
| Your primary use case is analytics                     | Your primary use case is transactions                |
| You need low query latency                             | You don't need low query latency (for analytics)     |
| You have large amounts of data                         | You're working with smaller data (for analytics)     |
| You don't need strict ACID compliance                  | You need strict ACID compliance                      |
| You're using event sourcing principles                 | You need to do frequent, small replaces and deletes  |
| You need to store and analyze lots of time series data | You need to store and access records with unique IDs |

:::note
Keep in mind that column-oriented storage isn't a silver bullet for query latency on complex analytics.

Even with the most performant columnar databases,  
You still must consider proper indexing, sorting, partitioning,  
And replication mechanisms to maintain and optimize the performance of column-oriented databases at scale.
:::

## References

- [https://www.tinybird.co/blog-posts/what-is-a-columnar-database](https://www.tinybird.co/blog-posts/what-is-a-columnar-database)

## Read More

- [https://www.tinybird.co/blog-posts/when-to-use-columnar-database](https://www.tinybird.co/blog-posts/when-to-use-columnar-database)
