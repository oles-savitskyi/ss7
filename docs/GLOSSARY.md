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

## Reporting Architecture

A subsystem responsible for transforming business data, register data, and valuation data into analytical datasets and user-consumable information.

Reporting Architecture includes metadata definitions, runtime execution, dataset generation, and presentation models.

---

## Report

A metadata-defined analytical object that describes how analytical information should be obtained, processed, and presented.

A report does not store analytical results.

---

## Report Definition

A metadata object that defines report structure, data sources, dimensions, measures, filters, parameters, and presentation settings.

---

## Data Source

A metadata-defined provider of analytical data used by reports.

Data Sources abstract report execution from storage and runtime implementation details.

---

## Data Source Provider

A runtime component responsible for retrieving datasets from a specific source type.

---

## Dataset

A platform-neutral analytical data structure produced by report execution.

Datasets form the architectural boundary between Reporting Runtime and Presentation Layer.

---

## Dataset Definition

A metadata description that defines the structure of a report dataset.

A Dataset Definition specifies:

* Data Sources
* Dimensions
* Measures
* Filters
* Parameters
* Ordering Rules

---

## Dimension

An analytical axis used to classify, group, filter, and navigate business facts.

Examples include Customer, Product, Warehouse, Period, Region, and Department.

Dimensions answer the question:

> What are we analyzing by?

---

## Measure

A numerical value used to quantify business facts.

Examples include Quantity, Amount, Cost, Profit, and Margin.

Measures answer the question:

> What are we measuring?

---

## Base Measure

A measure directly obtained from source data without additional calculations.

---

## Calculated Measure

A measure derived from one or more measures through analytical expressions.

Calculated Measures are evaluated after aggregation.

---

## Dimension Hierarchy

A metadata-defined hierarchy that organizes dimension values into analytical navigation levels.

Examples:

* Year → Quarter → Month → Day
* Region → City → Customer

---

## Report Parameter

A runtime value supplied during report execution and used to influence filtering, grouping, calculations, or data acquisition.

---

## Report Compiler

A runtime component that transforms report metadata into compiled runtime structures.

---

## Compiled Report

A runtime representation of a report definition produced by the Report Compiler.

Compiled Reports are independent from metadata storage.

---

## Execution Plan

A runtime structure describing the sequence of operations required to produce a report dataset.

Typical operations include filtering, grouping, aggregation, calculation, and sorting.

---

## Execution Plan Builder

A runtime component responsible for creating execution plans from compiled reports.

---

## Report Executor

A runtime component responsible for executing report execution plans and producing datasets.

---

## Report Manager

The primary runtime entry point for report execution requests.

The Report Manager coordinates report validation, compilation, planning, and execution.

---

## Data Source Manager

A runtime component responsible for resolving data source providers and acquiring datasets.

---

## Report Runtime

The runtime subsystem responsible for transforming report metadata into analytical datasets.

Report Runtime does not perform presentation or export operations.

---

## Presentation Layer

A subsystem responsible for transforming datasets into user-consumable representations.

Presentation is independent from report execution.

---

## Presentation Model

A metadata structure describing how a dataset should be displayed.

Presentation Models are independent from rendering technologies.

---

## Presentation Renderer

A component responsible for transforming presentation definitions into technology-specific outputs.

Examples include Qt renderers, web renderers, Excel renderers, and PDF renderers.

---

## Tabular Presentation

A presentation type that displays datasets as rows and columns.

---

## Pivot Presentation

A presentation type that displays datasets using dimensions and measures arranged in analytical matrices.

---

## Chart Presentation

A presentation type that visualizes datasets using graphical representations.

---

## Dashboard Presentation

A presentation type that combines multiple analytical views into a unified interface.

---

## Export Presentation

A presentation type that generates portable outputs such as Excel, PDF, CSV, or JSON.

---

## Dataset Cache

A runtime cache containing previously generated datasets.

Dataset Caching is an optimization mechanism and does not affect report semantics.

---

## Drill-Down

An analytical navigation operation that moves from aggregated information to more detailed information.

Drill-Down may use Dimension Hierarchies or report-specific navigation paths.

---

## Roll-Up

An analytical navigation operation that moves from detailed information to higher aggregation levels.

---

## Analytical Dataset

A dataset intended for analytical processing, aggregation, visualization, or decision support.

---

## Analytical Model

The combination of Dimensions and Measures used to describe and analyze business facts.

---

## Renderer Independence

An architectural principle stating that presentation definitions must remain independent from rendering technologies.

---

## Dataset/Presentation Separation

An architectural principle stating that report execution produces datasets while presentation consumes datasets.

Neither layer depends on the internal implementation details of the other.


## API Architecture

A subsystem responsible for publishing Integration Contracts through external communication protocols while preserving business and runtime boundaries.

---

### API Publication Layer

A runtime layer that exposes Integration Contracts through protocol-specific representations such as REST, gRPC, WebSocket, or messaging systems.

---

### Command API

An API endpoint or interface used to execute state-changing business operations through Integration Contracts.

