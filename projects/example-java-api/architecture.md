# Workshop Inventory API architecture

> Fictional example.

## Structure

```text
HTTP request
  -> InventoryController
      -> InventoryService
          -> InventoryRepository interface
              -> JpaInventoryRepository
                  -> PostgreSQL
```

```text
src/main/java/example/inventory/
├─ controller/
├─ domain/
├─ dto/
├─ mapper/
├─ repository/
├─ service/
├─ validation/
└─ config/
```

## Responsibilities

| Area | Owns | Does not own |
| --- | --- | --- |
| Controllers | transport validation, status codes, DTO mapping | inventory calculations, SQL |
| Domain | item, movement, reservation and invariants | HTTP or database configuration |
| Services | use cases and business transactions | response formatting |
| Repositories | persistence, queries and locking | business decisions |
| Flyway migrations | database schema history | runtime feature toggles |

## Transaction boundary

An inventory adjustment writes both an immutable movement and the resulting balance in one transaction.

```text
validate command
  -> load item with version
  -> calculate new balance
  -> append movement
  -> persist balance
  -> commit
```

The item version prevents silent lost updates. A concurrency conflict returns a retryable conflict response; it must not overwrite newer stock.

## API model boundary

Request/response DTOs are separate from JPA entities. Internal version fields and audit metadata are not writable client fields.

## Architecture verification

```bash
./mvnw test
./mvnw verify
```

Add a repository integration test when query, locking or migration behaviour changes.
