# Database Management Systems

## Database Fundamentals

### What is a Database?
- Collection of interrelated data stored in a computer system
- Organized to support efficient retrieval, insertion, and deletion
- Managed by Database Management System (DBMS)

### DBMS vs File System
- *Data Redundancy*: DBMS eliminates redundancy, file systems have duplication
- *Data Inconsistency*: DBMS ensures consistency across all data
- *Data Isolation*: DBMS provides integrated view, file systems store data separately
- *Integrity Problems*: DBMS enforces integrity constraints automatically
- *Atomicity Problems*: DBMS supports transactions, file systems don't
- *Concurrent Access*: DBMS handles multiple users, file systems have limited support
- *Security*: DBMS provides user authentication and authorization

##  Database Models

### Hierarchical Model
- Tree-like structure with parent-child relationships
- Each child has exactly one parent
- Example: File systems, organizational charts

### Network Model
- Graph structure allowing many-to-many relationships
- Uses pointers to connect records
- More flexible than hierarchical but complex

### Relational Model
- Data stored in tables (relations)
- Based on mathematical set theory
- Uses SQL for data manipulation
- Most widely used model

### Object-Oriented Model
- Data stored as objects with attributes and methods
- Supports inheritance and encapsulation
- Good for complex data types

## Relational Database Concepts

### Key Terms
- *Relation*: Table with rows and columns
- *Tuple*: Row in a table
- *Attribute*: Column in a table
- *Domain*: Set of allowed values for an attribute
- *Cardinality*: Number of tuples in a relation
- *Degree*: Number of attributes in a relation

### Keys
- *Primary Key*: Uniquely identifies each tuple, cannot be NULL
- *Foreign Key*: References primary key of another table
- *Candidate Key*: Attribute(s) that can serve as primary key
- *Super Key*: Set of attributes that uniquely identifies tuples
- *Composite Key*: Primary key consisting of multiple attributes
- *Alternate Key*: Candidate keys not chosen as primary key

## Normalization

### Purpose
- Eliminate data redundancy
- Minimize data inconsistency
- Optimize database structure

### Normal Forms

#### First Normal Form (1NF)
- Each attribute contains only atomic (indivisible) values
- No repeating groups or arrays
- Each row must be unique

#### Second Normal Form (2NF)
- Must be in 1NF
- All non-key attributes are fully functionally dependent on primary key
- Eliminate partial dependencies

#### Third Normal Form (3NF)
- Must be in 2NF
- No transitive dependencies
- Non-key attributes depend only on primary key

#### Boyce-Codd Normal Form (BCNF)
- Must be in 3NF
- For every functional dependency A→B, A must be a super key
- Stricter version of 3NF

#### Fourth Normal Form (4NF)
- Must be in BCNF
- No multi-valued dependencies

### Denormalization
- Intentionally introducing redundancy for performance
- Trade-off between storage space and query speed
- Common in data warehouses and reporting systems

## SQL (Structured Query Language)

### DDL (Data Definition Language)
```
sql
CREATE TABLE, ALTER TABLE, DROP TABLE
CREATE INDEX, DROP INDEX
CREATE VIEW, DROP VIEW
```

### DML (Data Manipulation Language)
```
sql
INSERT, UPDATE, DELETE, SELECT
```

### DCL (Data Control Language)
```
sql
GRANT, REVOKE
```

### TCL (Transaction Control Language)
```
sql
COMMIT, ROLLBACK, SAVEPOINT
```


### Common SQL Operations
- *Joins*: INNER, LEFT, RIGHT, FULL OUTER, CROSS
- *Aggregate Functions*: COUNT, SUM, AVG, MIN, MAX
- *Grouping*: GROUP BY, HAVING
- *Subqueries*: Correlated and non-correlated
- *Set Operations*: UNION, INTERSECT, EXCEPT

## Transactions and ACID Properties

### Transaction
- Sequence of database operations treated as a single unit
- Either all operations succeed (commit) or none do (rollback)

### ACID Properties
- *Atomicity*: All or nothing - transaction is indivisible
- *Consistency*: Database remains in valid state before and after transaction
- *Isolation*: Concurrent transactions don't interfere with each other
- *Durability*: Committed changes are permanent, survive system failures

