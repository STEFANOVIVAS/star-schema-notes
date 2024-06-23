# Chapter 12 - Factless fact tables
Paradoxically, a fact table does not always require facts to measure a process (Factless fact table). There are two situations where even though no facts are explicitly recorded in a factless fact table, it does support measurement: Factless fact tables for events and Factless fact tables for conditions.

- Factless fact tables for events record the occurrence of activities. Examples include the number of documents processed or approved, the number of calls to a customer support center, or the number of impressions of an advertisement.

- Factless fact tables for conditions are used to capture significant information that is not part of a business activity. Conditions associate various dimensions at a point in time. When compared with activities, they provide valuable insight. Examples of conditions include eligibility of people for programs, the assignment of salesreps to customers, active marketing programs for a product, or special weather conditions in effect.

## The Factless Fact Table

- There are no dollar amounts to be aggregated, no quantities to be summed, no balances to be averaged. Businesses measure this kind of process simply by counting the activities. 
- Activities with no associated facts can be tracked in a factless fact table. Each row is a set of foreign keys that describes the dimensionality of the event. The presence of a row constitutes a measurement.
- When a factless fact table tracks events, it is possible to make it resemble a standard fact table by adding a special fact. This fact will always contain the value 1 (The fact table is no longer factless)
- Designs that start out factless often become the home for measurements of duration or cost. A factless fact table that tracks phone calls, for example, might track the duration of each call.

## Conditions, Coverage, or Eligibility
Factless fact tables can also be used in situations that do not clearly correspond to events or activities. Some common examples include:
- Tracking the salesperson assigned to each customer
- Logging the eligibility of individuals for programs or benefits
- Recording when severe weather alerts are in effect
- Capturing the marketing campaigns that are active at a given time

Factless fact tables that describe conditions, coverage, or eligibility almost always serve as a basis for comparison with other business processes. As fact tables, Conditions at a point in time also capture relationships between dimensions in a particular context. The environment at a point in time may link a salesperson with a customer, a product with a promotion, or an individual with an eligible benefit. These conditions can play an important part in understanding activities like orders, sales, or benefit participation. The assignment of a customer to a salesperson is an example of a “condition” that is in effect for a period of time. Conditions like this do not correspond to order transactions, nor to any other transaction fact tables associated with the sales process. Yet they are significant; the business may wish to compare conditions to sales activities. We might want to compare customer assignments with orders to produce a list of
customer assignments with no corresponding orders during the first quarter of 2009. 






