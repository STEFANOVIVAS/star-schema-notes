# Chapter 4 - A Fact Table for Each Process

It is rare to find a subject area that can be fully described by a single fact table. This chapter presents techniques you can use to determine when you are dealing with multiple processes, and explains the implications of not describing them in separate fact tables. While analysis of individual processes is useful, some of the most powerful analytics cross process boundaries. In a dimensional environment, this will require combining information from more than one fact table (Drill across).


## Fact Tables and Business Processes

While the entity-relationship model is used to describe information, the process model is used to describe business activity. Process models involve functional decomposition. That is to say: one process can be broken down into several subprocesses. For example, the sales process may be broken down into subprocesses for order entry, shipment, invoicing, and returns management. 

How can we see that events describe two different processes or not? Or best saying, how can we discover if these events can be placed in the same fact table?
1. Do these facts occur simultaneously?
2. Are these facts available at the same level of detail (or grain)?
If the answer to either of these questions is “no,” the facts represent different processes.

For example, in an e-commerce store, orders and shipments do not occurs simultaneously, neither have the same grain, cause shipment quantities are associated with
specific shippers, while order quantities are not.

When a single fact table tracks two or more processes, let's say orders and shipments, problems occur when someone is interested in studying only one process. In this case, the process being examined is shipments, and the problem is evident in the final row of the report. Although a certain product has not shipped during the reporting period, it appears on the report, with a quantity_shipped of 0, cause we have an order for it.


