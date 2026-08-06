# AcCore Glossary

**Status:** Draft

**Version:** 0.1

**Language:** English

---

# 1. Purpose

This document defines the official terminology of the AcCore platform.

Its purpose is to establish a consistent vocabulary for all architectural, engineering, and user documentation.

Every architectural term used within the AcCore project shall have a single normative definition.

This document is normative.

---

# 2. Scope

This glossary defines concepts that belong specifically to the AcCore platform.

General software engineering terminology and implementation technologies are outside the scope of this document unless they acquire a specific meaning within AcCore.

---

# 3. Conventions

Definitions describe concepts rather than implementations.

Definitions should remain stable even if implementation technologies change.

Each architectural term shall have exactly one normative definition.

Documents shall use terminology consistently with this glossary.

Terms are listed in alphabetical order.

---

# 4. Terms

## Accumulation Register

A register that stores business movements affecting balances and accumulated values.

Accumulation Registers consist of movement records and totals. Movements represent historical business events, while totals provide optimized access to balances.

Examples include inventory balances, cash balances, accounts receivable and accounts payable.

---

## Architecture

**Category:** Foundation

**Status:** Stable

**Definition**

The fundamental organization of the AcCore platform, including its concepts, principles, components, relationships, and evolution.

**See also**

- Core
- Platform

---

## Adaptive Totals Strategy

A Totals Engine strategy that allows totals storage granularity to vary according to workload and data volume.

Supported granularities include:

Yearly
Quarterly
Monthly
Daily

---

## Balance

An aggregated representation of register resources for a specific dimension set and point in time.

Balances are derived data maintained by the Totals Engine.

Balances are not primary facts.

---

## Balance Query

A Register Query that retrieves register state and answers the question:

"What is the state?"

---

## Business Process

**Category:** Business

**Status:** Stable

**Definition**

A sequence of business activities implemented by a configuration to achieve a specific organizational objective.

**See also**

- Configuration

---

## Capability

**Category:** Foundation

**Status:** Stable

**Definition**

A reusable functional responsibility provided by the platform independently of any specific business domain.

**See also**

- Platform Capability
- Configuration

---

## Configuration

**Category:** Foundation

**Status:** Stable

**Definition**

A business solution built on top of a platform edition by defining business processes, metadata, and business logic.

Configurations extend platform functionality without modifying the platform architecture.

**See also**

- Platform
- Platform Edition
- Metadata
- Standard Configuration

---

## Contract

A Contract is the published architectural agreement between a component and its consumers.

A Contract defines the capabilities, responsibilities, guarantees and compatibility rules that a component provides.

Consumers interact with a component exclusively through its published Contract.

A Contract is independent of any particular implementation technology or programming language.

---

## Core

**Category:** Foundation

**Status:** Stable

**Definition**

The common architectural foundation shared by every AcCore platform edition.

**See also**

- Platform
- Platform Edition

---

### Dependency Graph

A directed graph describing influence relationships between posted objects.

Dependency Graph is used to identify affected objects, support consistency analysis, and determine reposting scope after accounting data changes.

Dependencies are established through register participation rather than direct document-to-document relationships.

---

## Development Environment

**Category:** Platform

**Status:** Stable

**Definition**

The set of tools used to create, maintain, test, and deploy AcCore configurations.

**See also**

- Configuration
- Platform

---

### Dirty Object

A posted object whose accounting consistency may be affected by external changes.

A Dirty Object is marked with the DIRTY consistency state and may require reposting or other consistency restoration procedures.

Being marked DIRTY does not necessarily indicate incorrect accounting data, only that consistency can no longer be guaranteed.

---

## Domain Object

A Domain Object is the architectural representation of a business entity within the AcCore platform.

Domain Objects encapsulate business state, behavior and relationships while executing within the Runtime Environment.

A Domain Object is defined by Metadata and exists as a Runtime Object during execution.

---

## EAV (Entity-Attribute-Value)

A storage model used to persist user-defined fields without requiring schema modifications.

In AcCore, EAV is an implementation detail of the Storage subsystem and remains transparent to Runtime and Metadata.

---

## Information Register

A register that stores business information that does not represent accumulation.

Information Registers may be periodic or non-periodic and typically store facts such as exchange rates, prices, tax rates or configuration data.

---

## Interface

An Interface is a programming-language construct used to implement one or more architectural Contracts.

An Interface is an implementation detail.

The architecture specifies Contracts rather than language-specific interfaces.

---

## Logical Field

A field as perceived by Metadata and Runtime.

