# Example: Workshop Inventory API

> **Fictional example.** Names, commits and runtime results in this directory exist only to demonstrate a compact project instruction set.

## Source repository

```text
example-org/workshop-inventory-api (fictional)
```

## Purpose

Workshop Inventory API tracks tools and consumable stock for a small repair workshop. Staff can register receipts, adjust stock and reserve items for work orders.

## Stack

```text
Java 21
Spring Boot 3.5
PostgreSQL 15
Flyway
Maven Wrapper
```

## Main flows

```text
Receive stock
  -> validate item and quantity
  -> append inventory movement
  -> update current balance

Reserve stock
  -> verify available quantity
  -> create reservation
  -> reduce available balance
```

## Local commands

```bash
./mvnw spring-boot:run
./mvnw test
./mvnw verify
```

The commands are documented examples. Verify them in the real source repository before use.

## Reading order

1. `architecture.md`
2. `current-status.md`
3. Relevant sections of `pitfalls.md`
4. Actual source on the verified branch

## Project-specific rules

- Controllers translate HTTP requests and responses only.
- `InventoryService` owns adjustment and reservation rules.
- Repositories own SQL/JPA persistence and locking details.
- Never allow a client to provide the authoritative current balance.
- A stock-changing request must fail as one unit when movement history and balance cannot both be persisted.

This small example intentionally omits separate `context.md`, `next-steps.md` and `handover.md`. Its stable context fits in the README.
