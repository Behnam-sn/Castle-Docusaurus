# SQL Data Types

## Character Data

Character data can be stored as either fixed-length or variable-
length strings; the difference is that fixed-length strings are
right-padded with spaces and always consume the same
number of bytes, and variable-length strings are not right-
padded with spaces and don’t always consume the same
number of bytes. When defining a character column, you must
specify the maximum size of any string to be stored in the
column. For example, if you want to store strings up to 20
characters in length, you could use either of the following
definitions:

```sql
char(20)
/* fixed-length */
varchar(20) /* variable-length */
```

The maximum length for char columns is currently 255 bytes,
whereas varchar columns can be up to 65,535 bytes. If you
need to store longer strings (such as emails, XML documents, etc.), then you will want to use one of the text types
(mediumtext and longtext), which I cover later in this
section. In general, you should use the char type when all
strings to be stored in the column are of the same length, such
as state abbreviations, and the varchar type when strings to
be stored in the column are of varying lengths. Both char and
varchar are used in a similar fashion in all the major
database servers.

### CHARACTER SETS

For languages that use the Latin alphabet, such as English,
there is a sufficiently small number of characters such that only
a single byte is needed to store each character. Other
languages, such as Japanese and Korean, contain large
numbers of characters, thus requiring multiple bytes of storage
for each character. Such character sets are therefore called
multibyte character sets.

MySQL can store data using various character sets, both
single- and multibyte. To view the supported character sets in

your server, you can use the show command, as shown in the
following example:

If the value in the fourth column, maxlen, is greater than 1,
then the character set is a multibyte character set.

In prior versions of the MySQL server, the latin1 character
set was automatically chosen as the default character set, but
version 8 defaults to utf8mb4. However, you may choose to
use a different character set for each character column in your
database, and you can even store different character sets
within the same table. To choose a character set other than the
default when defining a column, simply name one of the
supported character sets after the type definition, as in:
varchar(20) character set latin1

With MySQL, you may also set the default character set for
your entire database:

create database european_sales character set
latin1;

While this is as much information regarding character sets as is
appropriate for an introductory book, there is a great deal more
to the topic of internationalization than what is shown here. If
you plan to deal with multiple or unfamiliar character sets, you
may want to pick up a book such as Jukka Korpela’s Unicode
Explained: Internationalize Documents, Programs, and Web
Sites (O’Reilly).
