# Chapter 9 - Multi-Valued Dimensions and Bridges

Until now, each and every dimension attribute has participated in a simple one-to-many relationship with every fact. Real-world complexity sometimes makes it
impossible to model a process in this manner, for example, each order may have more than one salesperson. This situation occurs in the following contexts:  

- Multi-valued dimensions occur when a fact table row may need to refer to more than one row in a dimension table.  
- Multi-valued attributes occur when a dimension row needs to capture multiple values for a single attribute.  

## Multi-Valued Dimensions

- The simplest way to deal with a multi-valued dimension is to decompose the many-to-many relationship into two or more one-to-many relationships. This solution makes use of roles, as covered in Chapter 6. The fact table will have not one relationship to the dimension table but two or more. However, this solution complicates reporting and supports only a finite number of relationships (What if we have three salespeople per order?)
- Although imperfect, this solution may be acceptable. If the frequency of collaboration is rare and can be limited to a fixed number of participants, it may be the right choice.
- The multi-valued dimension problem can be solved by developing a group table that sits between the fact table and the dimension table. Instead of directly referring to the dimension table, each fact will refer to a single group.
- For example, the table sales_group has one row for each member of the group. Each row has only two columns: the group_key and the salesrep_key.
- Unlike the simplification option, this approach can accommodate groups of any size, so if a group of 15 works together, a group is created and 15 rows are added.
- Instead of simplifying a many-to-many relationship, a multi-valued dimension can be accommodated through the design of a special table called a bridge. This approach is much more flexible but brings with it the danger of double-counting.

![Bridge Table](https://github.com/STEFANOVIVAS/star-schema-notes/blob/main/images/bridge_table.png)

### Double-counting
- Sometimes this double-counting is actually a good thing. For example, it may be useful to have a report that shows order_dollars by salesperson. This kind of report provides insight into the impact that a particular member of the dimension table has on the facts.
- The only safe way to construct an impact report is to group by a column in the dimension that will have a unique value for each member of the group. Most often, this will be the natural key.
- Another way to avoid the danger of double-counting is to hide the bridge from inexperienced users. This is done by supplementing the bridged solution with a simplified solution recognizing only one dimension row. The bridge is hidden from everyone except carefully trained analysts.

## Multi-Valued Attributes

When a dimension attribute may take on more than one value for any given row in the table, we face a similar design challenge. How does one model an indefinite number of attribute values for a single row in the dimension? Customers have multiple phone numbers, bank accounts have multiple account holders, and so on.
Like the multi-valued dimension, this challenge can be resolved by simplifying the problem or by using a bridge table.

### Simplifying the Multi-Valued Attribute
- When you are faced with multi-valued attributes, the first option to consider is simplification of the problem through a technique that is sometimes referred to as “flattening.” Instead of designing a single column to capture the attribute, you can include two or more columns.
- This approach works best where a limited number of values is acceptable, where each version corresponds to an easily identifiable role, and where it will not be necessary to filter or group transactions in a fact table using values that may occur in any of the columns.  
This solution has several shortcomings:

    -  The solution is limited to a specific number of values. Later, we may encounter a customer that requires more than three industries.
    -  Filtering a query for a particular industry will require defining multiple conditions, since the industry in question may appear in any one of the columns.
    -  Grouping facts by industry will be particularly challenging, since a given industry may appear in any of the three columns.

### Bridging the Relationship
- A multi-valued attribute can be supported using an attribute bridge table, which works in much the same way as the dimension bridge in the previous section. This time, instead of placing the bridge between fact table and dimension table, the bridge will be placed between the dimension table and an outrigger.
- The multi-valued attributes are not stored in the dimension table. Instead, they are placed in a separate table with its own surrogate key. This table will act as an outrigger.
- A bridge table is set up with two columns: a group_key and a second column referring to the outrigger.
- When a dimension row refers to a specific combination of values in the outrigger, a group is set up for those values in the bridge table.
- The dimension table and the bridge can be joined using the group_key; the bridge table is joined to the outrigger in turn.
- Compared to a solution that simplifies multi-valued attributes, using a bridge table offers increased flexibility and simplifies reporting challenges.

  ### The Impact of Changes

