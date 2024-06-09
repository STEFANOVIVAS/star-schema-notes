# Chapter 7 - Hierarchies and Snowflakes

It is possible to describe a dimension table as a series of parent-child relationships among groups of attributes. Days make up months, months fall into quarters, and quarters fall into years, for example. When an attribute hierarchy is instantiated as a series of physical tables, rather than as a single dimension table, the result is a variation of the star schema known as a snowflake. On rare occasions, a limited form of snowflaking is employed to help resolve unmanageable row length or to ensure consistent representation of repeating attributes (Outrigger).

## Drilling

- The word drill connotes digging deeper into something (Fact).
- A generic concept of drilling is expressed simply as the addition of dimensional detail.
- This basic concept of drilling is sometimes referred to as drilling down, in order to distinguish it from the converse activity drilling up, wherein dimensional detail is removed from a report.

### Attribute Hierarchies and Drilling

- Attribute hierarchies offer a natural way to organize facts at successively deeper levels of detail.
- The bottom of such a hierarchy represents the lowest level of detail described by the dimension table, while the top represents the highest level of summarization.
- The attributes in a product dimension table, for example, may form a simple hierarchy (Products fall within brands, and brands fall within categories)
- There are other ways to drill, instead of attribute hierarchy, and the possibilities include following an alternative hierarchy within the dimension, following hierarchies in more than one dimension (Categories -> Months), drilling without any form of hierarchy (Product color), and drilling through instance hierarchies (Employees->Employees). 

### Documenting Attribute Hierarchies

- The attribute hierarchy is the primary focus of many business intelligence tools. By defining hierarchies within dimensions, these tools are able to anticipate what users might do and prepare for it.
- It includes important information about the product attribute hierarchies, such as names for each level of the attribute hierarchy, attributes present at each level, and the one-to-many relationships between instances of each level.
- In addition to helping you configure the drilling feature of business intelligence software, information on attribute hierarchies helps with the design of
conformed dimensions, cubes, and aggregate tables.

![Attribute Hierarchy](https://github.com/STEFANOVIVAS/star-schema-notes/blob/main/images/attribute_hierarchy2.png)

## Snowflakes

You may find a snowflake configuration appealing because it exposes a natural taxonomy in the data. For those trained in ER modeling, the snowflake reflects some best practices learned in the service of operational systems; however, it is of little utility for an analytic database, aside from saving some space.

![Snowflake](https://github.com/STEFANOVIVAS/star-schema-notes/blob/main/images/snowflake.png)

### Why avoid the snowflake?
- Snowflaking a dimension is similar to a process called normalization, which guides the design of operational systems.
- This technique was developed to ensure referential integrity of data in operational systems, which support a wide variety of simultaneous transactions that are highly granular.
- An analytic database does not share this usage pattern, and referential integrity can be enforced by the ETL process.
- Star schema improves business user understandability (Measurements are in the middle, surrounded by options for filtering them or breaking them out).
- Snowflake design adds complexity (PK/FK between dimensions must be managed, SCD)
- Performance benefits, as snowflake design increases the number of joins.

### When embrace the snowflake?

- Some products in your architecture may function best with a snowflake design (Some tools require the use of a snowflake to support aggregates, and others may require it in order to automate the drill-across process).
- Some specific modeling challenges cannot be met without decomposing a dimension into more than one table (Multi-Valued Attributes, Recursive Instance Hierarchies and Repeating Groups).

## Outriggers

- On rare occasions, a repeating set of attributes may lead to concerns over inconsistent representation, particularly if the attributes repeat in multiple tables. 
- If concerns about row length or ETL consistency cannot be addressed by other means, the solution may be to add an outrigger table.
- The repeating attributes are placed in a separate table, the outrigger, which is given its own surrogate key.
- In the original dimension table, the relocated attributes are replaced with one or more foreign key references to the outrigger.
- Outriggers may be used to streamline ETL or reduce row length, but they introduce complexity and may have an impact on query performance.
- You may be able to define multiple dimensions or construct a mini-dimension to avoid the problem.
- With an outrigger in place, it may be necessary to apply a type 2 change to a dimension row, even if none of its attributes have changed. The change is precipitated by a type 2 change in the outrigger.