A Logical Field is independent of its physical persistence mechanism and may be stored in primary storage, EAV storage or future storage implementations.

---

## Logical Field Model

The architectural principle stating that Metadata and Runtime interact only with Logical Fields.

Storage is responsible for determining how fields are physically persisted.

Physical storage details remain hidden from Runtime.

---

## Metadata

**Category:** Foundation

**Status:** Stable

**Definition**

The declarative description of the structure and behavior of a business information system.

Metadata defines what a configuration contains rather than how the platform is implemented.

**See also**

- Configuration
- Runtime

---

## Metadata Field

A field defined by Metadata as part of a business object structure.

Metadata Fields specify field names, types, semantics, constraints and other properties required by the platform.

---

## Money

A Platform Type representing monetary values.

Money is always interpreted together with Currency metadata, which defines scale, precision and currency-specific rules.

---

## Movement

A business fact stored within an Accumulation Register.

A Movement represents a change applied to register resources and is the primary source of balances and turnovers.

Movements are generated during posting, validated according to register contracts, and persisted through Register Services.

A Movement may contain dimensions, resources, attributes, period information, and other register-specific data required by the target register.

---

## MovementChanged

A Register Event indicating that an existing movement has been modified.

## MovementCreated

A Register Event indicating that a new movement has been stored.

## MovementDeleted

A Register Event indicating that an existing movement has been removed.

## Movement Query

A Register Query that retrieves movements and answers the question:

"What happened?"

## Movement Service

A Register service responsible for storing, retrieving, and managing movements.

Movement Service provides the interface between Posting Architecture and register storage.

### MovementSet

A collection of movements generated during a single posting operation.

MovementSet is the primary output of a Posting Handler and serves as the input to movement validation and persistence processes.

---

## Movement Type

A movement classification defining the direction of resource change.

Supported movement types are:

INCOME
EXPENSE

Movement direction is determined exclusively by movement_type.

---

## Object Composition

Object Composition is the architectural process of assembling a Domain Object from its architectural components.

Object Composition combines Object Identity, Object Type, Object State, Object Behavior and Object Relationships into a coherent Runtime Object.

---

## Object Identity

Object Identity is the immutable architectural identity of a Domain Object.

Object Identity uniquely distinguishes one Domain Object from all other objects throughout its lifetime.

Object Identity remains stable regardless of changes to the object's state.

---

## Object Instance

An Object Instance is a concrete realization of a Metadata-defined Domain Object.

Every Runtime Object is an Object Instance of exactly one Metadata Object.

---

## Object Lifetime

Object Lifetime is the period during which a Runtime Object exists within the Runtime Environment.

Object Lifetime begins when the Runtime Object is created and ends when it is disposed.

---

## Object Reference

An Object Reference is the architectural relationship that allows one Domain Object to refer to another Domain Object.

Object References connect Domain Object identities while remaining independent of object ownership, persistence mechanisms and implementation details.

Object References are resolved by the Runtime during execution.

---

## Object State

Object State is the complete set of mutable values associated with a Runtime Object at a particular moment in time.

Object State changes during execution while Object Identity remains unchanged.

---

## Persistent Entity

A Storage Entity that possesses identity and participates in persistence lifecycle operations such as creation, update, versioning and deletion.

Catalogs, Documents, Registers, Constants and Sequences are Persistent Entities.

---

## Persistent Object

A Persistent Object is the storage representation of a Runtime Object.

Persistent Objects are optimized for durability and persistence rather than execution.

The mapping between Runtime Objects and Persistent Objects is defined by the Storage subsystem.

---

## Platform

**Category:** Foundation

**Status:** Stable

**Definition**

A software system that provides reusable capabilities for developing, executing, and maintaining business information systems.

**See also**

- Core
- Platform Capability
- Platform Edition
- Configuration

---

## Platform Capability

**Category:** Platform

**Status:** Stable

**Definition**

A reusable service provided by the platform and available to all configurations within a platform edition.

**See also**

- Capability
- Platform

---

## Platform Edition

**Category:** Platform

**Status:** Stable

**Definition**

A specific distribution of the AcCore platform that provides a defined set of platform capabilities while sharing the common architectural Core.

**See also**

- Platform
- Core
- Configuration

---

## Platform Type

A logical type defined by the AcCore Platform Type System.

Platform Types are independent of Storage Provider implementations and provide consistent behavior across the platform.

Examples include String, Integer, Boolean, Date, DateTime, Money, Quantity and Reference.

---

### Posting

