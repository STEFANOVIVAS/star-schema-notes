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






