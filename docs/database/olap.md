# OLAP

## What is OLAP?

OLAP stands for **Online Analytical Processing**.

It is a broad term that can be looked at from two perspectives:  
Technical and business.

At the highest level,  
You can just read these words backward:

- **Processing** some source data is processed,
- **Analytical** to produce some analytical reports and insights,
- **Online** in real-time.

## OLAP from the business perspective

In recent years business people started to realize the value of data.  
Companies who make their decisions blindly,  
More often than not fail to keep up with the competition.

The data-driven approach of successful companies,  
Forces them to collect all data that might be even remotely useful for making business decisions,  
And imposes on them a need for mechanisms which allow them to analyze this data in a timely manner.

Here's where OLAP database management systems (DBMS) come in.

In a business sense,  
OLAP allows companies to continuously plan, analyze, and report operational activities,  
Thus maximizing efficiency, reducing expenses, and ultimately conquering the market share.

It could be done either in an in-house system,  
Or outsourced to SaaS providers like web/mobile analytics services, CRM services, etc.

OLAP is the technology behind many BI applications (Business Intelligence).

ClickHouse is an OLAP database management system,  
That is pretty often used as a backend for those SaaS solutions for analyzing domain-specific data.

However, some businesses are still reluctant to share their data with third-party providers,  
And so an in-house data warehouse scenario is also viable.

## OLAP from the technical perspective

All database management systems could be classified into two groups:

- OLAP (Online Analytical Processing)
- OLTP (Online Transactional Processing)

The former focuses on building reports,  
Each based on large volumes of historical data,  
But by doing it less frequently.

The latter usually handles a continuous stream of transactions,  
Constantly modifying the current state of data.

In practice OLAP and OLTP are not viewed as binary categories,  
But more like a spectrum.

Most real systems usually focus on one of them,  
But provide some solutions or workarounds if the opposite kind of workload is also desired.

This situation often forces businesses to operate multiple storage systems that are integrated.

This might not be such a big deal,  
But having more systems increases maintenance costs,  
And as such the trend in recent years is towards HTAP (Hybrid Transactional/Analytical Processing),  
When both kinds of workload are handled equally well by a single database management system.

Even if a DBMS started out as a pure OLAP or pure OLTP,  
It is forced to move in the HTAP direction to keep up with the competition.

ClickHouse is no exception.

Initially it has been designed as a fast-as-possible OLAP system,  
And it still does not have full-fledged transaction support,  
But some features like consistent read/writes and mutations for updating/deleting data have been added.

The fundamental trade-off between OLAP and OLTP systems remains:

- To build analytical reports efficiently,  
  It's crucial to be able to read columns separately,  
  Thus most OLAP databases are columnar,

- While storing columns separately increases costs of operations on rows,  
  Like append or in-place modification,  
  Proportionally to the number of columns,  
  (Which can be huge if the systems try to collect all details of an event just in case).

  Thus, most OLTP systems store data arranged by rows.

## References

- [clickhouse.com/docs/concepts/olap](https://clickhouse.com/docs/concepts/olap)
