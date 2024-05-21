# Chapter 2 - Data Warehouse Architectures

## Inmon’s Corporate Information Factory

- Called Corporate information factory
- ETL process consolidates information from the various operational systems, integrates it, and loads it into a single repository called the enterprise data warehouse.
- The enterprise data warehouse is the hub of the corporate information factory.
- It's an Integrated repository of atomic data, as the data in this repository is captured at the lowest level of detail possible.
- It's not intended to be queried directly by analytic applications, business intelligence tools, or the like.
- Instead, its purpose is to feed additional data stores dedicated to a variety of analytic systems (Data marts), for which Inmon advocates the use of dimensional design.
- The enterprise data warehouse is usually stored in a relational database management system, and Inmon advocates the use of third normal form database design.


  [<img src="corporate information factory.png">](https://github.com/STEFANOVIVAS/star-schema-notes/)


## Kimball’s Dimensional Data Warehouse

- It's called dimensional data warehouse.
- Shares many characteristics in common with corporate information factory.
- Different from Inmon's perspective (ER modeling), the Integrated repository of atomic data is designed according to the principles of dimensional modeling (Star schema).
- The dimensional data warehouse may be accessed directly by analytic systems.

[<img src="dimensional design.png">](https://github.com/STEFANOVIVAS/star-schema-notes/)


## Stand-Alone Data Marts

- Allows rapid and inexpensive results in the short term, they can give rise to long-term costs and inefficiencies.
- The stand-alone data mart is an analytic data store that has not been designed in an enterprise context.
- The data mart may employ dimensional design,an entity-relationship model, or some other form of design.
- Analytic tools or applications query it directly, bringing information to end users. 
- Lacking a repository for granular data, a data mart may fail to answer a future question that requires more detail than originally anticipated.
- Due to his characteristics forms Islands of information.
- Developed to satisfy a narrow set of needs, they fail to support cross-functional analysis.

[<img src="data marts.png">](https://github.com/STEFANOVIVAS/star-schema-notes/)

## Comparison between approaches

[<img src="data warehouse architecture.png">](https://github.com/STEFANOVIVAS/star-schema-notes/)

[<img src="characteristics of each architecture.png">](https://github.com/STEFANOVIVAS/star-schema-notes/)

