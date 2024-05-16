# Chapter 1 - Analytic Databases and Dimensional Design
The dimensional model of a business process is made up of two components: measurements and their context. Known as facts and dimensions, these components
are organized into a database design that facilitates a wide variety of analytic usage.

## Dimensional design

The core of every dimensional model is a set of business metrics that captures how a process is evaluated, and a description of the context of every measurement.
A dimensional design organizes facts and dimensions for storage in a database. It is common for a set of dimensions to share relationships to one another, independent of facts. These are grouped together in a single table to reflect their natural clustering. Similarly, facts that are available at the same level of detail are grouped together. In a relational database management system (RDBMS), the design is referred to as a star schema.

- Operational process x Analytical process

  [<img src="analytical x operational.png">](https://github.com/STEFANOVIVAS/star-schema-notes/)
  
### Facts and Dimensions

- In a spoken or written statement, the words “by” and "for" are almost always followed by a dimension (“What are order dollars by product category for January?”)
- Facts tend to be numeric in value, but not always, and people want to see them at various levels of detail.
- Dimensions serve as a "filter" or "query predicates".
- In a report, dimensions also serve to specify groupings or “break levels,” or to identify levels of subtotals.
- Elements that are aggregated, summarized, or subtotaled are facts.

## The Star Schema

A dimensional design for a relational database is called a star schema. Related dimensions are grouped as columns in dimension tables, and the facts are stored as columns in a fact table. The star schema gets its name from its appearance: when drawn with the fact table in the center, it looks like a star or asterisk.

[<img src="star schema.png">](https://github.com/STEFANOVIVAS/star-schema-notes/)


