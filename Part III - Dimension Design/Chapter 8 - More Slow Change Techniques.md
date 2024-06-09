# Chapter 8 - More Slow Change Techniques
A crucial part of star schema design is determining how changes to source data will be reflected in dimension tables. The change response pattern for each dimension attribute in the star schema must be carefully matched to business requirements. Most requirements can be satisfied by employing types 1 and 2 of slowing change dimensions. When these options are not satisfied, we have a set of options to use, like time-stamped dimensions, type 3 changes, and hybrid techniques.

## Time-Stamped Dimensions

- The type 2 response has one glaring shortcoming: it cannot tell you what the dimension looked like at any point in time. This is a particular concern if you have a dimensional data warehouse architecture or stand-alone data mart, since in these architectures the dimensional model doubles as the integrated repository of granular data.  
- The time-stamped dimension permits three forms of point-in-time analysis within the dimension table itself(1-Easily order a chronological history of changes; 2- Quickly select dimension rows that were in effect for a particular date; 3-Easily identify the dimension rows currently in effect).
- For example, users might want to know how many policy holders were married versus how many were single on a particular date, or what the total number of covered parties was at the close of a fiscal period.
- In a time-stamped dimension the table is outfitted with additional columns to capture the effective and expiration dates for the row.
- When a particular dimension attribute has not expired, the expiration_date is set to 12/31/9999.
- If it is necessary to track changes at a finer grain, this can be achieved by adding columns to capture the time of day at which the record became effective and expired: effective_time and expiration_time.
  
## Type 3 Changes

In most dimensional schemas, the bulk of changes to source data generate type 1 and type 2 changes. Occasionally, neither technique satisfies. A third type of change response is called into play when there is a need to analyze all facts, those recorded before and after the change, with either the old value or the new value. The preferred approach is to include two attributes for the changed data element, one to carry the current value and one to carry the prior value. Both are updated when a change occurs. 
For example, when senior management studies orders, they usually do not dive right into customer detail. Instead, they use some standard regional groupings, let's say, east and west. As the company grew, these groupings became insufficient. What began as the East region was broken down into two regions: Northeast and Southeast. When changes like this occur, management begins using the new designations immediately. Management also needs to hang onto the old designations, at least for a little while, in order to compare this year’s performance to what was reported for the previous year.

- When requirements call for using the old or new values of a changed attribute to study all facts, a pair of attributes is modeled, one attribute for the current value and one for the previous value.
- When a change occurs, both columns are updated; no rows are added.
- A type 3 change does not preserve the historic context of facts. Each time a type 3 change occurs, the history is restated.

## Hybrid Slow Changes

A hybrid design allows for type 1 and type 2 treatment of the same source attribute by providing two separate dimension columns. One is designated as a type 1 attribute and can be used to group all facts under the latest value. The other is designated as a type 2 attribute and can be used to group facts with the historic values.
