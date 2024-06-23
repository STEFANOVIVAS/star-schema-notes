# Chapter 11 - Transactions, Snapshots, and Accumulating Snapshots

Each star schema in the preceding chapters features a fact table that measures activities. This kind of fact table is known as a transaction fact table. As you have seen, it supports a wide
variety of analytic possibilities with great efficiency and can be used to capture detailed granular information about a process. Some facts, however, cannot be easily studied using
this kind of design, and others cannot be accommodated at all. This chapter introduces two additional kinds of fact table: the snapshot and the accumulating snapshot.

## Snapshot Fact Tables
Sometimes, measuring the effect of a series of transactions is as useful as measuring the transactions themselves. These effects are called status measurements. Common examples include account balances and inventory levels. You can figure out how many ballpoint pens are in the stockroom, for example, by adding up all the deliveries of ballpoint pens to the stockroom and deducting all the pens that were removed from the stockroom. This will give you the number of pens remaining, but it is a highly inefficient process.

Designers faced with the challenge of tracking both transactions and their effects may be tempted to store the status measurement as an additional fact in the transaction fact table. There are two reasons why it does not make sense to record a status, level, or balance with each transaction. Perhaps the most obvious reason is that the transaction fact table is sparse. If there is no activity on a particular day, there is no row in which to record this important fact. Less obvious, but equally problematic, is the fact that there will be some days where there are more than one transaction. If a balance is stored with each transaction, then it is likely it will be double-counted by queries.

- Whereas a transaction fact table’s grain may be expressed in various ways, the grain of a snapshot fact table is usually declared in dimensional terms. While a transaction fact table is sparse, snapshots are dense. Last, while the facts in a transaction fact table are fully additive, a snapshot model will contain at least one fact that exhibits a property known as semi-additivity.
- In a transaction fact table, if there is no transaction on a particular day, no row is recorded. In a snapshot, however, rows are recorded regardless of activity. 
- Note that this density does not necessarily imply that the snapshot will have more rows than the transaction fact table. Relative sizes will be determined by the snapshot’s grain and transaction volume. If accounts average more than one transaction per day, the snapshot may actually be smaller.
- Unlike the additive facts in a transaction fact table, the semi-additive fact cannot be summed meaningfully across the time dimension. This does not mean it cannot be aggregated across time; averages, minimums, and maximums may all be of use.

### Snapshot Considerations
 - It may be useful to provide both transaction and snapshot representations of the same process; like two sides of the same coin, these models provide different and valuable perspectives of the same activities.
 - When a design will include both a transaction fact table and a periodic snapshot, the snapshot can and should be designed to use the transaction fact table as its data source.

## Accumulating Snapshot Fact Tables
Many business processes can be described as a series of stages, steps, or statuses through which something must pass. In made-to-order manufacturing, an individual item is ordered, manufactured, quality assured, packaged, and shipped. The efficiency of a process is often measured as the amount of time it takes to complete one or more steps. The manufacturer may like to know the average number of days between order and shipment, or between manufacturing and packaging. Tracking time elapsed at one or more steps of a business process can be supported with a third kind of fact table, called an accumulating snapshot. 

- The grain of an accumulating snapshot will be defined as one row per instance of the entity in question. For mortgage processing, for example, the entity is an application.
- This statement of grain contrasts with the grain of a transaction fact table, which typically records one row per event, or the grain of a periodic snapshot, which records a row for something for each period. Also unlike these designs, the rows in the accumulating snapshot will be regularly updated after they have been inserted.
- The snapshot records the date each monitored processing stage was completed.
- These facts are sometimes referred to as “lags” because they represent the elapsed time between the dates associated with successive status milestones.
- Facts for elapsed time will be incremented as days go by, and milestone dates will be set whenever a new status is achieved. Mortgage_processing_facts, for example, will be updated nightly. During each load, the time an application has spent at its current stage will be incremented. If an application reaches a new stage, the appropriate day_key will be set, and the mortgage amount for the completed stage will be
recorded.
 ![Accumulating snapshot](https://github.com/STEFANOVIVAS/star-schema-notes/blob/main/images/accumulating_snapshot.png)

### Accumulating Snapshot Considerations
- When there is a very large number of status values, an accumulating snapshot can be designed to provide a simplified view of the process. Rather than track each individual status, you can design the snapshot to track the major milestones of a process.
- Rather than proceeding through a standard rigid set of milestones, the process may involve optional, alternative, or repeating steps. These situations do not preclude the use of an accumulating snapshot, but they will require some additional due diligence during the schema design process.

  Submitted → Reviewed → Processed → Underwritten → Settled  
  Submitted → Reviewed → Submitted → …

- When working with a nonlinear process, it is essential to work with business users to make determinations about which facts to increment at any given time and which dates to use when a milestone is reached. Remember.
- When something represented by the defining dimension of an accumulating snapshot undergoes a type 2 change, there will be two rows for it in the dimension table. The surrogate key of the most recent row should be used in the fact table. Do not use the natural key since this will result in double-counting.
