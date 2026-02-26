# TRANSACTIONS IN DBMS – COMPLETE NOTES

---

# 1. What is a Transaction?

A transaction is a logical unit of work that consists of one or more database operations.
It must follow ACID properties.

Example:

BEGIN;
UPDATE accounts SET balance = balance - 500 WHERE id = 1;
UPDATE accounts SET balance = balance + 500 WHERE id = 2;
COMMIT;

---

# 2. Transaction States

1. Active – Transaction is executing.
2. Partially Committed – Final statement executed but not yet committed.
3. Committed – Successfully completed and changes are permanent.
4. Failed – Cannot proceed due to error/crash.
5. Aborted – Rolled back and database restored.
6. Terminated – Leaves the system after commit/abort.

State Flow:
Active → Partially Committed → Committed → Terminated
Active → Failed → Aborted → Terminated

---

# 3. Schedule

A schedule is the chronological order of execution of operations from multiple transactions.

---

## Serial Schedule

T1 → T2 → T3

Advantages:
- High consistency
- No concurrency anomalies

Disadvantages:
- Low throughput

---

## Concurrent (Parallel) Schedule

Operations interleave.

Advantages:
- High throughput
- Better CPU utilization

Disadvantages:
- Risk of anomalies

---

# 4. Concurrency Problems

## 1. Dirty Read (Uncommitted Read)
A transaction reads data written by another uncommitted transaction.

Prevented by:
- Read Committed and above

---

## 2. Non-Repeatable Read
Reading same row twice and getting different values due to committed update.

Prevented by:
- Repeatable Read
- Serializable

---

## 3. Lost Update
Two transactions update same data and one overwrites the other.

Prevented by:
- Proper locking
- Repeatable Read
- Serializable

---

## 4. Phantom Read
Re-executing a query returns new rows inserted by another committed transaction.

Prevented by:
- Serializable

---

# 5. Recoverability

## Recoverable Schedule
A transaction commits only after transactions whose data it read have committed.

Safe for recovery.

---

## Irrecoverable Schedule
A transaction commits before the transaction it depends on commits.

If the first rolls back → inconsistency.

Unsafe.

---

## Cascading Rollback
If one transaction aborts, dependent transactions must also abort.

---

## Cascadeless Schedule
Transactions read only committed data.
Prevents cascading rollback.

---

# 6. Serializability

Ensures concurrent schedule produces same result as serial schedule.

---

## Conflict Serializability

Based on swapping non-conflicting operations.

Uses Precedence Graph:
- Node = Transaction
- Edge = Conflict dependency

If graph has no cycle → Serializable.

---

## View Serializability

Preserves read-from and final-write relationships.
More flexible but harder to test.

---

# 7. Concurrency Control Techniques

- Two Phase Locking (2PL)
- Strict 2PL
- Timestamp Ordering
- MVCC (Multi-Version Concurrency Control)

---

# 8. Two Phase Locking (2PL)

Phase 1: Growing (acquire locks)
Phase 2: Shrinking (release locks)

Guarantees conflict serializability.

Strict 2PL:
Releases locks only after commit/abort.
Prevents cascading rollback.

---

# 9. Isolation Levels

1. Read Uncommitted
2. Read Committed
3. Repeatable Read
4. Serializable

Higher isolation → More consistency → Less concurrency

---

# FINAL SUMMARY

Transaction = Logical unit of work  
States = Active → Commit/Abort → Terminated  
Schedules = Serial or Concurrent  
Problems = Dirty, Non-repeatable, Lost update, Phantom  
Solutions = Locking, 2PL, Isolation levels  
Goal = Serializability and Recoverability  
"""