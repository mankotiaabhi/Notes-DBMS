# SQL Joins – 

---

# 1. Why Do We Need Joins?

Joins are used to combine data from multiple tables.

Since relational databases store data in separate tables, joins allow us to:

- Retrieve related data
- Combine rows based on a condition
- Create meaningful result sets

Joins do NOT modify data.
They only create a temporary result set.

---

# 2. SQL JOIN Types Overview

| Join Type   | Description | Unmatched Left Rows | Unmatched Right Rows |
|-------------|------------|---------------------|----------------------|
| INNER JOIN  | Returns only matching rows from both tables | No | No |
| LEFT JOIN   | Returns all rows from left table and matching rows from right table | Yes | No |
| RIGHT JOIN  | Returns all rows from right table and matching rows from left table | No | Yes |
| FULL JOIN   | Returns all rows from both tables | Yes | Yes |
| CROSS JOIN  | Returns all possible combinations of rows (Cartesian Product) | — | — |
| SELF JOIN   | A table joined with itself | Depends | Depends |

---

# 3. Result Size Behavior

| Join Type  | Minimum Result Size |
|------------|--------------------|
| INNER JOIN | Less than or equal to matching rows |
| LEFT JOIN  | At least size of left table |
| RIGHT JOIN | At least size of right table |
| FULL JOIN  | At least size of larger table |
| CROSS JOIN | Left table size × Right table size |

---

# 4. What Actually Happens When You Write a JOIN?

When you write a JOIN:

1. Database reads rows from first table
2. Reads rows from second table
3. Compares rows using the ON condition
4. Produces a virtual result set

A JOIN does not permanently change data.

---

# 5. Logical Query Execution Order

Even if SQL is written differently, the logical execution order is:

1. FROM
2. JOIN
3. ON
4. WHERE
5. GROUP BY
6. HAVING
7. SELECT
8. ORDER BY

---

# 6. How Different Joins Work Internally

## INNER JOIN

Conceptually:

For each row in A:
    For each row in B:
        If condition matches:
            Include row

Only matching rows are returned.

---

## LEFT JOIN

For each row in A:
    If matching row found in B:
        return combined row
    Else:
        return A row + NULL values for B columns

Left table rows are always preserved.

---

## RIGHT JOIN

Same as LEFT JOIN but tables are swapped.

RIGHT JOIN = LEFT JOIN (swap table order)

---

## FULL JOIN

Combination of:

- LEFT JOIN
- RIGHT JOIN

Returns all rows from both tables.

---

## CROSS JOIN

No condition.

For each row in A:
    For each row in B:
        combine them

Result size = A × B

This is called Cartesian Product.

---

# 7. Physical Join Algorithms

Database engines use optimized algorithms.

## 1. Nested Loop Join

For each row in A:
    Scan entire table B

Time complexity ≈ O(n × m)

Simple but slow for large tables.

---

## 2. Hash Join

Used for equality joins (=).

Steps:
1. Build hash table for smaller table
2. Scan larger table
3. Match using hash lookup

Faster than nested loop.

---

## 3. Merge Join

Used when tables are sorted on join key.

Steps:
- Walk through both tables together
- Match rows sequentially

Very efficient when indexes exist.

---

# 8. JOIN Conditions

Join conditions can include:

- Equality (=)
- Inequality (<, >)
- Multiple conditions
- AND / OR
- Composite keys

Example:

```sql
ON A.id = B.id AND A.type = B.type
```