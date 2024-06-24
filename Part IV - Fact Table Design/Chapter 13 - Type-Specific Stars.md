# Chapter 13 - Type-Specific Stars
Sometimes, the attributes you would like to record in the dimension table vary by type. A department store, for example, describes clothing items with a very different set of attributes from electronic items, yet all of them are products. In these situations, the dimensional modeler is faced with a dilemma. On one hand, there is a desire to study a business process across all types. On the other hand, there is a desire to study each particular type, using the type-specific attributes.
There are three ways to accommodate heterogeneous attributes, both within dimensions and within fact tables:

- A single star solution calls for one star that contains all possible attributes.
- The core and custom approach provides multiple stars. A core star contains all common attributes; one custom star for each type contains any type-specific
attributes. 
- The use of generic attributes creates multipurpose columns, the contents of which are determined by type. This technique is only viable when all interaction with the star will take place through a customized application.

## Type-Specific Attributes

### The Single-Star Approach
- The simplest way to deal with heterogeneous attributes in a dimensional model is to build a single star containing all possible attributes.
- For a seller of books and magazines, a single product dimension would contain all possible product attributes, including those specific to books or magazines.
- For any particular row in this table, many of these attributes will be blank (or will contain a NULL alternative such as N/A, as described in Chapter 6).
- Similarly, if different facts are collected for book orders and magazine orders, all potential facts are included in the fact table.

### Drawbacks to the Single-Star Approach
- Sometimes a star that consolidates all possible attributes is not practical and the obstacles may be technical or semantic.
- Technical: extreme variability in a dimension may result in more attributes than can be managed in a single row.
- Semantic: A star that consolidates all possible attributes may give rise to nonsensical reports and this is likely to occur when there are type-specific dimensions and facts.

## Core and Custom Stars

### Core and Custom Dimension Tables
- When the attributes of a dimension vary by type, and it is impractical or undesirable to build a single table with all possible attributes, the alternative is to build multiple versions of the dimension table.
- One version will contain only the attributes shared by all subtypes and contain a row for each instance, regardless of type (Core dimension).
- The remaining versions each correspond to a single type. They contain the core attributes, plus any type-specific attributes (Custom dimension tables).
- The core product dimension will be called on when the analytic questions look across all product types.
- The presence of the core attributes in each of the custom dimensions allows access to those attributes when studying a particular type. 
![Core and custom](https://github.com/STEFANOVIVAS/star-schema-notes/blob/main/images/core_and_custom.png)

### Core and Custom Fact Tables
If there are custom facts that correspond to specific types, then custom fact tables for each type will be necessary. Each custom fact table will contain any core facts, along with type-specific facts. It will contain rows only for the specific type represented.
