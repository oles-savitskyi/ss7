# Preview — Logical Storage Models

The previous sections of this specification define the architectural contracts of the Storage subsystem, including Storage Providers, Identity Model, Reference Model and Storage Entities.

This part defines the logical storage models used to persist business data.

A Logical Storage Model specifies how a particular category of business objects is represented within the Storage subsystem while remaining independent of any physical database implementation.

Logical Storage Models define:

- persistent structure;
- storage responsibilities;
- lifecycle participation;
- relationships;
- versioning;
- transaction behavior.

Logical Storage Models do not define:

- business rules;
- business validation;
- user interface behavior;
- query optimization;
- document posting logic.

These responsibilities belong to other platform subsystems.

Every Logical Storage Model SHALL:

- inherit the common persistence rules defined by this specification;
- remain independent of the selected Storage Provider;
- preserve identical logical behavior across all supported database engines;
- expose a stable contract to the Runtime subsystem.

The following Logical Storage Models are defined by the AcCore platform:

- Catalog Storage Model;
- Document Storage Model;
- Register Storage Model.

# 10. Catalog Storage Model

## 10.1 Overview

Catalog Storage Model defines the logical persistence model for catalog entities.

Catalogs represent long-lived business objects that are referenced throughout the platform.

Typical examples include:

- Products
- Customers
- Suppliers
- Employees
- Warehouses
- Currencies
- Measure Units

Catalog Storage Model defines how catalog data is persisted, versioned and referenced.

Business behavior, validation rules and user interaction remain outside the scope of Storage.

---

## 10.2 Design Goals

The Catalog Storage Model is designed to satisfy the following goals.

### Metadata Driven

Catalog structure SHALL be defined entirely by Metadata.

Storage MUST NOT require manual schema definition.

---

### Provider Independence

Catalog persistence MUST remain independent of the selected Storage Provider.

Catalog behavior SHALL remain identical across all supported providers.

---

### Extensibility

Catalogs MUST support extension through Metadata without requiring Storage architecture changes.

---

### Scalability

The model SHALL support:

- small embedded databases;
- medium business installations;
- large enterprise deployments.

---

### Transparency

Runtime and application code MUST interact with logical fields only.

Physical storage details SHALL remain hidden inside the Storage subsystem.

---

## 10.3 Logical Structure

Every catalog consists of the following logical layers.

```
Catalog
│
├── System Fields
│
├── Metadata Fields
│
├── Semantic Fields
│
└── User-defined Fields
```

Each layer serves a different purpose.

Storage SHALL expose a unified logical view regardless of physical implementation.

---

## 10.4 Logical Field Model

### Purpose

The Logical Field Model defines the relationship between Metadata, Runtime and Storage.

For Metadata and Runtime there exists only one concept:

```
Field
```

Storage determines how the field is physically persisted.

---

### Logical Field Principle

Metadata defines fields.

Runtime consumes fields.

Storage persists fields.

Neither Metadata nor Runtime SHALL depend on the physical storage strategy.

---

### Physical Storage Transparency

A logical field MAY be stored in:

```
Main Storage
```

or

```
EAV Storage
```

The choice is an internal Storage implementation detail.

Runtime MUST NOT distinguish between these storage mechanisms.

---

### Unified Access Model

All fields SHALL be accessed through a unified logical interface.

Examples:

```
Product.Name
```

```
Product.Barcode
```

```
Product.CustomAttribute
```

Runtime SHALL observe identical behavior regardless of physical storage location.

---

### Future Compatibility

Future Storage implementations MAY introduce additional persistence strategies.

Examples include:

- column-oriented storage;
- compressed storage;
- distributed storage;
- external storage providers.

The Logical Field Model MUST remain unchanged.

---

## 10.5 System Fields

### Purpose

System Fields provide platform-level functionality required by all catalog entities.

System Fields are defined by the platform and SHALL exist independently of Metadata.

---

### Core System Fields

Every Catalog Storage Entity SHALL contain the following fields.

| Field | Description |
|---------|-------------|
| id | Object identity (ULID) |
| version | Optimistic version |
| created_at | Creation timestamp |
| updated_at | Last modification timestamp |
| deleted | Logical deletion flag |

These fields SHALL be managed by the platform.

Application code MUST NOT modify them directly.

---

### Hierarchy Fields

If hierarchy is enabled by Metadata, the following additional fields SHALL exist.