The process of transforming a business object into register movements and applying its accounting effects to the system.

Posting is executed by the Posting Engine through Posting Handlers and results in validated and persisted movements.

---

### Posting Context

A controlled runtime environment provided to Posting Handlers during posting execution.

Posting Context provides access to the current document, metadata, runtime services, registers, queries, references, user information, session information, and platform time.

Posting Context acts as the integration boundary between posting logic and platform services.

---

## Posting Engine

The central orchestration component of the Posting Architecture.

The Posting Engine coordinates the posting lifecycle, resolves Posting Handlers, creates Posting Contexts, validates generated movements, coordinates persistence, updates totals, manages dependency integration, and publishes posting events.

The Posting Engine does not contain business-specific accounting logic.

Business logic is implemented by Posting Handlers.

Storage is responsible only for movement persistence and does not perform posting logic.

---

### Posting Handler

A component responsible for generating movements for a specific business object.

Posting Handlers contain business-specific posting logic and transform document data into a MovementSet.

Posting Handlers do not perform persistence, transaction management, totals updates, or dependency management.

---

## Published Artifact

A Published Artifact is an immutable architectural product that has successfully completed composition, validation and publication.

Published Artifacts serve as architectural contracts between platform subsystems.

Examples include:

- Published Semantic Metadata Graph;
- Published Runtime Service Graph;
- Published Runtime Context;
- Compiled Query Plan (future);
- Compiled Expression Plan (future).

---

## Quantity

A Platform Type representing measurable quantities.

Quantity values are interpreted together with Measure Unit metadata, which defines precision, scale and measurement rules.

---

## Query Service

A Register service responsible for executing register queries.

Query Service provides movement, balance, and turnover queries while hiding storage implementation details.

---

## Reference Cardinality

Reference Cardinality defines how many target Domain Objects may be associated with a single Reference Source.

Typical cardinalities include one-to-one, one-to-many and many-to-many relationships.

---

## Reference Integrity

Reference Integrity is the architectural guarantee that every valid Reference either resolves to an existing Domain Object or reports a well-defined resolution failure.

Reference Integrity is maintained across Runtime and Storage boundaries.

---

## Reference Model

The platform-wide mechanism used to represent relationships between business objects.

All references are based on ULID identities and remain independent of business numbers, names or physical storage identifiers.

---

## Reference Navigation

Reference Navigation is the Runtime process of traversing a Reference from its source Domain Object to its target Domain Object.

Navigation operates on Object References and is independent of persistence technology.

---

## Reference Resolution

Reference Resolution is the Runtime process of transforming a Reference into an accessible Runtime Object.

The Runtime determines how a Reference is resolved without exposing the underlying implementation mechanism.

---

## Reference Resolution Policy

A Reference Resolution Policy defines the Runtime strategy used to resolve Object References.

Resolution policies are implementation-independent and may include immediate, lazy or deferred resolution.

---

## Reference Source

A Reference Source is the Domain Object that owns a Reference.

The Reference Source establishes the architectural relationship to another Domain Object.

---

## Reference Target

A Reference Target is the Domain Object identified by a Reference.

The Reference Target is resolved by the Runtime using Object Identity.

---

## Register

A metadata-defined structure used to store and organize business facts.

Registers provide persistent storage, aggregation, querying, and dependency participation within the platform.

AcCore supports Information Registers and Accumulation Registers.

Information Register

A register type used to store informational business facts.

Information Registers support historical tracking, versioning, temporal queries, and source traceability.

Information Registers do not participate in accumulation.

Accumulation Register

A register type used to store accounting movements representing business facts.

Accumulation Registers are the source of balances and turnovers.

Balances and turnovers are derived from movements.

---

## Register Event

An infrastructure event describing changes in register facts or register state.

Register Events do not contain business logic.

---

## Register Lifecycle

The sequence of runtime stages through which a register progresses during its existence.

The lifecycle includes compilation, registration, initialization, operation, maintenance, and shutdown.

---

## Register Manager

A Runtime service responsible for registration, initialization, lifecycle management, and discovery of register definitions.

Register Manager manages register participation in the Runtime Architecture.

---

## Register Query

A request for register information executed through the Register Query Model.

Register Queries are independent of storage layout and aggregation implementation details.

---

## Register Record

A persistent fact stored within a register.

A register record may contain dimensions, resources, attributes, identity information, version information, and source information depending on the register type.

---

## Rebuild Service

A Register service responsible for maintenance operations including totals reconstruction, recovery, migration, and consistency verification.

---

## Register State

