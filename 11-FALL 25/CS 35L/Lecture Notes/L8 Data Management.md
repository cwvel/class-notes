- **DBMS (Database Management System)**
	- SQL (Structured Query Language) is a declarative language used across most DBMS systems
		- **Declarative**: User specifies the operation, DBMS figures out how to do it efficiently
	- Database structures modeled using **Entity-Relationship Diagrams (ERDs)**
		- Defines entities, attributes, and their relationships
- **Relational vs. non-relational**
	- Relational: consistent and structured, good for complex queries
	- Non-relational: flexible and scalable, good for less structured data
- SQL queries
	- **Primary key**: a unique identifier for each entry in the table, must never be null
		- Links tables together (creates relations)
```sql
CREATE TABLE Student {
	uid INTEGER NOT NULL PRIMARY KEY,
	name VARCHAR(100) NOT NULL
}
```

### Database operations
**JOIN**
- Make temporary table that combines tables based on common attributes
**SELECTION ($\sigma$)**
- Use a Boolean predicate on rows to get a sub-table of what fits the filter
**PROJECTION ($\pi$)**
- Eliminates columns while keeping all rows
**GROUP BY**
- Aggregates all rows who have the same value in the given column

### Transactions: ACID
**A = Atomicity**
- A transaction is *all-or-nothing*: if any part fails, the database goes back to the previous state
**C = Consistency**
- Transaction must bring the database from one valid state to another (prevents invalid data from being written)
**I = Isolation**
- Concurrent transactions do not interfere with each other
- First transaction must finish before results can be viewed by other transactions
**D = Durability**
- Once the transaction is committed, its changes are permanent and will survive system failures

### NoSQL
- Stores data in flexible, non-tabular formats (documents, key-value pairs, graphs)
	- Helpful when your data doesn't fit the relational database model
- **Does not guarantee the ACID properties**
	- Weaker consistency models (eventual consistency) but more efficient
### CAP Theorem
1. **Consistency**: All nodes see the same data at the same time
2. **Availability**: Every request receives a response (even if stale)
3. **Partition tolerance**: System continues to operate despite network partitions
You can only pick two
- ATMS sacrifice consistency