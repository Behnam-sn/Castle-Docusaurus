# SQL: A Nonprocedural Language

If you have worked with programming languages in the past,  
You are used to defining variables and data structures,  
Using conditional logic (i.e., if-then-else)  
And looping constructs (i.e., do while ... end),  
And breaking your code into small, reusable pieces (i.e., objects, functions, procedures).

<!-- Your code is handed to a compiler,
And the executable that results does exactly (well, not always exactly) what you programmed it to do. -->

Whether you work with Java, Python, Scala, or some other procedural language,  
You are in complete control of what the program does.

:::note
A procedural language defines both the desired results and the mechanism, or process, by which the results are generated.  
Nonprocedural languages also define the desired results,  
But the process by which the results are generated is left to an external agent.
:::

With SQL, however,  
You will need to give up some of the control you are used to,  
Because SQL statements define the necessary inputs and outputs,  
But the manner in which a statement is executed is left to a component of your database engine known as the optimizer.

The optimizer’s job is to look at your SQL statements,  
And taking into account how your tables are configured and what indexes are available,  
Decide the most efficient execution path (well, not always the most efficient).

Most database engines will allow you to influence the optimizer’s decisions by specifying optimizer hints,  
Such as suggesting that a particular index be used;

Most SQL users, however, will never get to this level of sophistication,  
And will leave such tweaking to their database administrator or performance expert.

Therefore, with SQL, you will not be able to write complete applications.

Unless you are writing a simple script to manipulate certain data,  
You will need to integrate SQL with your favorite programming language.

Some database vendors have done this for you,  
Such as Oracle’s PL/SQL language,  
MySQL’s stored procedure language,  
And Microsoft’s Transact-SQL language.

With these languages,  
The SQL data statements are part of the language’s grammar,  
Allowing you to seamlessly integrate database queries with procedural commands.

If you are using a non-database-specific language such as Java or Python, however,  
You will need to use a toolkit/API to execute SQL statements from your code.

Some of these toolkits are provided by your database vendor,  
Whereas others have been created by third-party vendors or by open source providers.

If you only need to execute SQL commands interactively,  
Every database vendor provides at least a simple command-line tool for submitting SQL commands to the database engine and inspecting the results.

Most vendors provide a graphical tool as well,  
That includes one window showing your SQL commands,  
And another window showing the results from your SQL commands.

Additionally,  
There are third-party tools such as SQuirrel,  
Which will connect via a JDBC connection to many different database servers.

Since the examples in this book are executed against a MySQL database,  
I use the mysql command-line tool that is included as part of the MySQL installation to run the examples and format the results.