The current aggregated state of a register as exposed through register services.

Register State is the primary dependency unit used by the Dependency Graph.

---

## RegisterChanged

A Register Event indicating that the state of a register has changed.

This event serves as the primary integration point with the Dependency Graph.

---

### Register Posting Contract

A metadata-driven specification defining the requirements that movements must satisfy before they can be accepted by a register.

A Register Posting Contract may define required dimensions, resources, attributes, movement types, data types, and validation rules.

Register Posting Contracts form the integration boundary between Posting Architecture and Register Architecture.

---

### Reposting

The process of rebuilding accounting effects for an already posted object.

Reposting typically consists of removing existing movements and generating a new MovementSet based on the current object state.

Reposting is used to restore accounting consistency after modifications or dependency changes.

---

## Resolved Reference

A Resolved Reference is the Runtime result of a successful Reference Resolution.

A Resolved Reference provides access to the target Runtime Object while preserving the architectural semantics of the original Reference.

---

## Runtime

**Category:** Runtime

**Status:** Stable

**Definition**

The execution environment responsible for interpreting metadata and executing business functionality provided by configurations.

**See also**

- Metadata
- Platform

---

## Runtime Object

A Runtime Object is the executable instance of a Domain Object within the Runtime Environment.

Runtime Objects execute business behavior, maintain runtime state and interact with Runtime Services through published Service Contracts.

Runtime Objects are created according to Metadata definitions.

---

## Scalar Storage Entity

A Storage Entity that stores a single logical value rather than tabular data.

Examples include Constants and Sequences.

---

## Semantic Field

A Metadata Field associated with predefined platform meaning.

Semantic Fields allow Runtime and platform services to provide specialized behavior while remaining independent of physical storage.

Examples include CODE, BARCODE, EMAIL, PHONE and URL.

---

## Service Contract

A Service Contract is the published architectural specification of a Runtime Service.

A Service Contract defines:

- provided capabilities;
- supported operations;
- lifecycle expectations;
- dependency requirements;
- compatibility guarantees.

Service implementations may evolve without changing the published Service Contract.

---

## Standard Configuration

**Category:** Configuration

**Status:** Stable

**Definition**

The reference business solution delivered together with the platform to provide an out-of-the-box business information system.

The Standard Configuration uses only public platform capabilities.

**See also**

- Configuration
- Platform

---

## Storage Entity

The logical persistence representation of a business object inside the Storage subsystem.

Storage Entities define how objects participate in persistence independently of Runtime behavior.

---

## Storage Optimizer

A subsystem responsible for adaptive optimization of physical storage structures.

Examples include automatic totals granularity selection, adaptive indexing and future storage optimizations.

Storage Optimizer must preserve identical logical behavior.

---

## Storage Provider

A concrete implementation of the Storage subsystem.

Examples may include SQLite, PostgreSQL or future storage backends.

Storage Providers must preserve the logical behavior defined by the platform architecture.

---

## Table Storage Entity

A Storage Entity representing tabular business data.

Catalogs, Documents and Registers are examples of Table Storage Entities.

---

## Temporal Query

A query executed relative to a specified point in time.

Temporal Queries allow reconstruction of historical register state.

---

## Totals Engine

A Runtime subsystem responsible for maintaining aggregated register state derived from movements.

The Totals Engine manages balance calculation, totals storage, adaptive aggregation strategies, and totals rebuild operations.

The Totals Engine ensures consistency between movements and aggregated register state.

The Totals Engine does not perform posting, valuation, reporting, or business logic.

---

## Totals Bucket

An aggregated totals record representing accumulated resource changes for a specific period bucket and dimension set.

Totals Buckets are used by the Totals Engine to calculate balances.

---

## Totals Service

A Register service responsible for maintaining and accessing totals data.

Totals Service manages totals updates and adaptive aggregation strategies.

---

## TotalsUpdated

A Register Event indicating that register totals have been updated.

---

## TotalsRebuilt

A Register Event indicating that register totals have been rebuilt.

---

## Turnover

An aggregated representation of resource changes during a specified period.

Turnovers are derived from movements and may be materialized as a performance optimization.

---

## Turnover Query

A Register Query that retrieves aggregated resource changes and answers the question:

"What changed during a period?"

---

## ULID (Universally Unique Lexicographically Sortable Identifier)

The platform-wide identity format used by AcCore.

ULIDs provide globally unique object identities while preserving chronological ordering characteristics.

ULID values are independent of Storage Providers and business numbering systems.

---

## User-defined Field

