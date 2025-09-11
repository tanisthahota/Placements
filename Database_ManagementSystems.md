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

## Database Models

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

## Functional Dependencies

### Definition
- Relationship between attributes where one attribute determines another
- If A → B, then A functionally determines B
- For every value of A, there's exactly one value of B

### Types
- *Trivial FD*: A → A (subset dependency)
- *Non-trivial FD*: A → B where B is not subset of A
- *Fully Functional*: A → B where B is not dependent on any proper subset of A
- *Partial Dependency*: Non-key attribute depends on part of composite primary key
- *Transitive Dependency*: A → B → C, so A → C indirectly

### Armstrong's Axioms
- *Reflexivity*: If B ⊆ A, then A → B
- *Augmentation*: If A → B, then AC → BC
- *Transitivity*: If A → B and B → C, then A → C

### Closure of Functional Dependencies
- Set of all FDs that can be derived from given FDs
- Used to find candidate keys and check normal forms

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

## Relational Algebra

### Basic Operations
- *Selection (σ)*: Select rows based on condition
- *Projection (π)*: Select specific columns
- *Union (∪)*: Combine relations with same schema
- *Set Difference (-)*: Tuples in first but not in second
- *Cartesian Product (×)*: All possible combinations
- *Rename (ρ)*: Change relation/attribute names

### Derived Operations
- *Intersection (∩)*: Common tuples in both relations
- *Join (⋈)*: Combine relations based on common attributes
- *Division (÷)*: Find tuples in first relation for all tuples in second

### Join Types
- *Natural Join*: Join on common attributes with same name
- *Equi Join*: Join using equality condition
- *Theta Join*: Join using any comparison operator
- *Outer Join*: Include unmatched tuples from one or both relations

## SQL (Structured Query Language)

### DDL (Data Definition Language)
```sql
CREATE TABLE, ALTER TABLE, DROP TABLE
CREATE INDEX, DROP INDEX
CREATE VIEW, DROP VIEW
```

### DML (Data Manipulation Language)
```sql
INSERT, UPDATE, DELETE, SELECT
```

### DCL (Data Control Language)
```sql
GRANT, REVOKE
```

### TCL (Transaction Control Language)
```sql
COMMIT, ROLLBACK, SAVEPOINT
```

### Common SQL Operations
- *Joins*: INNER, LEFT, RIGHT, FULL OUTER, CROSS
- *Aggregate Functions*: COUNT, SUM, AVG, MIN, MAX
- *Grouping*: GROUP BY, HAVING
- *Subqueries*: Correlated and non-correlated
- *Set Operations*: UNION, INTERSECT, EXCEPT

### Constraints
- *NOT NULL*: Attribute cannot be empty
- *UNIQUE*: No duplicate values allowed
- *PRIMARY KEY*: Combination of NOT NULL and UNIQUE
- *FOREIGN KEY*: References another table's primary key
- *CHECK*: Custom validation condition
- *DEFAULT*: Default value when none specified

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
- *Lost Update*: One transaction overwrites another's changes
- *Unrepeatable Read*: Different results when reading same data twice

### Locking Mechanisms
- *Shared Lock (S)*: Multiple transactions can read
- *Exclusive Lock (X)*: Only one transaction can write
- *Two-Phase Locking*: Growing and shrinking phases
- *Strict 2PL*: Hold all locks until transaction commits/aborts
- *Rigorous 2PL*: Hold all exclusive locks until end

### Deadlock
- Two or more transactions waiting for each other indefinitely
- *Detection*: Wait-for graph, timeout mechanisms
- *Prevention*: Wait-die, wound-wait schemes
- *Avoidance*: Banker's algorithm

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
- *B+ Tree*: Variant where data only in leaf nodes
- *Hash Index*: Fast for equality searches
- *Bitmap Index*: Good for low-cardinality data

### Sparse vs Dense Index
- *Dense Index*: Entry for every record in data file
- *Sparse Index*: Entry for every block/page, requires sorted data

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

### Heuristic Optimization Rules
- Push selections down to reduce intermediate results
- Push projections down to reduce data transfer
- Combine selections and projections with joins
- Choose most selective operations first

## Database Design

### ER Model (Entity-Relationship)
- *Entity*: Object or concept (rectangle)
- *Attribute*: Property of entity (oval)
- *Relationship*: Association between entities (diamond)
- *Cardinality*: One-to-one, one-to-many, many-to-many