---

### Query API

An API endpoint or interface used to retrieve information without modifying platform state.

---

### Dataset API

An API interface that exposes Reporting Datasets to external consumers.

---

### Event API

An API interface used to publish or consume Integration Events.

---

### Integration Contract

A versioned definition of a business interaction exposed by the platform.

Contracts define structure, semantics, validation rules, and versioning independently from transport protocols.

---

### Event Architecture

A subsystem responsible for publishing, transporting, and consuming business events generated by the platform.

---

### Event

An immutable representation of a completed business fact.

Events describe what has happened and never represent commands or requested actions.

---

### Event Contract

A versioned contract that defines the structure and semantics of a published event.

---

### Event Publisher

A runtime component responsible for creating and publishing events into Event Runtime.

---

### Event Runtime

A runtime subsystem responsible for event registration, routing, filtering, dispatching, and delivery coordination.

---

### Event Manager

The primary runtime service responsible for event publication and subscription management.

---

### Subscriber

A component that consumes events published through Event Runtime.

Subscribers are independent from event publishers.

---

### Event-Aware Architecture

An architectural model in which events are generated from completed business facts and serve as mechanisms for observation, integration, notification, and extension.

Events do not drive core business execution.

---

### Import Architecture

A subsystem responsible for importing information into the platform through Integration Contracts and Runtime Services.

---

### Export Architecture

A subsystem responsible for publishing platform information through Integration Contracts and transport formats.

---

### Import Contract

A contract that defines the structure, validation rules, and processing semantics of imported information.

---

### Export Contract

A contract that defines the structure, projection rules, and delivery semantics of exported information.

---

### ImportExport Runtime

A runtime subsystem responsible for executing import and export operations.

Responsibilities include validation, transformation, mapping, execution, and serialization.

---

### Mapping Definition

A metadata object that defines how external structures are mapped to internal contract structures.

---

### Transformation Definition

A metadata object that defines deterministic conversion rules applied during import or export processing.

---

### File Format

A transport representation used for moving information between systems.

Examples include CSV, Excel, JSON, XML, and ZIP packages.

File formats do not define business semantics.

---

### Connector Framework

A subsystem responsible for integrating external systems with AcCore through Integration Contracts and Runtime Services.

---

### External Connector

A runtime component that adapts an external system to AcCore integration mechanisms.

Connectors do not contain business logic.

---

### Connector Runtime

A runtime environment responsible for connector lifecycle management and execution.

---

### Connector Manager

A runtime service responsible for connector registration, discovery, activation, monitoring, and shutdown.

---

### Connector Definition

A metadata object that describes a connector type and its runtime characteristics.

---

### Connector Configuration

A metadata object containing connector-specific settings such as endpoints, credentials, mappings, and synchronization policies.

---

### Application Connector

A connector used to integrate external business applications such as ERP, CRM, HRMS, or e-commerce systems.

---

### Service Connector

A connector used to integrate external services such as payment providers, tax services, currency services, email services, or SMS services.

---

### Messaging Connector

A connector used to integrate external messaging infrastructure and event delivery systems.

---

### Dataset Connector

A connector used to expose Reporting Datasets to external analytical consumers.

---

### Synchronization Connector

A connector used to synchronize information between AcCore and external systems.

---

### Contract-First Integration

An integration approach in which business contracts are defined before communication protocols, file formats, or connector implementations.

Contracts are the primary integration artifact.

---

### Protocol Independence

An architectural principle stating that business contracts remain independent from communication protocols and transport technologies.

---

### Format Independence

An architectural principle stating that business semantics remain independent from file formats and transport representations.

---

### Runtime-Mediated Integration

An architectural principle stating that all external interactions must pass through Runtime Services rather than directly accessing storage or internal structures.

## Security Architecture

### Authentication
Process of verifying identity.

### Authorization
Process of determining whether an authenticated principal may perform an operation.

### Principal
Runtime representation of an authenticated identity.

### Role
Collection of permissions assigned to users.

### Permission
Authorization unit representing an allowed operation on a security object.

### Security Object
Metadata-based protected resource participating in authorization.

### Constraint
Contextual restriction applied to a permission.

### Session
Authenticated runtime context associated with a principal.

### Audit Event
Immutable record describing a security-relevant or business-relevant action.

### Audit Trail
Append-only collection of audit events.

### Security Policy
Platform-wide mandatory security rule.

### Service Account
Non-human identity used by integrations and background processes.

### Default Deny
Security principle that denies access unless explicitly granted.

### Least Privilege
Security principle granting only required permissions.

### Fail Closed
Security principle that denies access when security evaluation cannot be completed.

## Workflow
Metadata-driven process coordinating lifecycle of business objects.

### Workflow Definition
Metadata description of states, transitions, approvals and automation rules.

### Workflow Instance
Runtime execution of a workflow definition.

### State
Business lifecycle stage of a workflow-controlled object.

### Transition
Allowed movement between workflow states.

### Approval Rule
Rule defining approval requirements for a transition.

