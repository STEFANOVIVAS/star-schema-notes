# Chapter 6 - More on dimensions tables

## Grouping Dimensions into Tables

- Unlike an entity-relationship (ER) model, a dimensional model does not expose every relationship between attributes as a join. Relationships that are contextual tend to pass through fact tables, while natural affinities are represented by co-locating attributes in the same dimension table.
- In a star schema, the relationship between a given pair of dimension attributes may be expressed explicitly or implicitly. 
- Relationships of the explicit variety are the most familiar. They take the form of joins that intersect in a fact table, which provides an important context for the relationship. For example, a fact table row may record the fact that on January 1, 2008 (a day), Hal Smith (a salesperson) took an order for 100 black ballpoint pens (a product) from ABC Stationery Emporium (a customer) as part of order number 299113. The fact table row records a relationship among these instances of day, salesperson, product, customer, and order. They are related to one another in the context of this particular order.  
- Less familiar are implicit relationships, which occur when two attributes are located in the same table. Implicit relationships imply a natural affinity between attributes, rather than a relationship that can take many contexts. These relationships tend to be more consistent, and they are browsable. These relationships tend to exist only in a single context, representing a natural affinity rather than one based on process activities. The relationships among attributes in a dimension table may change over time but tend to be less volatile than those of the explicit variety. When implicit relationships do change, their history can be preserved through a type 2 slow change response.  

## Breaking Up Large Dimensions
Sometimes, a dimension table becomes so wide that database administrators become concerned about its effect on the database. Such a concern may be purely technical but is completely valid. Very wide rows, for example, may impact the way that the database administrator allocates space or designates block size. When a table has scores of type 2 attributes, incremental updates to the dimension can become a tremendous processing bottleneck.How to deal with them?

### Splitting Dimension Tables Arbitrarily
One common solution to the overly long dimension row is a simple separation of attributes into two tables. These two tables use the same surrogate key values, and they share a one-to-one relationship with one another. The excessive row length is split across the two tables, bringing row size back into the comfort zone of the
database administrators.
While this approach addresses issues raised by database administrators, it replaces them with a series of new challenges, such as sub-optimal performance, lack of configuration in RDBMS to double-reference foreign keys, and no benefit from an ETL developer perspective.
### Alternatives to split dimensions

- Design two differente dimensions, each one with your own surrogate key, generating two explicit relationships via fact table.
- When the number or size of free-form text fields is large, they can be relocated to a separate table and replaced with a foreign key reference (Outrigger)
- In situations that involve subtype-specific attributes, dimension row size can be controlled by building a core dimension with only the shared attributes, and separate custom dimensions for each subtype. The core dimension is used when analyzing all subtypes, such as products, and the custom dimensions are used when studying only one particular subtype, such as books, subscriptions, or compact discs.
- Considering mini-dimensions

### Mini-Dimensions Alleviate ETL Bottlenecks and Excessive Growth

- A mini-dimension is created by removing a number of the more volatile attributes from the dimension in question and placing them in a new table with its own surrogate key. These attributes share no direct relationship to one another, and there is no natural key. A one-time-only process can populate this table with data by creating a row for each combination of values.  
- Unlike the split dimension, the mini-dimension does not share surrogate keys with the original dimension table. There is not a one-to-one relationship between the original dimension and the mini-dimension. Fact tables will carry separate foreign keys which refer to the original dimension table and to the mini-dimension.
- Mini-dimensions do have a potential drawback: they disrupt browsability. The dimension table the mini-dimension are only related via facts. It is possible to provide limited browsability between a dimension and mini-dimension by adding a foreign key to the dimension table that refers to the mini-dimension, however, this cross-beowsability is limited to the current information in the mini-dimension. 

## Avoiding the NULL
- Not part of the set theory on which the relational database is founded, the concept of the NULL was added by vendors as a way to distinguish the absence of data from blank or zero.
- For dimension attributes, the inelegant but practical solution is to store a specific value such as 0 or “N/A” when data is not available.
- It is also useful to avoid allowing the NULL as a foreign key value in a fact table.

### Problems Caused by NULL

- Because a NULL does not represent anything, it cannot be considered equal to anything else—not even another NULL. At the same time, a NULL cannot be considered not equal to anything else.
- If one report shows January sales for tax exempt customers and another shows January sales for customers who are not tax exempt, a reasonable assumption would be that the two figures together represent all of January sales. Unfortunately, this is not the case.
- Rather than store NULLs in a dimension, star schema designers choose specific values that will be used when a data value is not available. For text columns, the value “N/A” is a trusted standby. For numeric columns, the value 0 is usually chosen, and dates are often defaulted to an arbitrary date in the very far future (more on dates in a moment).

### NULL Foreign Keys in Fact Tables
- Sometimes, it is not possible to associate a fact with a row in a dimension table. This occurs when the dimension value is unknown or invalid, or the relationship is optional.
- An example of an optional relationship occurs in retail sales. You may have noticed that in some stores the cashier will note when a salesperson has helped you. This information may be used to evaluate salespeople or to compute their compensation.
- Avoid allowing NULL values in foreign key columns. They require alternative join syntax and create NULL instance values for dimension columns even when nulls are not stored. This increasing group of workarounds leans heavily on a cadre of experienced

### Avoiding NULL Foreign Key Values
In addition to the optional relationship, there may be transactions for which the dimension information has not yet been supplied, for which the operational system has recorded invalid information, or for which the dimension represents something that has not yet occurred.

- For the optional relationship case, create a special row in the dimension table with a surrogate key value of 0.
- For the invalid data case, create a special row in the dimension table with a surrogate key value of 0, and row_type as Invalid.
- For the late-arriving data case, create a special row in the dimension table with a surrogate key value of 1, and row_type as Unknown.
- For future events cases, when a fact table represents something that may expire, it is useful to record a pair of dates: the date it became effective and the date it expired. In this case, avoid NULLS using a '9999/12/31' pattern for facts that have not expired yet.