### Transaction States
- Active, Partially Committed, Committed, Failed, Aborted

## Concurrency Control

### Problems in Concurrent Execution
- *Dirty Read*: Reading uncommitted data
- *Non-repeatable Read*: Reading different values in same transaction
- *Phantom Read*: New rows appearing during transaction

### Locking Mechanisms
- *Shared Lock (S)*: Multiple transactions can read
- *Exclusive Lock (X)*: Only one transaction can write
- *Two-Phase Locking*: Growing and shrinking phases

### Isolation Levels
- *Read Uncommitted*: Lowest isolation, allows dirty reads
- *Read Committed*: Prevents dirty reads
- *Repeatable Read*: Prevents dirty and non-repeatable reads
- *Serializable*: Highest isolation, prevents all anomalies

## Indexing

### Purpose
- Speed up data retrieval operations
- Reduce disk I/O operations
- Improve query performance

### Types of Indexes
- *Primary Index*: On primary key, automatically created
- *Secondary Index*: On non-key attributes
- *Clustered Index*: Data physically ordered by index key
- *Non-clustered Index*: Logical ordering, separate from data storage
- *Composite Index*: On multiple columns
- *Unique Index*: Ensures uniqueness of values

### Index Structures
- *B-Tree*: Balanced tree, good for range queries
- *Hash Index*: Fast for equality searches
- *Bitmap Index*: Good for low-cardinality data

## Query Optimization

### Steps in Query Processing
1. Parsing and translation
2. Optimization
3. Evaluation

### Query Optimization Techniques
- *Cost-based optimization*: Choose plan with lowest estimated cost
- *Rule-based optimization*: Apply predefined rules
- *Index selection*: Use appropriate indexes
- *Join order optimization*: Choose efficient join sequence

### Query Execution Plans
- Show how database executes a query
- Help identify performance bottlenecks
- Can be analyzed to optimize queries

##  Database Design

### ER Model (Entity-Relationship)
- *Entity*: Object or concept (rectangle)
- *Attribute*: Property of entity (oval)
- *Relationship*: Association between entities (diamond)
- *Cardinality*: One-to-one, one-to-many, many-to-many

### ER to Relational Mapping
1. Strong entity becomes table
2. Weak entity includes owner's primary key
3. One-to-many: Foreign key in "many" side
4. Many-to-many: Create junction table
5. Multi-valued attributes become separate table

## Storage and File Organization

### File Organization Methods
- *Heap Files*: Unordered, fast insertion
- *Sequential Files*: Ordered by key, good for range queries
- *Hash Files*: Direct access using hash function
- *Index-Sequential*: Combination of sequential and index organization

### Storage Hierarchy
- Primary Storage: RAM (volatile, fast)
- Secondary Storage: Hard disks (non-volatile, slower)
- Tertiary Storage: Tapes, optical disks (archival)

## Backup and Recovery

### Types of Failures
- *Transaction Failure*: Logical error, system error
- *System Failure*: Power failure, software crash
- *Media Failure*: Disk crash, head crash

### Recovery Techniques
- *Log-based Recovery*: Undo/Redo operations using transaction logs
- *Shadow Paging*: Maintain shadow copy of database
- *Checkpoints*: Periodic saves to reduce recovery time

### Backup Strategies
- *Full Backup*: Complete copy of database
- *Incremental Backup*: Changes since last backup
- *Differential Backup*: Changes since last full backup

## Distributed Databases

### Characteristics
- Data distributed across multiple sites
- Connected by network
- Appears as single database to users

### Advantages
- Reliability and availability
- Improved performance
- Local autonomy
- Scalability

### Challenges
- Data consistency
- Network communication overhead
- Security across sites
- Complexity of distributed transactions

### Drawbacks
- Single Point Failure

## NoSQL Databases

### Types
- *Document*: MongoDB, CouchDB (JSON-like documents)
- *Key-Value*: Redis, DynamoDB (simple key-value pairs)
- *Column-Family*: Cassandra, HBase (column-oriented)
- *Graph*: Neo4j, Amazon Neptune (nodes and relationships)
##

### CAP Theorem
- *Consistency*: All nodes see same data simultaneously
- *Availability*: System remains operational
- *Partition Tolerance*: System continues despite network failures
- Can only guarantee two out of three properties