| Field | Description |
|---------|-------------|
| parent_id | Parent catalog item |
| is_folder | Folder indicator |

If hierarchy is disabled, these fields MAY be omitted by the Storage implementation.

---

### Identity

The field:

```
id
```

SHALL contain the unique ULID of the catalog object.

Identity MUST remain immutable during the entire object lifetime.

---

### Version

The field:

```
version
```

SHALL support optimistic concurrency control.

The version SHALL increase only when persistent data changes.

---

### Timestamps

The fields:

```
created_at
updated_at
```

SHALL be managed automatically by the platform.

Storage Providers MAY use provider-specific timestamp implementations.

Logical behavior MUST remain identical.

---

### Logical Deletion

The field:

```
deleted
```

SHALL indicate logical deletion status.

Logical deletion preserves:

- references;
- historical integrity;
- auditability.

Physical deletion MAY occur later.

---

## 10.6 Metadata Fields

### Purpose

Metadata Fields define the business structure of a catalog.

Metadata determines:

- field names;
- types;
- semantics;
- constraints;
- indexes;
- default values.

Storage SHALL persist Metadata Fields without interpreting their business meaning.

---

### Field Definitions

Every Metadata Field SHALL be defined by Metadata.

Typical properties include:

- field_name;
- platform_type;
- semantic;
- nullable;
- default_value;
- indexed.

Additional properties MAY be introduced by future Metadata versions.

---

### Business Fields

Examples of Metadata Fields include:

```
name
```

```
full_name
```

```
description
```

```
manufacturer
```

```
weight
```

Storage SHALL treat these fields as ordinary persisted values.

---

### Required Fields

Metadata MAY define fields as mandatory.

Validation of required fields belongs to Runtime.

Storage SHALL persist values provided by Runtime.

---

### Constraints

Metadata MAY define constraints.

Examples include:

- uniqueness;
- maximum length;
- value range.

Storage MAY assist in constraint enforcement.

The authoritative validation logic belongs to Runtime.

---

### Type Preservation

Storage SHALL preserve:

- platform type;
- value precision;
- value scale;
- serialization format.

Type semantics are defined by the Platform Type System.

---

End of Chapter 10A.

## 10.7 Semantic Fields

### Purpose

Semantic Fields are Metadata Fields with predefined platform meaning.

Semantic Fields allow Runtime and platform services to provide specialized behavior while preserving Storage independence.

Storage SHALL persist Semantic Fields as ordinary field values.

Storage MUST NOT interpret semantic meaning.

---

### Semantic Definition

Metadata MAY assign a semantic identifier to a field.

Examples include:

- CODE
- BARCODE
- EMAIL
- PHONE
- URL

Additional semantic identifiers MAY be introduced by future platform versions.

---

### Semantic Contracts

Semantic identifiers define platform-level expectations.

Example:

```
BARCODE
```

indicates that the field contains barcode values.

Runtime MAY provide:

- barcode search;
- barcode validation;
- barcode scanning integration.

Storage remains unaware of these behaviors.

---

### Field Names

Field names and semantic identifiers are independent concepts.

Example:

```
field_name = product_barcode
semantic   = BARCODE
```

or

```
field_name = barcode
semantic   = BARCODE
```

Runtime behavior SHALL be determined by the semantic identifier rather than the field name.

---

### Storage Requirements

Storage SHALL:

- persist semantic identifiers;
- preserve semantic metadata;
- remain independent of semantic interpretation.

---

## 10.8 User-defined Fields (EAV)

### Purpose

User-defined Fields provide catalog extensibility without requiring schema modifications.

User-defined Fields SHALL be implemented using the Entity-Attribute-Value (EAV) model.

---

### Design Goals

The EAV model is intended to support:

- customer-specific extensions;
- industry-specific attributes;
- configuration-level customization;
- future schema evolution.

---

### Logical Model

For Runtime and Metadata, a User-defined Field is indistinguishable from any other logical field.

Example:

```
Product.CustomAttribute
```

Runtime SHALL access the field using the same mechanisms as Metadata Fields.

---

### Physical Transparency

Storage MAY persist User-defined Fields separately from the primary catalog structure.

Example:

```
Catalog Item
        │
        ▼
User-defined Field Values
```

This separation SHALL remain invisible outside the Storage subsystem.

---

### Metadata Definition

