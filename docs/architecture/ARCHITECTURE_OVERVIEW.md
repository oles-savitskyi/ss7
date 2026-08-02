# AcCore Architecture Overview

**Status:** Draft

**Version:** 0.2

**Language:** English

---

# 1. Purpose

This document provides a high-level overview of the AcCore architecture.

Its purpose is to identify the major architectural subsystems of the platform, define their responsibilities, and describe their relationships.

Detailed designs of individual subsystems are described in dedicated architecture documents.

This document is normative.

---

# 2. Architectural Principles

The architecture of AcCore is derived from the System Model.

Every subsystem exists to realize one or more conceptual relationships defined by the System Model.

Business functionality belongs to Configurations.

Reusable functionality belongs to the Platform.

Architectural integrity takes precedence over implementation convenience.

Subsystem responsibilities must remain stable over time.

Architectural dependencies should be explicit and directional.

---

# 3. Architectural View

At the highest level, AcCore consists of a set of cooperating architectural subsystems.

```text
AcCore Platform

├── Metadata Architecture
├── Runtime Architecture
├── Object Architecture
├── Storage Architecture
├── Posting Architecture
├── Register Architecture (planned)
├── Reporting Architecture (planned)
├── Capability Architecture
├── User Interface Architecture
├── Processing Architecture
└── Development Architecture
```

Each subsystem has a clearly defined responsibility and communicates through well-defined architectural interfaces.

---

# 4. Core Architectural Flow

The primary business execution flow of the platform is organized around the following architectural chain:

```text
Metadata
    ↓
Runtime
    ↓
Business Objects
    ↓
Posting
    ↓
Registers
    ↓
Reports
```

Conceptually:

* Metadata defines the business model.
* Runtime interprets metadata.
* Business Objects represent business state and behavior.
* Posting transforms business objects into accounting movements.
* Registers store accounting facts.
* Reports consume register data and present business information.

This flow represents the core accounting lifecycle of the platform.

---

# 5. Architectural Subsystems

## 5.1 Metadata Architecture

Responsible for defining, storing, validating, compiling, and managing metadata.

Metadata provides the declarative description of business systems.

Metadata serves as the foundation for all higher-level architectural subsystems.

---

## 5.2 Runtime Architecture

Responsible for interpreting metadata and executing platform behavior.

The Runtime Architecture provides execution environments, runtime services, contexts, and system pipelines.

Runtime serves as the operational foundation of the platform.

---

## 5.3 Object Architecture

Responsible for business object identity, references, lifecycle, state management, behavior, and object creation.

Object Architecture defines how business entities are represented and manipulated at runtime.

Business Objects form the primary business layer of the platform.

---

## 5.4 Storage Architecture

Responsible for persistent data management.

Storage Architecture defines how business data, metadata, documents, movements, and register data are stored and retrieved.

Storage mechanisms remain implementation details behind architectural abstractions.

---

## 5.5 Posting Architecture

Responsible for transforming business objects into accounting movements.

Posting Architecture defines:

* posting lifecycle;
* posting execution model;
* posting handlers;
* posting context;
* movement generation;
* movement validation;
* register posting contracts;
* posting dependencies;
* posting events.

Posting Architecture forms the integration boundary between Object Architecture and Register Architecture.

---

## 5.6 Register Architecture (Planned)

Responsible for managing accounting registers and register operations.

Register Architecture will define:

* register models;
* register storage structures;
* totals calculation;
* balances;
* turnovers;
* register querying.

Registers represent the accounting facts of the system.

---

## 5.7 Reporting Architecture (Planned)

Responsible for transforming accounting and business data into analytical information.

Reporting Architecture will provide reporting models, report execution, report composition, and analytical processing.

Reports represent the primary information consumption layer of the platform.

---

## 5.8 Capability Architecture

Responsible for organizing reusable platform capabilities.

Capabilities expose reusable functionality to configurations while remaining independent of business domains.

Capability Architecture complements Runtime Architecture and may evolve as platform services mature.

---

## 5.9 User Interface Architecture

Responsible for presenting business functionality to users.

The user interface remains independent of business logic, metadata storage, and persistence implementation details.

---

## 5.10 Processing Architecture

Responsible for executing configurable business operations, workflows, automation procedures, and platform processes.

Processing mechanisms remain independent of individual business domains.

---

## 5.11 Development Architecture

Responsible for tools supporting development, testing, debugging, packaging, deployment, and maintenance of configurations.

Development Architecture supports the platform lifecycle rather than runtime business execution.

---

# 6. Architectural Dependencies

Architectural dependencies should always point toward more fundamental layers.

The core dependency chain is:

```text
Metadata
    ↓
Runtime
    ↓
Objects
    ↓
Posting
    ↓
Registers
    ↓
Reports
```

Supporting subsystems interact with multiple architectural layers while preserving conceptual independence.

Examples:

* User Interface interacts with Runtime, Objects, Registers, and Reports.
* Processing interacts with Runtime, Objects, Posting, and Registers.
* Development interacts with all architectural subsystems.

Subsystems should remain as independent as possible.

---

# 7. Evolution Strategy

New platform functionality should normally be introduced by extending existing architectural subsystems.

Creation of new subsystems requires architectural justification.

Architectural responsibilities should remain stable throughout the lifetime of the platform.

Subsystem boundaries should evolve more slowly than implementations.

---

# 8. Architecture Documentation

Each architectural subsystem is documented separately.

Current architecture documentation includes:

* Architecture Foundation
* Metadata Architecture
* Runtime Architecture
* Object Architecture
* Storage Architecture
* Posting Architecture

Planned architecture documentation includes:

* Register Architecture
* Reporting Architecture
* Capability Architecture
* User Interface Architecture
* Processing Architecture
* Development Architecture

Additional documents may be introduced as the platform evolves.

---

# 9. Architectural Integrity

Subsystem boundaries define responsibilities rather than implementation units.

Implementation technologies may evolve independently without changing subsystem responsibilities.

Architectural consistency is considered more important than minimizing the number of subsystems.

Cross-subsystem interactions should occur through explicit architectural contracts.

---

# 10. Final Principle

The architecture of AcCore is organized as a composition of independent, cooperating subsystems.

Each subsystem has a primary responsibility and a clearly defined architectural boundary.

Together these subsystems realize the AcCore System Model while preserving platform integrity, extensibility, maintainability, and long-term architectural consistency.
