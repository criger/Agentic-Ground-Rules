# Architecture and project structure

## Default architectural model

Use MVC and DRY as the default structural model across languages and frameworks.

Framework terminology differs. React may use pages, components, hooks and clients where a server framework uses views, controllers, services and repositories. Names may change; responsibility boundaries must remain obvious.

A developer should quickly be able to answer:

```text
Where is this presented?
Where is the action received and coordinated?
Where does the business rule live?
Where is the data model defined?
Where is the contract declared?
Where is data loaded and stored?
Where are database and external integrations implemented?
```

If the answer is "all in one class or component", the design needs another pass.

## MVC with supporting layers

| Layer or folder | Responsibility | Should normally not contain |
| --- | --- | --- |
| `views`, `pages`, `components` | presentation, input and display state | SQL, connections, heavy business logic |
| `controllers`, `handlers` | receive requests/events, coordinate flow, produce responses | direct SQL, large calculations, domain implementation |
| `models`, `domain`, `entities` | domain concepts, values and relevant invariants | UI or transport framework details |
| `services`, `application`, `use-cases` | business rules, workflows and transaction boundaries | rendering and framework-specific UI |
| `interfaces`, `contracts`, `abstractions` | stable boundaries between layers and implementations | unrelated helper behaviour or mutable state |
| `repositories` | domain-oriented persistence operations | product flow or UI decisions |
| `data`, `database`, `db-connectors` | connections, pools, migrations and database configuration | business rules |
| `integrations`, `clients`, `gateways` | external APIs, queues and third-party systems | view state and product policy |
| `dto`, `mappers` | transport shapes and translation between layers | business orchestration |
| `validators` | reusable, bounded validation | database and UI orchestration |
| `helpers`, `utils` | small, general and preferably pure operations | orphaned domain logic |
| `config` | typed or centralized configuration | secrets and business logic |

A project does not need every folder. It does need an obvious home for every responsibility it uses.

## Example structures

Layer-oriented:

```text
src/
├─ controllers/
├─ views/ or pages/components/
├─ models/ or domain/
├─ services/ or use-cases/
├─ interfaces/ or contracts/
├─ repositories/
├─ data/
│  └─ db-connectors/
├─ integrations/ or clients/
├─ dto/
├─ mappers/
├─ validators/
└─ config/
```

Feature-oriented:

```text
src/
├─ features/
│  ├─ users/
│  │  ├─ controllers/
│  │  ├─ views/
│  │  ├─ models/
│  │  ├─ services/
│  │  └─ repositories/
│  └─ orders/
│     └─ ...
└─ shared/
   ├─ data/
   ├─ integrations/
   └─ small-pure-utilities/
```

Choose one understandable model and use it consistently. Do not randomly mix layer folders, feature folders and large root files without documenting why.

## Dependency direction

A typical flow is:

```text
View
  -> Controller
      -> Service / use case
          -> Interface
              -> Repository / integration implementation
                  -> Database / external service
```

Rules:

- A view must not know the database.
- A controller should be thin and delegate business logic.
- Domain models must not depend on UI or concrete database clients.
- Services should depend on contracts at replaceable external boundaries.
- Repositories hide persistence details from application logic.
- Database connectors own connection lifecycle and technical setup, not business flow.
- Integration clients normalize transport and errors, not product decisions.
- Avoid circular dependencies between layers.

## Thin controllers

A controller normally:

1. receives a request, event or user action
2. validates and normalizes transport input
3. calls a focused service or use case
4. maps the result to a response or view state
5. delegates errors to established handling

It should not own long queries, payment rules, complex calculations or large transformations.

## Models and data shapes

Separate these when their needs differ:

```text
Domain model / entity
  Domain concepts and invariants

DTO / request / response
  Transport between API, UI and application

Persistence model
  Database representation
```

Do not use one large object as a database row, domain object, API response and UI state merely because it is convenient initially.

## Interfaces and contracts

Name contracts after the role they provide:

```text
UserRepository
PaymentGateway
DocumentExporter
MarketDataClient
```

In languages without formal interfaces, use types, schemas, modules or documented function contracts.

Add an interface for a real boundary, alternative implementation, external dependency or meaningful testing seam. Do not create a one-to-one interface around every class as ceremony.

## Repositories and database access

```text
Controller
  -> Service
      -> Repository contract
          -> Repository implementation
              -> DB connector / data source
```

- SQL and database-specific mapping belong in repository/data layers.
- Credentials and connection strings do not belong in repository source code.
- Connection lifecycle, pooling and technical transaction support belong in data infrastructure.
- The service/use case normally owns the business transaction boundary.
- Ownership and authorization must be enforced in an authoritative server-side layer.

## React and other frontend frameworks

| Architectural role | React example |
| --- | --- |
| View | pages and presentational components |
| Controller | controller hooks, event handlers and use cases |
| Model | types, schemas, domain objects and bounded state |
| Service | application workflows and feature operations |
| Repository/client | API, storage and data-access adapters |
| Mapper/validator | normalization, mapping and validation |

A large component that renders UI, calls APIs, maps data, enforces business rules, manages modals and persists state is a god component. Split it by responsibility.

Hooks are not a new dumping ground. A very large controller hook may need separate orchestration, data and domain responsibilities.

## Large classes and god objects

Treat size as an architectural signal when:

- the unit has several independent reasons to change
- private methods form distinct responsibility groups
- it mixes presentation, orchestration, domain logic, persistence and integration
- tests require many unrelated dependencies
- a small fix requires understanding most of the file
- deep nesting, flags or large conditionals hide separate use cases

Do not use an arbitrary line count as the only metric. The responsibility should be describable precisely in one sentence.

## DRY: one natural source

Apply DRY to shared semantics:

- business rules and calculations
- validation and authorization checks
- mapping and normalization
- equivalent persistence queries
- API and integration contracts
- constants and configuration
- repeated UI behaviour

DRY does not mean that all visually similar code has the same meaning. Two small operations with different domain intent may be safer than one generic abstraction controlled by flags. Reuse semantics, not merely matching lines.

## Helpers are not an architecture

A helper should be small, clearly named and preferably free of hidden state or side effects.

Move it elsewhere when it owns domain rules, database access, a user flow, authentication state or many feature-specific branches. Avoid large `Utils`, `Common`, `Manager` and `Helper` classes that collect unrelated behaviour.

## Existing systems

Do not reorganize a working legacy system as part of an unrelated fix.

1. Understand the existing design and tests.
2. Place new code in the clearest available layer.
3. Extract one bounded responsibility when the touched unit would otherwise grow.
4. Preserve public behaviour and contracts.
5. Propose broad restructuring separately when it needs wider validation.

Improve MVC and DRY incrementally without turning a small repair into a risky rewrite.

## Architecture checklist for a feature

Before implementation, answer:

```text
Which view is affected?
Which controller or handler starts the flow?
Which service or use case owns the rule?
Which model or DTO describes the data?
Which interface defines the boundary?
Which repository or client loads or stores data?
Are mapping, validation or database connector changes required?
Which layers need isolated and integrated tests?
```

If everything is planned for one existing file, revisit the split before writing code.

Update project `architecture.md` when a lasting component, dependency, ownership, integration or deployment boundary changes.
