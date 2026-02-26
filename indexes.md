# Indexing in DBMS

## What is Indexing?

An **Index in DBMS** is used for faster retrieval of data from a table.

---

## Why Do We Need Indexes?

```sql
SELECT * FROM users WHERE email = 'abc@gmail.com';
```

**Without index:**
- Database scans every row in the table (Full Table Scan)
- Time complexity ≈ **O(n)**

**With index:**
- Database directly jumps to matching rows
- Time complexity ≈ **O(log n)** (usually via B-Tree)

---

## Indexing Improves

- Search speed
- Sorting performance
- Join performance
- Filtering performance

---

## What is Stored in an Index?

```
Indexed Column Value → Pointer to actual row
```

---

## Internal Data Structures

### B-Tree
Used by MySQL, PostgreSQL, Oracle. Provides logarithmic search time and good range query support.

### Hash Index
Very fast for equality (`=`) but not suitable for range queries (`<`, `>`).

---

## Index Types

- **Primary Index**: Created on PRIMARY KEY, unique, one per table
- **Clustered Index**: Data is ordered but duplicates values, we also use block hanker
- **Unique Index**: Prevents duplicate values
- **Composite Index**: Index on multiple columns
- **Bitmap Index**: For low-cardinality data
- **Full-Text Index**: For text searching

---

## Clustered vs Non-Clustered Index

**Clustered Index** : Data itself is stored in sorted order.
**Non-Clustered Index** : Separate structure that points to data.

| Feature | Clustered | Non-Clustered |
|---------|-----------|---------------|
| Physical order | Yes | No |
| Quantity allowed | 1 | Many |
| Storage | Data itself | Separate structure |

---

## Selectivity

High selectivity (unique values) = good index candidate. Low selectivity = poor index.

---

## Trade-offs

**Advantages**: Faster searches and queries

**Disadvantages**: Extra storage, slower INSERT/UPDATE/DELETE operations

---

## Best Practices

- Index columns in WHERE, JOIN, ORDER BY, GROUP BY
- Avoid indexing low-cardinality columns
- Avoid redundant indexes
- Don't over-index

---

## I/O Cost Reduction

Indexing reduces I/O cost by:
- Avoiding full table scans
- Using shallow B-Tree structures
- Narrowing search space quickly


## Dense vs Sparse Index

| Feature | Dense Index | Sparse Index |
|---------|-------------|--------------|
| Entry for every row | Yes | No |
| Entry per page | No | Yes |
| Storage size | Larger | Smaller |
| Search speed | Faster direct | Slightly slower |
| Used in | Non-clustered | Clustered |





