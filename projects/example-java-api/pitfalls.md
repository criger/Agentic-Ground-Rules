# Workshop Inventory API pitfalls

> Fictional example.

## Do not calculate authoritative stock in the controller

**Risk:** Two endpoints implement slightly different balance rules.

**Safe model:** Every stock-changing operation calls the same domain/application service. Controllers map transport data only.

**Regression test:** Receipt and reservation tests must assert the resulting movement and balance.

## Preserve optimistic locking

**Tempting change:** Remove the entity version after seeing occasional conflicts.

**Why it is wrong:** The conflict prevents concurrent requests from silently overwriting one another.

**Safe response:** Return a conflict result and let the caller refresh/retry explicitly.

## Never edit an applied Flyway migration

Add a new migration instead. Editing a migration already applied to another environment breaks schema history and checksum validation.

## Keep DTOs separate from entities

Binding request payloads directly to JPA entities can expose version and audit fields and create accidental persistence behaviour.

Verify request mapping and forbidden-field handling whenever DTOs change.