Each User-defined Field SHALL possess Metadata describing:

- field_name;
- platform_type;
- semantic (optional);
- default value;
- indexing requirements.

---

### Future Optimization

Storage MAY optimize EAV persistence using:

- caching;
- denormalization;
- materialization;
- adaptive indexing.

Logical behavior MUST remain unchanged.

---

## 10.9 Hierarchy

### Purpose

Catalogs MAY support hierarchical organization.

Hierarchy support SHALL be enabled or disabled through Metadata.

---

### Hierarchical Fields

Hierarchical catalogs SHALL contain:

| Field | Description |
|---------|-------------|
| parent_id | Parent catalog item |
| is_folder | Folder indicator |

---

### Root Objects

Objects located at the root level SHALL contain:

```
parent_id = NULL
```

NULL indicates the absence of a parent object.

---

### Folder Semantics

Objects with:

```
is_folder = true
```

represent grouping nodes.

Objects with:

```
is_folder = false
```

represent ordinary catalog items.

Metadata MAY restrict allowed hierarchy combinations.

---

### Hierarchy Integrity

Storage SHALL preserve hierarchy integrity.

The following conditions MUST NOT occur:

- circular references;
- self-references;
- invalid parent references.

Runtime SHALL perform business validation.

Storage SHALL preserve structural consistency.

---

### Deletion Behavior

Deletion of a folder containing child objects SHALL require explicit Runtime approval.

Typical behavior MAY include:

- deletion rejection;
- recursive logical deletion;
- user confirmation workflow.

Storage performs only persistence operations.

---

## 10.10 References

### Purpose

Catalog objects participate extensively in platform relationships.

References SHALL use the Platform Reference Model.

---

### Reference Representation

References SHALL store:

```
Referenced Object ULID
```

References MUST NOT depend on:

- names;
- codes;
- document numbers;
- physical storage identifiers.

---

### Reference Integrity

Storage SHALL preserve referential integrity.

A reference MUST either:

- reference an existing object; or
- contain NULL when allowed by Metadata.

---

### Cross-Catalog References

Catalogs MAY reference:

- other catalogs;
- documents;
- constants;
- registers.

Storage SHALL remain agnostic regarding business meaning.

---

## 10.11 Indexing

### Purpose

Indexes improve retrieval performance.

Indexing strategy SHALL remain independent of Runtime and application code.

---

### System Indexes

Storage SHALL automatically create indexes required for:

- object identity;
- versioning;
- hierarchy support;
- referential integrity.

---

### Metadata Indexes

Metadata MAY define additional indexes.

Examples include:

- CODE
- BARCODE
- EMAIL
- custom business fields

Storage Providers SHALL implement indexes using native capabilities.

---

### Adaptive Indexing

Storage MAY automatically create, modify or remove physical indexes.

Such optimizations MUST preserve identical logical behavior.

---

## 10.12 Lifecycle

### Purpose

Catalog objects participate in a standardized persistence lifecycle.

---

### Lifecycle States

Catalog objects SHALL follow the lifecycle:

```
Create
    │
    ▼
Persist
    │
    ▼
Update
    │
    ▼
Logical Delete
```

---

### Creation

Creation SHALL generate:

- ULID identity;
- version;
- timestamps.

Creation MUST occur within a transaction.

---

### Modification

Updates SHALL preserve:

- object identity;
- reference integrity;
- version consistency.

---

### Logical Deletion

Logical deletion SHALL preserve:

- references;
- history;
- register consistency.

Storage MAY physically remove deleted objects later.

---

## 10.13 Versioning

### Purpose

Catalogs SHALL use optimistic concurrency control.

---

### Version Increment

Version SHALL increase only when persistent data changes.

Examples:

```
Name changed
```

→ version increases

```
Object loaded
```

→ version unchanged

---

### Concurrent Updates

Storage SHALL detect version conflicts.

Conflict resolution belongs to Runtime.

---

### Identity Independence

Version and identity represent different concepts.

Changing version MUST NOT affect identity.

---

## 10.14 Transactions

### Purpose

All catalog modifications SHALL occur inside transactions.

---

### Transaction Scope

The following operations SHALL require transactions:

- create;
- update;
- delete;
- hierarchy modification;
- reference modification.

---

### Consistency

Transactions SHALL guarantee:

- atomicity;
- consistency;
- isolation;
- durability.

