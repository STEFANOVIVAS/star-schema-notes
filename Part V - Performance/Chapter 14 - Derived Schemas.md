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