A field introduced by configuration or end users to extend business objects without modifying platform architecture.

User-defined Fields are typically persisted through the EAV model and participate in the Logical Field Model.





## Valuation Architecture Terms

### Valuation

The process of determining, maintaining, adjusting, and reporting economic value associated with quantity-carrying business objects.

Valuation is independent from quantity accounting but operates on the same economic objects.

---

### Valuation Engine

A subsystem responsible for producing valuation results from valuation facts.

Responsibilities:

* layer processing;
* valuation method execution;
* adjustment processing;
* allocation processing;
* cost movement generation.

Valuation Engine does not maintain cost balances.

---

### Cost Totals Engine

A subsystem responsible for maintaining materialized valuation totals.

Responsibilities:

* cost balance maintenance;
* balance rebuilding;
* balance verification.

Input:

```text id="g1q9wa"
CostMovement
```

Output:

```text id="n3v7zb"
CostBalance
```

---

### Valuation Method

A strategy used to determine which valuation layers are consumed by a quantity consumption event.

Examples:

```text id="h5r2mt"
FIFO

LIFO

Weighted Average
```

Valuation methods produce valuation consumptions.

---

### Valuation Key

A dimensional identifier used by the valuation subsystem.

According to Valuation Architecture:

```text id="x6p8dk"
Valuation Key
=
Quantity Key
```

Valuation does not introduce independent dimensional models.

---

### Valuation Layer

A valuation fact representing ownership of quantity and associated value.

A valuation layer is the primary carrier of cost ownership.

A valuation layer may participate in:

* valuation consumptions;
* valuation adjustments.

---

### Valuation Consumption

A valuation fact representing explicit consumption of a valuation layer.

Valuation consumptions are produced by valuation methods.

Valuation consumption preserves valuation provenance and layer usage history.

---

### Valuation Adjustment

A valuation fact representing a change in layer valuation.

Examples:

* delayed cost;
* transportation cost;
* customs cost;
* supplier correction;
* revaluation.

All valuation corrections are represented through adjustments.

---

### Valuation Allocation

A valuation fact representing explicit distribution of a valuation adjustment.

Valuation allocations connect valuation adjustments with their targets.

Supported targets:

```text id="p8k4sv"
Consumption

Remaining Layer
```

---

### Cost Movement

A materialized valuation fact representing a change in economic value.

Cost movements are produced by the Valuation Engine.

Cost movements are the source of valuation totals.

---

### Cost Balance

A materialized valuation total representing accumulated economic value.

Cost balances are maintained by the Cost Totals Engine.

Cost balances are rebuildable from cost movements.

---

### Effective Cost

The effective value of a valuation layer after applying all adjustments.

Definition:

```text id="r4t6wy"
Effective Cost =
Base Cost +
Σ Adjustments
```

---

### Base Cost

The initial value assigned to a valuation layer at creation time.

Base cost may subsequently be modified through valuation adjustments.

---

### Delayed Cost

A valuation fact that becomes known after the associated quantity fact.

Delayed costs are represented through valuation adjustments.

Examples:

* transportation invoices;
* customs invoices;
* supplier corrections;
* post-factum expenses.

---

### Cost Provenance

The ability to trace the origin and evolution of valuation results.

Cost provenance is provided through:

```text id="v7m3ac"
ValuationLayer
        ↓
ValuationConsumption
        ↓
ValuationAdjustment
        ↓
ValuationAllocation
        ↓
CostMovement
```

---

### Valuation Facts

Immutable valuation history used as the source of truth.

Valuation facts include:

```text id="z2k8nr"
ValuationLayer

ValuationConsumption

ValuationAdjustment
```

These facts are sufficient to reconstruct valuation state.

---

### Materialized Valuation Artifacts

Derived valuation structures maintained for performance.

Artifacts include:

```text id="m5x1pd"
ValuationAllocation

CostMovement

CostBalance
```

Materialized artifacts are rebuildable.

---

### Valuation Rebuild

The process of reconstructing valuation state from valuation facts.

Rebuild operations may target:

* allocations;
* cost movements;
* cost balances;
* complete valuation state.

---

### Valuation Resource

An economic measure maintained by the valuation subsystem.

The standard valuation resource is:

```text id="d8w4ul"
Money
```

Future implementations may introduce additional valuation resources while preserving the same valuation model.

---

### Quantity-Cost Consistency

Architectural principle stating:

```text id="a6v9rb"
Everything That Has Quantity
Must Have Value
```

Valuation dimensions are inherited from quantity accounting dimensions.