### ER Diagram Components
- *Strong Entity*: Independent existence
- *Weak Entity*: Depends on strong entity for identification
- *Composite Attribute*: Can be broken into sub-attributes
- *Multivalued Attribute*: Can have multiple values
- *Derived Attribute*: Calculated from other attributes
- *Total Participation*: Every entity participates (double line)
- *Partial Participation*: Some entities may not participate

### ER to Relational Mapping
1. Strong entity becomes table
2. Weak entity includes owner's primary key
3. One-to-many: Foreign key in "many" side
4. Many-to-many: Create junction table
5. Multi-valued attributes become separate table

### Database Design Process
1. Requirements analysis
2. Conceptual design (ER model)
3. Logical design (relational schema)
4. Physical design (storage and indexing)

## Storage and File Organization

### File Organization Methods
- *Heap Files*: Unordered, fast insertion
- *Sequential Files*: Ordered by key, good for range queries
- *Hash Files*: Direct access using hash function
- *Index-Sequential*: Combination of sequential and index organization

### Hashing Techniques
- *Static Hashing*: Fixed number of buckets
- *Dynamic Hashing*: Buckets can grow/shrink
- *Extendible Hashing*: Directory-based approach
- *Linear Hashing*: Incremental expansion

### Storage Hierarchy
- Primary Storage: RAM (volatile, fast)
- Secondary Storage: Hard disks (non-volatile, slower)
- Tertiary Storage: Tapes, optical disks (archival)

### Buffer Management
- *Buffer Pool*: Main memory cache for disk pages
- *Replacement Policies*: LRU, FIFO, Clock algorithm
- *Pinning*: Keeping pages in buffer when needed

## Backup and Recovery

### Types of Failures
- *Transaction Failure*: Logical error, system error
- *System Failure*: Power failure, software crash
- *Media Failure*: Disk crash, head crash

### Recovery Techniques
- *Log-based Recovery*: Undo/Redo operations using transaction logs
- *Shadow Paging*: Maintain shadow copy of database
- *Checkpoints*: Periodic saves to reduce recovery time

### Log Records
- *Undo Log*: Old values for rollback
- *Redo Log*: New values for recovery
- *Undo-Redo Log*: Both old and new values

### Recovery Algorithms
- *Immediate Update*: Changes written to database immediately
- *Deferred Update*: Changes written only after commit
- *ARIES*: Algorithm for Recovery and Isolation Exploiting Semantics

### Backup Strategies
- *Full Backup*: Complete copy of database
- *Incremental Backup*: Changes since last backup
- *Differential Backup*: Changes since last full backup

## Data Warehousing and OLAP

### Data Warehouse Characteristics
- *Subject-oriented*: Organized by business subject
- *Integrated*: Data from multiple sources
- *Time-variant*: Historical data preserved
- *Non-volatile*: Data not updated, only queried

### OLTP vs OLAP
- *OLTP*: Online Transaction Processing, day-to-day operations
- *OLAP*: Online Analytical Processing, complex queries and analysis

### Data Warehouse Architecture
- *ETL Process*: Extract, Transform, Load
- *Data Mart*: Subset of data warehouse for specific department
- *Metadata*: Data about data, schema information

### OLAP Operations
- *Drill-down*: Move from summary to detailed data
- *Roll-up*: Move from detailed to summary data
- *Slice*: Select specific dimension value
- *Dice*: Select multiple dimension values
- *Pivot*: Rotate data to see different perspective

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

### Distribution Strategies
- *Fragmentation*: Horizontal, vertical, mixed
- *Replication*: Full, partial, no replication
- *Allocation*: Where to store fragments/replicas

### Distributed Query Processing
- Query decomposition
- Data localization
- Global optimization
- Local optimization

### Two-Phase Commit Protocol
- *Phase 1*: Coordinator asks all sites to prepare
- *Phase 2*: Coordinator tells all sites to commit/abort
- Ensures atomicity in distributed transactions

## NoSQL Databases

### Types
- *Document*: MongoDB, CouchDB (JSON-like documents)
- *Key-Value*: Redis, DynamoDB (simple key-value pairs)
- *Column-Family*: Cassandra, HBase (column-oriented)
- *Graph*: Neo4j, Amazon Neptune (nodes and relationships)

### CAP Theorem
- *Consistency*: All nodes see same data simultaneously
- *Availability*: System remains operational
- *Partition Tolerance*: System continues despite network failures
- Can only guarantee two out of three properties

### BASE Properties (NoSQL alternative to ACID)
- *Basically Available*: System remains available
- *Soft State*: Data consistency not guaranteed at all times
- *Eventual Consistency*: System becomes consistent over time

