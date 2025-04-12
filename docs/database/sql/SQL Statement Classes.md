# SQL Statement Classes

The SQL language is divided into several distinct parts:

SQL schema statements,  
Which are used to define the data structures stored in the database;

SQL data statements,  
Which are used to manipulate the data structures previously defined using SQL schema statements;

and SQL transaction statements,  
Which are used to begin, end, and roll back transactions.

For example,  
To create a new table in your database,  
You would use the SQL schema statement `create table`,

Whereas the process of populating your new table with data would require the SQL data statement `insert`.

To give you a taste of what these statements look like,  
Here’s an SQL schema statement that creates a table called `corporation`:

```sql
CREATE TABLE corporation (corp_id SMALLINT, name VARCHAR(30), CONSTRAINT pk_corporation PRIMARY KEY (corp_id));
```

This statement creates a table with two columns,  
`corp_id` and `name`,  
With the `corp_id` column identified as the primary key for the table.

Next, here’s an SQL data statement that inserts a row into the corporation table for Acme Paper Corporation:

```sql
INSERT INTO corporation (corp_id, name)
VALUES (27, 'Acme Paper Corporation');
```

This statement adds a row to the `corporation` table,  
With a value of `27` for the `corp_id` column,  
And a value of `Acme Paper Corporation` for the `name` column.

Finally, here’s a simple `select` statement to retrieve the data that was just created:

```sql
mysql< SELECT name
-> FROM corporation
-> WHERE corp_id = 27;

+------------------------+
| name
|
+------------------------+
| Acme Paper Corporation |
+------------------------+
```

## Data Dictionary

All database elements created via SQL schema statements,  
Are stored in a special set of tables called the **data dictionary**.

This “data about the database” is known collectively as **metadata**.

Just like tables that you create yourself,  
Data dictionary tables can be queried via a `select` statement,  
Thereby allowing you to discover the current data structures deployed in the database at runtime.

For example,  
If you are asked to write a report showing the new accounts created last month,  
You could either hardcode the names of the columns in the `account` table,  
That were known to you when you wrote the report,  
Or query the data dictionary to determine the current set of columns and dynamically generate the report each time it is executed.
