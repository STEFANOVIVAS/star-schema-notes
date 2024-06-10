# Chapter 9 - Multi-Valued Dimensions and Bridges

Until now, each and every dimension attribute has participated in a simple one-to-many relationship with every fact. Real-world complexity sometimes makes it
impossible to model a process in this manner, for example, each order may have more than one salesperson. This situation occurs in the following contexts:  

- Multi-valued dimensions occur when a fact table row may need to refer to more than one row in a dimension table.  
- Multi-valued attributes occur when a dimension row needs to capture multiple values for a single attribute.  

## Multi-Valued Dimensions

- The simplest way to deal with a multi-valued dimension is to decompose the many-to-many relationship into two or more one-to-many relationships. This solution makes use of roles, as covered in Chapter 6. The fact table will have not one relationship to the dimension table but two or more. However, this solution complicates reporting and supports only a finite number of relationships (What if we have three salespeople per order?)
- Although imperfect, this solution may be acceptable. If the frequency of collaboration is rare and can be limited to a fixed number of participants, it may be the right choice.
- Instead of simplifying a many-to-many relationship, a multi-valued dimension can be accommodated through the design of a special table called a bridge. This approach is much more flexible but brings with it the danger of double-counting.
- Sometimes this double-counting is actually a good thing. For example, it may be useful to have a report that shows order_dollars by salesperson. This kind of report provides insight into the impact that a particular member of the dimension table has on the facts.
- 
- The multi-valued dimension problem can be solved by developing a group table that sits between the fact table and the dimension table. Instead of directly referring to the dimension table, each fact will refer to a single group.
- For example, the table sales_group has one row for each member of the group. Each row has only two columns: the group_key and the salesrep_key.
- Unlike the simplification option, this approach can accommodate groups of any size, so if a group of 15 works together, a group is created and 15 rows are added. 

![Bridge Table](https://github.com/STEFANOVIVAS/star-schema-notes/blob/main/images/bridge_table.png)
