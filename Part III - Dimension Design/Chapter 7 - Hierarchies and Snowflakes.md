# Hierarchies and Snowflakes

It is possible to describe a dimension table as a series of parent-child relationships among groups of attributes. Days make up months, months fall into quarters, and quarters fall into years, for example. When an attribute hierarchy is instantiated as a series of physical tables, rather than as a single dimension table, the result is a variation of the star schema known as a snowflake. On rare occasions, a limited form of snowflaking is employed to help resolve unmanageable row length or to ensure consistent representation of repeating attributes (Outrigger).

## Drilling

- The word drill connotes digging deeper into something (Fact).
- A generic concept of drilling is expressed simply as the addition of dimensional detail.
- This basic concept of drilling is sometimes referred to as drilling down, in order to distinguish it from the converse activity drilling up, wherein dimensional detail is removed from a report.

### Attribute Hierarchies and Drilling

- Attribute hierarchies offer a natural way to organize facts at successively deeper levels of detail.
- The bottom of such a hierarchy represents the lowest level of detail described by the dimension table, while the top represents the highest level of summarization.
- The attributes in a product dimension table, for example, may form a simple hierarchy (Products fall within brands, and brands fall within categories)
- There are other ways to drill, instead of attribute hierarchy, and the possibilities include following an alternative hierarchy within the dimension, following hierarchies in more than one dimension, drilling without any form of hierarchy, and drilling through instance hierarchies. 

 ![Attribute hierarchy](https://github.com/STEFANOVIVAS/star-schema-notes/blob/main/images/attribute_hierarchy.png)
