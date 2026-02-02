# 🗄️ Database Management Systems - Last Minute Notes

## Quick Navigation
- [ER Model](#er-model)
- [Relational Model](#relational-model)
- [SQL](#sql)
- [Normalization](#normalization)
- [Transactions](#transactions)
- [Concurrency Control](#concurrency-control)
- [Indexing](#indexing)

---

# ER Model

## 1. ER Diagram Components

### 💡 Basic Components
```
Entity: Rectangle
  - Strong Entity: Simple rectangle
  - Weak Entity: Double rectangle

Attribute: Oval
  - Simple: Single oval
  - Composite: Oval with sub-ovals
  - Multivalued: Double oval
  - Derived: Dashed oval
  - Key: Underlined

Relationship: Diamond
  - Strong: Simple diamond
  - Identifying (Weak): Double diamond
```

### 💡 Cardinality Ratios
```
1:1 (One-to-One)
1:N (One-to-Many)
M:N (Many-to-Many)

Participation:
- Total (mandatory): Double line
- Partial (optional): Single line
```

---

## 2. ER to Relational Mapping

### 💡 Mapping Rules
```
Strong Entity → Table
  Primary key: Entity's key attribute

Weak Entity → Table
  Primary key: Owner's key + Partial key

1:1 Relationship:
  - Merge with total participation side, OR
  - Add FK to either side

1:N Relationship:
  - Add FK to N-side (many side)

M:N Relationship:
  - Create new relation with FKs from both sides
  - Primary key: Combination of both FKs

Multivalued Attribute:
  - Separate table with FK to parent
```

### 💡 Minimum Tables
```
n entities, m relationships:

Best case: n tables (if 1:1 or 1:N relationships merge)
Worst case: n + m tables (if all M:N)
```

---

# Relational Model

## 1. Keys

### 💡 Types of Keys
```
Super Key: Any set of attributes uniquely identifying tuples
Candidate Key: Minimal super key
Primary Key: Chosen candidate key
Alternate Key: Candidate keys not chosen as primary
Foreign Key: Attribute referencing primary key of another table
Composite Key: Key with multiple attributes
```

---

## 2. Relational Algebra

### 💡 Basic Operations
| Operation | Symbol | Description |
|-----------|--------|-------------|
| Selection | σ | Filter rows (horizontal) |
| Projection | π | Select columns (vertical) |
| Union | ∪ | Combine tuples |
| Set Difference | - | Tuples in R but not in S |
| Cartesian Product | × | All combinations |
| Rename | ρ | Rename relation/attributes |

### 💡 Derived Operations
| Operation | Expression | Description |
|-----------|------------|-------------|
| Intersection | R ∩ S = R - (R - S) | Common tuples |
| Join (⋈) | σ(R × S) | Combine on condition |
| Natural Join | R ⋈ S | Join on common attributes |
| Division | R ÷ S | Tuples in R related to ALL in S |

### Examples
```
σ_salary>50000(Employee)         -- Selection
π_name,salary(Employee)          -- Projection
Employee ⋈ Department            -- Natural Join
π_name(σ_salary>50000(Employee)) -- Combined
```

### 💡 Join Types
```
Theta Join: R ⋈_θ S = σ_θ(R × S)
Equi Join: Theta join with equality condition
Natural Join: Equi join on same-named attributes, remove duplicates
Left Outer Join: Keep all tuples from left + matches
Right Outer Join: Keep all tuples from right + matches
Full Outer Join: Keep all tuples from both sides
```

---

# SQL

## 1. DDL (Data Definition Language)

```sql
CREATE TABLE Student (
    roll_no INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES Department(id)
);

ALTER TABLE Student ADD email VARCHAR(100);
ALTER TABLE Student DROP COLUMN email;
ALTER TABLE Student MODIFY name VARCHAR(100);

DROP TABLE Student;
TRUNCATE TABLE Student;  -- Delete all rows, keep structure
```

---

## 2. DML (Data Manipulation Language)

### 💡 Basic Queries
```sql
-- SELECT
SELECT * FROM Student;
SELECT name, salary FROM Employee WHERE dept = 'CS';
SELECT DISTINCT dept FROM Employee;

-- INSERT
INSERT INTO Student VALUES (1, 'John', 101);
INSERT INTO Student (roll_no, name) VALUES (2, 'Jane');

-- UPDATE
UPDATE Employee SET salary = salary * 1.1 WHERE dept = 'CS';

-- DELETE
DELETE FROM Student WHERE roll_no = 1;
```

### 💡 Aggregate Functions
```sql
COUNT(*), COUNT(column), COUNT(DISTINCT column)
SUM(column)
AVG(column)
MAX(column)
MIN(column)

-- With GROUP BY
SELECT dept, AVG(salary) FROM Employee GROUP BY dept;

-- With HAVING (filter on groups)
SELECT dept, AVG(salary) FROM Employee 
GROUP BY dept HAVING AVG(salary) > 50000;
```

### 💡 Order of Execution
```sql
FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT

-- Important: WHERE filters rows BEFORE grouping
--           HAVING filters AFTER grouping
```

---

## 3. Joins in SQL

```sql
-- INNER JOIN (only matching)
SELECT * FROM A INNER JOIN B ON A.id = B.id;

-- LEFT JOIN (all from left + matching)
SELECT * FROM A LEFT JOIN B ON A.id = B.id;

-- RIGHT JOIN (all from right + matching)
SELECT * FROM A RIGHT JOIN B ON A.id = B.id;

-- FULL OUTER JOIN
SELECT * FROM A FULL OUTER JOIN B ON A.id = B.id;

-- CROSS JOIN (Cartesian product)
SELECT * FROM A CROSS JOIN B;

-- Self Join
SELECT e1.name, e2.name AS manager 
FROM Employee e1, Employee e2 
WHERE e1.manager_id = e2.id;
```

---

## 4. Subqueries

```sql
-- IN subquery
SELECT * FROM Employee WHERE dept_id IN (SELECT id FROM Department WHERE name = 'CS');

-- EXISTS subquery
SELECT * FROM Employee e WHERE EXISTS (SELECT 1 FROM Project p WHERE p.emp_id = e.id);

-- Correlated subquery (references outer query)
SELECT * FROM Employee e WHERE salary > (SELECT AVG(salary) FROM Employee WHERE dept_id = e.dept_id);

-- Scalar subquery
SELECT name, (SELECT MAX(salary) FROM Employee) as max_sal FROM Employee;
```

---

## 5. Views

```sql
-- Create view
CREATE VIEW HighPaidEmployees AS
SELECT * FROM Employee WHERE salary > 100000;

-- Use view
SELECT * FROM HighPaidEmployees;

-- Drop view
DROP VIEW HighPaidEmployees;
```

---

# Normalization

## 1. Functional Dependencies

### 💡 FD Rules (Armstrong's Axioms)
```
Primary Rules:
1. Reflexivity: If Y ⊆ X, then X → Y
2. Augmentation: If X → Y, then XZ → YZ
3. Transitivity: If X → Y and Y → Z, then X → Z

Derived Rules:
4. Union: If X → Y and X → Z, then X → YZ
5. Decomposition: If X → YZ, then X → Y and X → Z
6. Pseudo-transitivity: If X → Y and WY → Z, then WX → Z
```

### 💡 Closure of Attributes
```
X⁺ = All attributes functionally determined by X

Algorithm:
1. Start with X⁺ = X
2. For each FD Y → Z:
   If Y ⊆ X⁺, add Z to X⁺
3. Repeat until no change
```

---

## 2. Normal Forms

### 💡 Normal Form Hierarchy
```
1NF ⊂ 2NF ⊂ 3NF ⊂ BCNF ⊂ 4NF ⊂ 5NF
```

### 💡 1NF (First Normal Form)
```
✓ All attributes are atomic (no multivalued attributes)
✓ No repeating groups
```

### 💡 2NF (Second Normal Form)
```
✓ 1NF
✓ No partial dependency
  (No non-prime attribute depends on part of candidate key)

Partial Dependency: A proper subset of CK → Non-prime attribute
```

### 💡 3NF (Third Normal Form)
```
✓ 2NF
✓ No transitive dependency
  (Non-prime attribute doesn't depend on non-prime attribute)

For every FD X → Y:
• X is a superkey, OR
• Y is part of some candidate key (prime attribute)
```

### 💡 BCNF (Boyce-Codd Normal Form)
```
For every non-trivial FD X → Y:
• X must be a superkey

Stricter than 3NF:
3NF allows Y to be prime attribute
BCNF doesn't allow any exception
```

### 💡 Quick Test
```
Given FD: X → Y

BCNF violation: X is not a superkey
3NF violation: X is not superkey AND Y is not prime attribute
2NF violation: X is proper subset of candidate key AND Y is non-prime
```

---

## 3. Decomposition

### 💡 Properties of Good Decomposition
```
1. Lossless Join: Original table can be reconstructed
   Test: Common attributes form superkey of at least one decomposed relation
   
2. Dependency Preservation: All FDs can be verified in decomposed relations
```

### Decomposition Algorithm (BCNF)
```
For each BCNF violation X → Y:
1. Create R1 = (X ∪ Y)
2. Create R2 = (R - Y) [original minus Y attributes]
3. Repeat for R1 and R2 until all in BCNF
```

---

## 4. Multivalued Dependencies (4NF)

### 💡 4NF
```
Multivalued Dependency: X →→ Y
Means: For each X value, Y values are independent of other attributes

4NF: For every MVD X →→ Y:
• X is a superkey, OR
• MVD is trivial (Y ⊆ X or X ∪ Y = all attributes)
```

---

# Transactions

## 1. ACID Properties

### 💡 ACID
```
Atomicity: All or nothing (Transaction either completes or rolls back)
Consistency: Database remains consistent before and after
Isolation: Concurrent transactions don't interfere
Durability: Committed changes are permanent
```

---

## 2. Transaction States

```
Active → Partially Committed → Committed
   ↓              ↓
Failed ←──────────┘
   ↓
Aborted
```

---

## 3. Schedules

### 💡 Schedule Types
```
Serial Schedule: Transactions execute one after another
Concurrent Schedule: Transactions interleave

Serializable: Equivalent to some serial schedule
Conflict Serializable: Can be transformed to serial via swapping
View Serializable: Same reads/writes/final writes
```

### 💡 Conflict Operations
```
Two operations conflict if:
1. They belong to different transactions
2. They access same data item
3. At least one is a write

Conflict pairs: W-W, R-W, W-R (same item)
Non-conflict: R-R (same item), any ops on different items
```

### 💡 Conflict Serializability Test
```
1. Create precedence graph
   - Node for each transaction
   - Edge Ti → Tj if operation of Ti conflicts with and precedes Tj
2. If graph has NO CYCLE → Conflict Serializable
3. Topological order gives equivalent serial schedule
```

### 💡 View Serializability
```
S1 is view equivalent to S2 if:
1. Same initial reads (same value read if no prior write)
2. Same value reads (Ti reads Tj's write → same in both)
3. Same final writes (same final write on each item)

View Serializable ⊃ Conflict Serializable
Testing view serializability is NP-complete
```

---

## 4. Recoverability

### 💡 Recoverable Schedule
```
If Tj reads from Ti, then Ti must commit before Tj commits
(Otherwise can't rollback Ti if Tj already committed)
```

### 💡 Cascadeless Schedule
```
Tj can only read value written by Ti after Ti commits
Prevents cascading rollbacks
Cascadeless ⊂ Recoverable
```

### 💡 Strict Schedule
```
Tj can only read OR write an item after Ti (who wrote it) commits
Strict ⊂ Cascadeless ⊂ Recoverable
```

---

# Concurrency Control

## 1. Lock-Based Protocols

### 💡 Lock Types
```
Shared Lock (S): Read-only, multiple transactions can hold
Exclusive Lock (X): Read/Write, only one can hold

Lock Compatibility:
        S    X
   S   Yes   No
   X   No    No
```

### 💡 Two-Phase Locking (2PL)
```
Growing Phase: Can acquire locks, cannot release
Shrinking Phase: Can release locks, cannot acquire

Guarantees conflict serializability
Does NOT prevent deadlocks

Strict 2PL: Hold all X-locks until commit
Rigorous 2PL: Hold all locks until commit
```

---

## 2. Timestamp-Based Protocols

### 💡 Basic Timestamp Protocol
```
Each transaction gets timestamp TS(Ti)
For each data item X, maintain:
- W-TS(X): Largest timestamp of transaction that wrote X
- R-TS(X): Largest timestamp of transaction that read X

Read X by Ti:
- If TS(Ti) < W-TS(X): Reject (reading too old value)
- Else: Allow, update R-TS(X) = max(R-TS(X), TS(Ti))

Write X by Ti:
- If TS(Ti) < R-TS(X): Reject (overwriting value already read)
- If TS(Ti) < W-TS(X): Reject (writing obsolete value) or ignore (Thomas write rule)
- Else: Allow, update W-TS(X) = TS(Ti)
```

### Thomas Write Rule
```
If TS(Ti) < W-TS(X): Ignore the write (don't reject)
Allows more schedules, still serializable
```

---

## 3. Deadlock Handling

### 💡 Deadlock Prevention
```
Wait-Die (Non-preemptive):
- Older waits for younger
- Younger aborts if needs resource held by older

Wound-Wait (Preemptive):
- Older wounds (aborts) younger
- Younger waits for older
```

### 💡 Deadlock Detection
```
Wait-for Graph:
- Node for each transaction
- Edge Ti → Tj if Ti waits for lock held by Tj
- Cycle → Deadlock
```

---

# Indexing

## 1. Index Types

### 💡 Index Classification
```
By structure:
- Ordered (B-tree, B+tree)
- Hash

By number of index levels:
- Single-level (Primary, Secondary, Clustering)
- Multi-level (B-tree, B+tree)

By organization:
- Dense: Entry for every record
- Sparse: Entry for some records (needs ordering)
```

---

## 2. B-Tree

### 💡 B-Tree Properties (Order m)
```
1. Root has at least 2 children (or 0 if leaf)
2. Internal nodes: ⌈m/2⌉ to m children
3. All leaves at same level
4. Keys in sorted order
5. Node with k children has k-1 keys
```

### 💡 B-Tree Formulas
```
Minimum keys in node: ⌈m/2⌉ - 1
Maximum keys in node: m - 1
Minimum children: ⌈m/2⌉
Maximum children: m

Height for n keys: O(log_(m/2) n)
```

---

## 3. B+ Tree

### 💡 B+ Tree Properties
```
1. All data in leaf nodes
2. Internal nodes only have keys (for navigation)
3. Leaves linked for sequential access
4. More keys per node than B-tree (no data in internal nodes)
```

### 💡 B+ Tree vs B-Tree
| Feature | B-Tree | B+ Tree |
|---------|--------|---------|
| Data location | All nodes | Leaves only |
| Leaf linking | No | Yes (sequential access) |
| Keys per node | Fewer | More |
| Range queries | Slower | Faster |
| Used in | DBMS indexes | DBMS indexes |

### 💡 B+ Tree Formulas (Order p, pointer size P, key size K, data pointer D)
```
Internal node: p pointers + (p-1) keys ≤ Block size
Leaf node: data pointers + keys ≤ Block size

Fan-out (p): Higher is better (shallow tree)
Height: log_p(n) where n is number of records
```

---

## 4. Hashing

### 💡 Static Hashing
```
Fixed number of buckets
Overflow handled by chaining
Problems: Fixed size, performance degrades
```

### 💡 Extendible Hashing
```
Dynamic hashing
Global depth: Bits used from hash value
Local depth: Bits used by bucket
Split on overflow, shrink when underflow
```

### 💡 Linear Hashing
```
Buckets added one at a time
Split pointer moves linearly
Less space overhead than extendible
```

---

## Quick Memory Tricks 🧠

1. **ACID**: "All Consistent, Isolated, Durable"
2. **Normal Forms**: "1NF=Atomic, 2NF=No Partial, 3NF=No Transitive, BCNF=LHS is Superkey"
3. **Armstrong's**: "RAT" - Reflexivity, Augmentation, Transitivity
4. **Conflict**: "RW, WR, WW conflict; RR doesn't"
5. **2PL Phases**: "Grow then Shrink"
6. **B+ Tree**: "Data at leaves, linked for range"

---

## 💡 Quick Formulas

```
Candidate key: Find closure of all combinations, minimal ones are CK
Closure X⁺: Start with X, keep adding determined attributes

B-tree height ≈ log_(m/2)(n)
B+ tree access = height + 1 (for data)

Conflict serializable if precedence graph is acyclic
```

---

## Common Mistakes to Avoid ⚠️

1. 3NF allows prime attribute on RHS, BCNF doesn't
2. HAVING filters after GROUP BY, WHERE filters before
3. NULL ≠ NULL in SQL comparisons
4. View serializable doesn't mean conflict serializable
5. 2PL prevents conflict serializability issues, not deadlocks
6. B+ tree stores data only in leaves
7. Cascadeless ⊂ Recoverable (not the reverse)
8. Partial dependency is about candidate key, not just primary key