### Task
Workflow-generated unit of work assigned to a user or role.

### Automation Rule
Metadata-defined action automatically executed by Workflow Runtime.

### Workflow Engine
Runtime component coordinating workflow execution.

### Workflow History
Historical record of workflow transitions and decisions.

### Business State
Domain-specific lifecycle state such as Draft, Approved or Posted.

### Lifecycle State
Runtime execution state such as Active, Waiting Approval or Completed.

### Workflow Context
Runtime context used during workflow execution.

## Configuration
Metadata-based business application built on top of the AcCore platform.

### Configuration Version
Versioned release of a configuration.

### Configuration Package
Deployable package containing a configuration.

### Extension
Metadata-based customization applied to a configuration.

### Extension Version
Versioned release of an extension.

### Metadata Module
Logical grouping of related metadata definitions.

### Metadata Composition
Process of assembling metadata from multiple layers.

### Metadata Composer
Runtime component responsible for metadata assembly.

### Runtime Metadata Model
Unified metadata model used by Runtime Architecture.

### Configuration Manager
Runtime component coordinating configuration lifecycle operations.

### Extension Manager
Runtime component managing extension lifecycle.

### Package Manager
Runtime component managing configuration and extension packages.

### Configuration Registry
Runtime registry exposing active configurations and metadata.

### Configuration Activation
Process of publishing a validated Runtime Metadata Model.

### Configuration Upgrade
Replacement of an active configuration version by a newer version.

### Configuration Lifecycle
Lifecycle governing creation, deployment, activation, upgrade, and retirement of configurations.

## Standard Configuration

A predefined business application built on top of the AcCore platform.

The Standard Configuration provides a complete SMB-oriented accounting and business management solution including reference data, documents, workflows, reporting, and security configuration.

---

### Continuous Cost Recognition

An accounting principle stating that business costs should be recognized and allocated as soon as the underlying business event occurs.

The principle applies to labor, depreciation, materials, services, and other business resources.

Period closing serves as a fallback mechanism rather than the primary recognition mechanism.

---

### Economic Object

The final business object that receives costs.

Examples include:

* purchased goods;
* produced products;
* sold products;
* services;
* other business assets.

Cost allocation ultimately targets Economic Objects.

---

### Direct Expense

An expense whose final cost receiver is known at the moment of recognition.

Direct expenses do not require cross-document allocation.

Examples:

* material consumed by a specific production order;
* labor assigned directly to a specific product.

---

### Related Expense

An expense whose final cost receiver is not fully known at the moment of recognition.

Related expenses are allocated through one or more allocation stages before reaching Economic Objects.

Examples:

* shared labor costs;
* shared depreciation;
* transportation expenses;
* administrative costs.

---

### Unallocated Cost

A recognized cost that has not yet been assigned to a specific Economic Object.

Unallocated costs may later be allocated operationally or recognized through period closing procedures.

---

### Salary Booking

The process that continuously recognizes labor quantities and labor costs.

Salary Booking creates labor facts independently from payroll taxation and payroll reporting.

---

### Salary Sharing

The process that allocates recognized labor costs to business documents and Economic Objects.

---

### Salary Taxation

The process that creates employee deductions and payroll tax liabilities.

Salary Taxation is independent from labor recognition and labor allocation.

---

### Salary Rollout

A consolidated payroll statement containing accruals, deductions, taxes, and other payroll information.

Salary Rollout does not create register movements.

---

### Depreciation Booking

The process that continuously recognizes asset utilization and corresponding depreciation costs.

---

### Depreciation Sharing

The process that allocates depreciation costs to business documents and Economic Objects.

---

### Depreciation Rate Plan

A time-dependent reference document defining planned hourly depreciation rates for assets.

---

### Bill To Pay

A planned or intended payment associated with a business transaction.

Bill To Pay does not create register movements and does not represent a financial fact.

Actual payment is recorded only through Cash documents.

---

### Resource Register

A register that records quantitative movements of inventory and other economic resources.

Resource Register stores quantities only and does not store costs.

---

### Labor Register

A register that records labor quantities recognized through Salary Booking.

Labor costs are maintained by the Valuation Engine.

---

### Asset Utilization Register

A register that records quantitative asset utilization recognized through Depreciation Booking.

Depreciation costs are maintained by the Valuation Engine.

---

### Settlement Register

A register that records receivables, payables, payroll liabilities, and tax liabilities.

Settlement Register stores obligations and claims rather than quantities.

---

### Cash Register

A register that records actual cash and bank movements.

Cash Register is the authoritative source of payment facts.

---

### Access Mode

A permission level assigned to a business object.

The Standard Configuration defines:

* View;
* Execute;
* Administer.

---

### Data Scope

A security restriction limiting access to a subset of business data.

Examples:

* departments;
* employee groups;
* financial accounts;
* business partner categories.

---

### Object Scope

A security restriction limiting access to a specific part of a business object.

Examples:

* document tabs;
* document sections;
* catalog folders.
