# ACID + isolation levels + anomalies

## ACID

- Atomicity. Transaction is a set of operations executed as indivisible unit. If all are successfull changes saved. If one of them failed nothing is saved.
- Consistency. Before and after transaction DB persists in consistent state.
- Isolation. One transaction should not affect another transaction if both running concurrently.
- Durability. If transaction is commited there is a guarantee its ata will persist even after crush.

## Isolation levels

- Read uncommited. The transaction can read data changed by another one even in case it's not commited.
- Read commited. If transaction changed data but not commited these changes aren't visible to other transactions.
- Repeatable read. If you read the same data several time within the same transaction it always stay same. You can;t read data used by another transaction.
- Serializable. Highest level of isolation. If transactions operate with same records they are executed consequitively.

## Corresponding phenomena

- Dirty read
- Non-repeatable read
- Lost update
- Phantom read
- Serialization anomaly

[Boris Strelnikov]: https://mkdev.me/posts/transaction-isolation-levels-with-postgresql-as-an-example
