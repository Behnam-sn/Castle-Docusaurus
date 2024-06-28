# Column-Oriented Databases

While an RDBMS stores data in rows and reads it row by row,
column-oriented databases are organized as a set of columns.

When you want to run analytics on a small number of columns in the network,
you can read those columns directly without consuming memory with unwanted data.

Columns are of the same type and benefit from more efficient compression, making reads even faster.
A column-oriented database can aggregate the value of a given column (adding up sales for the year, for example).

Use cases of a column-oriented database include analytics.

Note: While column-oriented databases are great for analytics,
the way they write data makes it difficult for them to be consistent as writes of all the columns in the column-oriented database require multiple write events on disk.
Relational databases don't suffer from this problem as row data is written contiguously to disk.

From <https://www.mongodb.com/databases/types>