Provider-specific implementations MAY differ.

Logical behavior MUST remain identical.

---

## 10.15 Extensibility

The Catalog Storage Model SHALL support future extensions without requiring architectural redesign.

Possible future extensions include:

- distributed catalogs;
- column-oriented persistence;
- catalog partitioning;
- adaptive storage layouts;
- advanced search indexes.

Such extensions MUST preserve compatibility with the logical model defined by this specification.

---

End of Chapter 10.

# 11. Document Storage Model

## 11.1 Overview

Document Storage Model defines the logical persistence model for business documents.

Documents represent business events occurring at a specific point in time.

Typical examples include:

- Sales Invoice
- Purchase Invoice
- Goods Receipt
- Payment Order
- Inventory Adjustment
- Production Order

Documents may generate register movements through the Posting Engine.

The Storage subsystem is responsible only for document persistence.

Document behavior, validation rules and posting logic remain outside the scope of Storage.

---

## 11.2 Design Goals

The Document Storage Model is designed to satisfy the following goals.

### Event Representation

Documents SHALL represent business events.

A document records the state of a business operation at a specific moment.

---

### Metadata Driven

Document structure SHALL be defined entirely by Metadata.

Storage MUST NOT require manual schema definition.

---

### Provider Independence

Document persistence SHALL remain independent of the selected Storage Provider.

Logical behavior MUST remain identical across all supported providers.

---

### Transactional Consistency

Documents SHALL participate in transactional persistence.

Document data MUST remain internally consistent.

---

### Posting Independence

Storage SHALL persist document state.

Storage MUST NOT implement posting logic.

---

## 11.3 Logical Structure

Every document consists of two logical parts:

```
Document
│
├── Header
│
└── Tabular Sections
        │
        ├── Row
        ├── Row
        └── Row
```

The Header stores document-level information.

Tabular Sections store collections of business records associated with the document.

---

## 11.4 Document Header

### Purpose

The Header contains document attributes describing the business event.

Examples include:

- document date;
- customer;
- supplier;
- warehouse;
- currency;
- comments.

The exact structure is defined by Metadata.

---

### System Fields

Every document SHALL contain the following system fields.

| Field | Description |
|---------|-------------|
| id | Object identity (ULID) |
| version | Optimistic version |
| created_at | Creation timestamp |
| updated_at | Last modification timestamp |
| deleted | Logical deletion flag |

---

### Document Fields

Every document SHALL additionally contain:

| Field | Description |
|---------|-------------|
| document_date | Business date |
| document_number | Business number |
| posted | Posting state |

Additional fields SHALL be defined by Metadata.

---

## 11.5 Tabular Sections

### Purpose

Tabular Sections store collections of business records associated with the document.

Examples include:

- products;
- services;
- accounting entries;
- inventory movements;
- payment allocations.

---

### Definition

Tabular Sections SHALL be defined by Metadata.

A document MAY contain:

- no tabular sections;
- one tabular section;
- multiple tabular sections.

---

### Row Identity

Every tabular section row SHALL possess its own ULID.

Row identity remains independent of:

- row position;
- document number;
- physical storage implementation.

---

### Ownership

Every row SHALL reference its owning document.

Ownership SHALL be represented through object identity.

---

### Fields

Rows MAY contain:

- Metadata Fields;
- Semantic Fields;
- References.

The Logical Field Model defined by this specification applies equally to tabular section rows.

---

### Versioning

Tabular section modifications SHALL participate in document versioning.

Changes to tabular section data SHALL increment the document version.

---

## 11.6 Document Numbering

### Purpose

Document numbers provide business identification.

Document numbers are intended for:

- user interaction;
- reporting;
- printed forms;
- business communication.

---

### Identity Independence

Document numbers MUST NOT be used as object identity.

The following concepts are independent:

```
ULID
```

and

```
Document Number
```

ULID identifies the object.

Document Number identifies the business document.

---

### Number Generation

Document numbers SHALL be generated by the Numbering subsystem.

Storage persists generated numbers.

Storage MUST NOT implement numbering logic.

---

### Numbering Policies

Supported numbering policies MAY include:

- continuous numbering;
- yearly numbering;
- monthly numbering;
- custom numbering.

Number generation rules are outside the scope of Storage.

---

## 11.7 Posting State

### Purpose

Documents MAY participate in posting.

Posting transforms document data into register movements.

