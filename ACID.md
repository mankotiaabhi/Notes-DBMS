# ACID Properties in DBMS

## Introduction

### What is ACID?

ACID is a set of properties that guarantee reliable and consistent
database transactions.

It ensures correctness even during: - System crashes - Power failures -
Concurrent access

------------------------------------------------------------------------

## What is a Transaction?

A transaction is a group of operations treated as a single logical unit
of work.

Example:

BEGIN; UPDATE accounts SET balance = balance - 500 WHERE id = 1; UPDATE
accounts SET balance = balance + 500 WHERE id = 2; COMMIT;

------------------------------------------------------------------------

# ACID Properties

## A --- Atomicity

A transaction either completes fully or does not happen at all.

Implemented using: - Write-Ahead Logging (WAL) - Undo logs - Rollback
mechanisms

------------------------------------------------------------------------

## C --- Consistency

The database moves from one valid state to another valid state.

Enforced by: - Primary Keys - Foreign Keys - Unique constraints - Check
constraints - Triggers

------------------------------------------------------------------------

## I --- Isolation

Concurrent transactions do not interfere improperly.

### Concurrency Problems

-   Dirty Read
-   Non-Repeatable Read
-   Lost Update
-   Phantom Read

Isolation Levels: - Read Uncommitted - Read Committed - Repeatable
Read - Serializable

------------------------------------------------------------------------

## D --- Durability

Once a transaction commits, the data is permanently stored.

Implemented using: - WAL - Redo logs - Checkpointing - Replication -
Backups

------------------------------------------------------------------------

# Transaction States

1.  Active
2.  Partially Committed
3.  Committed
4.  Failed
5.  Aborted
6.  Terminated

------------------------------------------------------------------------

# Schedules

## Serial Schedule

Transactions execute one after another.

## Concurrent Schedule

Transactions execute in interleaved manner.

------------------------------------------------------------------------

# Serializability

Ensures concurrent schedule gives same result as a serial schedule.

Types: - Conflict Serializability - View Serializability

------------------------------------------------------------------------

# ACID Summary

Atomicity → All or nothing
Consistency → Valid state maintained
Isolation → Safe concurrency
Durability → Permanent after commit