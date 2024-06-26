# Chapter 3 - Stars and cubes

## Dimension Table Features

### Surrogate Keys and Natural Keys

- Surrogate keys are created especially for the data warehouse or data mart and have a unique value (Generally integers).
- The use of surrogate keys as unique identifiers allows the data warehouse to respond to changes in source data in whatever manner best fits analytic requirements.
- Natural keys are identifiers carried over from source systems and may have meaning to users of the data warehouse.
- When more than one system can be the source for a dimension, the natural key may be composed of the identifier from the source system and an additional identifier that indicates which source it came from (Ex.: mergers and acquisitions leading to different source systems).

### Rich Set of Dimensions
- Dimensions unlock the value of facts so, the larger the set of dimension attributes, the more ways that facts can be analyzed.
- Dimensions and their values add meaning in many ways:
  
        • They are used to filter queries or reports.  
        • They are used to control the scope of aggregation for facts.  
        • They are used to order or sort information.  
        • They accompany facts to provide context on reports.  
        • They are used to define master–detail organization, grouping, subtotaling, and summarization.  

- Construct combinations of break data elements from operational system and include them in the dimensions to increase analytic value (First name+ middle name+ last name=Full Name).
- It is not always clear whether a numeric data element is a fact or a dimension, so if the element values are used to filter queries, order data,
control aggregation, or drive master–detail relationships, it is most likely a dimension.
- In some cases, it can be useful to create a table that contains dimensions attributes that do not have any real relationship to another table (Junk dimensions).
- Applying principles of normalization to the dimensional design results in a variation on the star schema called a snowflake schema (outrigger). Analytical systems do not benefit from these techniques.
- Why not simply perform these computations “on the fly” at query time? The precomputation and storage of these redundant data elements have three advantages in an analytic environment: performance, usability, and consistency.


## Fact Table Features

Every fact table represents a business process by capturing measurements that describe it.The level of detail at which the fact table records information is referred to as its grain. Fact tables do not contain rows for every combination of dimension values. Instead, they exhibit a characteristic called sparsity. 

- Facts are stored at a specific level of detail but can be rolled up to various levels of dimensionality (Additivity).
- Many key business metrics are expressed as rates or percentages and this type of measurement is never additive.
- However, ratios can be broken down into underlying components (For example, margin rate is the ratio of the margin dollars to order dollars)
- The nonadditive fact is not stored in the fact table and may be done in a query or by additional processing logic in the reporting tool. 
- Set the fact table grain at the lowest level of detail possible to ensure maximum analytic flexibility (It can be relaxed if there is a separate repository for granular data, but may limit future utility).
- Rows are recorded in fact tables to represent the occurrence of business activities. This means that fact tables do not contain a row for every possible combination of dimension values (Sparsity).
- Sometimes, it is not possible to sort all the dimensions associated with a business into a neat set of tables (Degenerated dimension).
- In most cases, candidates for degenerate dimensions are better placed in junk dimensions, with the exception of transaction identifiers.

## Slowly Changing Dimensions
In every dimensional design, it is crucial to identify how changes in source data will be represented in dimension tables.

### Type 1 Change
When the source of a dimension value changes, and it is not necessary to preserve its history in the star schema, a type 1 response is employed. The dimension is simply overwritten with the new value. This technique is commonly employed in situations where a source data element is being changed to correct an error.

A type 1 change has an important effect on facts, one that is often overlooked. When a record is updated in a dimension table, the context for existing facts is restated.

### Type 2 Change

The second method for responding to a change in source data is to insert a new record into the dimension table. Any previously existing records are unchanged. This type 2 response preserves context for facts that were associated with the old value, while allowing new facts to be associated with the new value.

This type 2 response has the effect of creating “versions” of one registry in the dimension table. Where there was previously one row representing it, there are now two. This “versioning” is made possible because the dimension table does not rely on the natural key, customer_id, as its unique identifier.

Type 2 changes preserve the dimensional detail surrounding facts. They may confuse users, however, by appearing to duplicate information in dimension tables. Avoid this confusion by issuing browse queries that select distinct values, and by offering a flag to indicate whether each row represents the current version for its natural key value.

Although the type 2 change preserves the historic context of facts, it does not preserve history in the dimension. It is easy to see that a given natural key has taken on multiple representations in the dimension, but we do not know when each of these representations was correct. However, this problem is easily rectified by adding a date stamp to each version of a dimension registry. This technique allows the dimension to preserve both the history of facts and the history of dimensions. 

## Cubes

Dimensional models are not always implemented in relational databases. A multidimensional database, or MDB, stores dimensional information in a format called a cube. The basic concept behind a cube is to precompute the various combinations of dimension values and fact values so they can be studied interactively.

### Multidimensional Storage vs. Relational Storage

- A cube allows users to change their perspective on the data interactively, adding or removing attributes to or from their view and receiving instantaneous feedback (OLAP).
- In contrast, a star schema is interacted with through a query-and-response paradigm so, each change in the information detail on display requires the issuance of a new query.
- MDBs were providing running totals, rankings and other statistical operations long before these capabilities were added to SQL.
- As the number of dimensions and their values increase, the number of possible combinations that must be precomputed explodes, limiting the ability to scale.

### Cubes and the Data Warehouse

- Used as a primary data store, the cube replaces a star schema to store dimensional data; as a derived data store, it supplements a star.
- Typically, the cube will replace relational storage as the primary data store in specific subject areas where the data sets are smaller.
- Stars and cubes work well together.
- If you build a star, you can take advantage of the scalability of the relational database to store very granular and detailed information. From this detail, you can build cubes to support an interactive query experience.



