# Chapter 15 - Aggregates
- Aggregates are the most powerful and effective tool at your disposal in the quest for improve performance, by summarizing granular data in advance.
in advance. The
- Derived schemas improve performance by restructuring data in a manner suited to a particular class of query, differently, aggregate schemas achieve a performance benefit by summarizing data.
- The benefits of aggregates are not free, so putting them to work requires selecting the correct aggregate to use for each query. It also requires that aggregates be populated with data and kept in sync with the base schema. The latter requirement can be particularly tricky when type 1 changes occur. 
- An aggregate table improves response time by reducing the number of rows that must be accessed by the DBMS when responding to a query.
- Like the derived schemas from Chapter 14, the aggregate star does not provide this performance benefit for free. The aggregate tables must be loaded and maintained, resulting in additional work for ETL developers and database administrators.
- The development of ETL routines for aggregate fact tables is guided by the same principle. Following these guidelines, the overall dependency of table load routines during the ETL process might look like this:
  
    1. Load base dimensions
    2. Load conformed rollups
    3. Load base fact table
    4. Load aggregate fact table

## Type 1 Changes
- When base data and aggregates are loaded sequentially, the occurrence of a type 1 change can force the need to reload the aggregate completely, rather than update it incrementally.
