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

