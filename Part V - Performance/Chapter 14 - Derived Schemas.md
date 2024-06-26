# Chapter 14 - Derived Schemas

- Performance is one of the foundational principles of data warehousing in general.
- By restructuring data at load time, rather than query time, answering analytic questions about business processes is faster and easier.
- Derived schemas store copies of existing dimensional data that has been restructured.
- These data structures can improve query performance and reduce report development complexity, at the cost of additional work loading and managing them.
- Besides some derived structures that have already been studied in this book, we have four more to know:  
    - Merged fact tables  
    - Pivoted fact tables
    - Sliced fact tables
    - Set operation fact tables
 
## Restructuring Dimensional Data
- Derived schemas provide a second layer to the dimensional architecture. They piggyback on existing dimensional structures, rather than drawing data from the original sources.
- Other examples of derived schemas: snapshots, accumulating snapshots, and core fact tables.
- By restructuring data, a derived schema makes answers accessible to users of less skill, and may also reduce report development costs.
- Benefits are achieved by moving work out of the query and reporting process and into the ETL process, as more tables must be designed, loaded, and maintained. 

### Uses for Derived Schemas
- Derived schemas can improve query performance and reduce report complexity.
- A derived schema can be used to produce a replica of the base schema that is limited in scope (Controls the size of data sets and allows for the application of role-based security)
- Very handy when deploying OLAP cubes for analytic purposes.
  
## The Merged Fact Table
