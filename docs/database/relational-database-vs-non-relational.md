# Relational Database vs Non-Relational

## When to use a relational database?

If you’re creating a project,

where the data is predictable, in terms of:

- structure
- size
- frequency of access

relational databases are still the best choice.

Normalization can help reduce the size of the data on disk by limiting duplicate data and anomalies,
decreasing the risk of requiring vertical scaling in future.

Relational databases are also
the best choice if relationships between entities are important.

Non-relational databases can store documents within the documents,
which helps keep data that will be accessed together in the same place.

But if this isn’t right for your needs,
a relational database is still the answer.

For example,
if you have a large dataset with complex structure and relationships,
embedding might not create clear enough relationships.

The amount of time that RDMSs have been around also means there is wide support available,
from tools to integration with data from other systems.

## When to use a non-relational database?

there are many types of non-relational databases,
each having their own advantages and disadvantages.

However,
non-relational databases still maintain some consistent advantages.

If the data you are storing,

needs to be in:

- flexible shape
- flexible size
- or if it needs to be open to change in future

then a non-relational database is the answer.

Modern NoSQL databases have been designed for the cloud,
making them naturally good for horizontal scaling
where a lot of smaller servers can be spun up to handle increased load.

## Relational Database vs Non-Relational

|      Features      |         Non-Relational          |      Relational      |
| :----------------: | :-----------------------------: | :------------------: |
|    Availability    |              High               |         High         |
| Horizontal Scaling |              High               |         Low          |
|  Vertical Scaling  |              High               |         High         |
|    Data Storage    | Optimized for huge data volumes | Medium to large data |
|    Performance     |              High               |    Low To Medium     |
|    Reliability     |             Medium              |     High (Acid)      |
|     Complexity     |               Low               |    Medium (Joins)    |
|    Flexibility     |              High               | Low (Strict-Schema)  |
|    Suitability     |   Suitable For OLAP and OLTP    |  Suitable For OLTP   |

From <https://www.mongodb.com/compare/relational-vs-non-relational-databases>
