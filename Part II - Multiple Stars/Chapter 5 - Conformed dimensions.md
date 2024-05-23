# Chapter 5 - Conformed dimensions
This chapter focuses on insuring cross-process capability through conformed dimensions. With the right dimension design and content, it is possible to compare facts from different fact tables, both within a subject area and across the enterprise. Conformed dimensions can do more than enable drilling across. They can serve as the
focus for planning enterprise analytic capability. 

## The Synergy of Multiple Stars

- New stars afford insights into a new business process and allows to be studied in conjunction with existing ones.
- Every business has chains of linked processes, often beginning with product development or acquisition, extending through customer acquisition, and culminating in the collection of revenues.
- Within a subject area such as sales, for example, there may be a series of linked processes (product manufacturing, sales, marketing, customer support, and finance).
- At a logical level, when a series of stars share a set of common dimensions, the dimensions are referred to as conformed dimensions.

## Dimensions and Drilling Across
- Drill-across failure occurs when dimensions differ in their structure or content, extinguishing the possibility of cross-process synergy.
- Dimension tables need not be identical to support drilling across, since stars do share some common dimension attributes.
- When the attributes of one are a subset of another, drilling across may also be possible.
- Corresponding dimension tables should provide consistent results when substituted for one another. In terms of content, this requires that they contain the same set of rows, that corresponding rows share the same surrogate key values, and that slow change processing rules have been applied consistently. 

![Stars common atributes](https://github.com/STEFANOVIVAS/star-schema-notes/blob/main/stars_common_atributes.png)

## Conformed Dimensions

When dimension tables exhibit the compatibility necessary to support drilling across, they are conformed dimensions. Identical dimensions ensure conformance, but conformance can take several other forms as well. Fact tables and conformed dimensions can be planned and documented in a matrix format and serve as the blueprint for incremental implementation.

### Types of Dimensional Conformance

- Shared Dimension Tables
- Conformed Rollups (When the dimension attributes from one table are a subset of those from another, and the common attributes share the same structure and content)
- Degenerate Dimensions
- Overlapping Dimensions (Non-identical dimension tables conform through a set of overlapping attributes)

**

  ![Base dimensional table x Conformed rollup](https://github.com/STEFANOVIVAS/star-schema-notes/blob/main/images/conformed_rollup.png)











