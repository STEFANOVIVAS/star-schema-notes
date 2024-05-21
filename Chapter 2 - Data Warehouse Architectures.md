# Chapter 2 - Data Warehouse Architectures

## Inmon’s Corporate Information Factory

- Called Corporate information factory
- ETL process consolidates information from the various operational systems, integrates it, and loads it into a single repository called the enterprise data warehouse.
- The enterprise data warehouse is the hub of the corporate information factory.
- It's an Integrated repository of atomic data, as the data in this repository is captured at the lowest level of detail possible.
- It's not intended to be queried directly by analytic applications, business intelligence tools, or the like.
- Instead, its purpose is to feed additional data stores dedicated to a variety of analytic systems (Data marts), for which Inmon advocates the use of dimensional design.
- The enterprise data warehouse is usually stored in a relational database management system, and Inmon advocates the use of third normal form database design.
  