---

### State Representation

Posting state SHALL be represented by:

```
posted
```

Possible values include:

```
true
false
```

---

### Storage Responsibilities

Storage SHALL:

- persist posting state;
- version posting state changes;
- include posting state in transactions.

Storage MUST NOT:

- calculate register movements;
- validate posting rules;
- determine posting eligibility.

---

## 11.8 Register Integration

### Purpose

Documents may serve as sources of register movements.

---

### Responsibility Separation

The following responsibilities belong to the Posting Engine:

- movement generation;
- movement recalculation;
- movement reversal;
- register updates.

Storage persists the resulting data.

---

### Traceability

Register movements SHOULD maintain references to:

- source document;
- source tabular section row (when applicable).

This allows complete traceability between documents and registers.

---

## 11.9 Lifecycle

Documents SHALL participate in the standard persistence lifecycle.

```
Create
    │
    ▼
Persist
    │
    ▼
Modify
    │
    ▼
Post / Unpost
    │
    ▼
Logical Delete
```

Posting state changes SHALL NOT affect document identity.

---

## 11.10 Versioning

### Purpose

Documents SHALL use optimistic concurrency control.

---

### Version Increment

Document version SHALL increase when:

- header fields change;
- tabular section data changes;
- posting state changes.

---

### Version Stability

Document version SHALL NOT change when:

- document is loaded;
- document is read;
- document is referenced by another object.

---

### Identity Independence

Version and identity represent independent concepts.

Changing the version MUST NOT affect document identity.

---

## 11.11 Transactions

### Purpose

All document modifications SHALL occur inside transactions.

---

### Transaction Scope

The following operations SHALL require transactional execution:

- document creation;
- document modification;
- tabular section modification;
- posting state changes;
- document deletion.

---

### Atomicity

Document updates SHALL be atomic.

Header and tabular section modifications MUST be committed together.

Partial document updates MUST NOT be observable.

---

### Register Consistency

When posting generates register movements, document persistence and movement persistence SHOULD participate in the same logical transaction.

The exact implementation depends on the Storage Provider.

---

## 11.12 Extensibility

The Document Storage Model SHALL support future extensions without architectural redesign.

Possible future extensions include:

- document attachments;
- document version history;
- distributed document storage;
- document partitioning;
- document snapshots.

Such extensions MUST preserve compatibility with the logical model defined by this specification.

---

End of Chapter 11.

# 12. Register Storage Model

## 12.1 Overview

Register Storage Model defines the logical persistence model for platform registers.

Registers store business facts and system state derived from business operations.

Registers provide the foundation for balances, totals, historical analysis and operational reporting.

The platform defines two register categories:

- Accumulation Registers
- Information Registers

Register behavior is defined by Metadata and Runtime.

Storage is responsible only for persistence.

---

## 12.2 Design Goals

The Register Storage Model is designed to satisfy the following goals.

### State Representation

Registers SHALL represent business state rather than business events.

Documents describe events.

Registers describe resulting state.

---

### Provider Independence

Register persistence SHALL remain independent of the selected Storage Provider.

Logical behavior MUST remain identical across all supported providers.

---

### Transactional Consistency

Register updates SHALL participate in transactions.

Register state MUST remain internally consistent.

---

### Historical Preservation

Registers SHALL preserve historical information.

Past register state MUST remain available for analysis and reporting.

---

### Performance

The model SHALL support efficient:

- balance calculation;
- aggregation;
- filtering;
- reporting.

---

## 12.3 Register Categories

The platform defines two register categories.

```
Register
│
├── Accumulation Register
│
└── Information Register
```

Additional register categories MAY be introduced in future platform versions.

---

# 12.4 Accumulation Register Model

## Purpose

Accumulation Registers store movements that affect balances.

Typical examples include:

- Inventory
- Cash
- Accounts Receivable
- Accounts Payable
- Production Resources

---

## Logical Structure

An Accumulation Register consists of:

```
Accumulation Register
│
├── Movements
│
└── Totals
```

Movements store business history.

Totals store aggregated state.

---

## Movement Records

Every movement SHALL contain:

| Field | Description |
|---------|-------------|
| id | Movement identity (ULID) |
| period | Business timestamp |
| document_id | Source document |
| movement_type | INCOME or EXPENSE |

Additional fields SHALL be defined by Metadata.

---

## Dimensions

