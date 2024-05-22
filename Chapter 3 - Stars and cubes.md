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
    • They are used to define
- Construct combinations of break data elements from operational system and include them in the dimensions to increase analytic value (First name+ middle name+ last name=Full Name).
- It is not always clear whether a numeric data element is a fact or a dimension, so if the element values are used to filter queries, order data,
control aggregation, or drive master–detail relationships, it is most likely a dimension.
- In some cases, it can be useful to create a table that contains dimensions attributes that do not have any real relationship to another table (Junk dimensions).
- Applying principles of normalization to the dimensional design results in a variation on the star schema called a snowflake schema (outrigger). Analytical systems do not benefit from these techniques.
- Why not simply perform these computations “on the fly” at query time? The precomputation and storage of these redundant data elements have three advantages in an analytic environment: performance, usability, and consistency.










