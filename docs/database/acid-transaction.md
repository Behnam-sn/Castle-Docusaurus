# ACID Transaction

Atomicity: All changes to data are performed as if they are a single operation. That is, all the changes are performed, or none of them are.

Consistency: Data remains in a consistent state from state to finish, reinforcing data integrity.

Isolation: The intermediate state of a transaction is not visible to other transactions, and as a result, transactions that run concurrently appear to be serialized.

Durability: After the successful completion of a transaction, changes to data persist and are not undone, even in the event of a system failure.

From <https://www.ibm.com/topics/relational-databases>
From <https://www.mongodb.com/basics/acid-transactions>
