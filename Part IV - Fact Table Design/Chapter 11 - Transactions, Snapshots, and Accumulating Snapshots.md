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

 ## Snapshot Considerations

 - It may be useful to provide both transaction and snapshot representations of the same process; like two sides of the same coin, these models provide different and valuable perspectives of the same activities.
 - When a design will include both a transaction fact table and a periodic snapshot, the snapshot can and should be designed to use the transaction fact table as its data source.