Dimensions identify the balance being affected.

Examples include:

- Product
- Warehouse
- Customer
- Currency
- Project

Dimensions SHALL be defined by Metadata.

---

## Resources

Resources represent accumulated values.

Examples include:

- Quantity
- Amount
- Weight
- Volume

Resources SHALL use Platform Types.

Resource values SHALL remain non-directional.

Movement direction SHALL be represented exclusively through:

```
movement_type
```

---

## Movement Types

The platform defines two movement types.

```
INCOME
```

```
EXPENSE
```

Direction MUST NOT be encoded through negative resource values.

This guarantees consistent aggregation behavior.

---

## Historical Integrity

Movements SHALL remain immutable after successful posting.

Corrections SHALL be represented through additional movements rather than direct modification.

---

# 12.5 Totals Model

## Purpose

Totals provide accelerated access to accumulated balances.

Totals are derived from movements.

Totals SHALL NOT replace movements.

---

## Separation Principle

Movements and totals SHALL be stored independently.

```
Register
│
├── Movements
│
└── Totals
```

Movement history remains the authoritative source of truth.

Totals serve as an optimization mechanism.

---

## Rebuild Capability

Totals MUST be fully reconstructible from movement history.

Loss of totals MUST NOT result in loss of business data.

---

## Granularity

Totals MAY be maintained at different granularities.

Examples include:

- yearly;
- quarterly;
- monthly;
- daily.

The selected strategy SHALL remain transparent to Runtime.

---

## Adaptive Totals

The platform MAY automatically optimize totals granularity.

Possible progression:

```
Yearly
    ↓
Quarterly
    ↓
Monthly
    ↓
Daily
```

Optimization decisions MAY be based on:

- movement volume;
- query patterns;
- reporting requirements;
- storage characteristics.

Logical behavior MUST remain unchanged.

---

## Required Baseline

Every Accumulation Register SHALL support yearly totals.

Yearly totals represent the minimum guaranteed optimization level.

---

# 12.6 Information Register Model

## Purpose

Information Registers store business facts that do not represent accumulation.

Examples include:

- Exchange Rates
- Product Prices
- Tax Rates
- User Settings
- Configuration Values

---

## Logical Structure

Information Registers consist solely of records.

```
Information Register
│
└── Records
```

No balance calculation is required.

---

## Dimensions

Information Registers MAY define dimensions.

Examples include:

- Currency
- Product
- Customer
- Region

Dimensions are defined by Metadata.

---

## Attributes

Information Registers MAY define attributes.

Examples include:

- Rate
- Price
- Description
- Status

Attributes are defined by Metadata.

---

## Periodicity

Information Registers MAY be:

- periodic;
- non-periodic.

---

## Periodic Registers

Periodic registers SHALL contain:

```
period
```

The period defines record validity in time.

---

## Non-Periodic Registers

Non-periodic registers store only the latest state.

Historical tracking is optional.

---

# 12.7 References

Registers MAY reference:

- catalogs;
- documents;
- constants;
- other registers.

All references SHALL use the Platform Reference Model.

---

# 12.8 Lifecycle

Registers participate in the standard persistence lifecycle.

```
Create
    │
    ▼
Persist
    │
    ▼
Update
    │
    ▼
Logical Delete
```

Accumulation Register movements MAY impose additional immutability rules.

---

# 12.9 Versioning

Registers SHALL use optimistic concurrency control.

Versioning rules defined by this specification apply to:

- movement records;
- totals records;
- information register records.

Version changes SHALL occur only when persistent data changes.

---

# 12.10 Transactions

All register modifications SHALL occur inside transactions.

---

## Atomicity

Register updates SHALL be atomic.

Partial register updates MUST NOT be observable.

---

## Posting Consistency

When document posting generates register movements:

```
Document Update
        +
Register Update
```

SHOULD participate in the same logical transaction.

---

## Totals Consistency

Movement persistence and totals updates SHALL remain transactionally consistent.

Totals MUST NOT reflect uncommitted movements.

---

# 12.11 Extensibility

The Register Storage Model SHALL support future extensions without architectural redesign.

Possible future extensions include:

- distributed registers;
- adaptive partitioning;
- column-oriented storage;
- incremental aggregation;
- advanced analytical indexes.

Such extensions MUST preserve compatibility with the logical model defined by this specification.

---

End of Chapter 12.