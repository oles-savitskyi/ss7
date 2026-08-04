# AcCore Architecture Overview

**Status:** Draft

**Version:** 0.3

**Language:** English

---

# 1. Purpose

This document provides a high-level overview of the AcCore architecture.

Its purpose is to identify the major architectural subsystems of the platform, define their responsibilities, and describe the relationships between them.

Detailed designs of individual subsystems are described in dedicated architecture documents.

This document is normative.

---

# 2. Architectural Principles

The architecture of AcCore is derived from the System Model.

Every architectural subsystem exists to realize one or more conceptual relationships defined by the System Model.

Business functionality belongs to Configurations.

Reusable functionality belongs to the Platform.

Architectural integrity takes precedence over implementation convenience.

Subsystem boundaries define responsibilities rather than implementation units.

---

# 3. Architectural Vision

AcCore is a metadata-driven platform for storing, transforming, aggregating, and analyzing business facts.

The platform is built around a continuous flow:

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
Future Valuation
↓
Future Reporting

Each architectural subsystem contributes to a specific stage of this flow.

---

# 4. Architectural View

At the highest level, AcCore consists of cooperating architectural subsystems.

```
                 AcCore Platform
```

┌─────────────────────────────────────────────┐
│          Architecture Foundation            │
└─────────────────────────────────────────────┘

┌─────────────┬─────────────┬─────────────────┐
│  Metadata   │   Runtime   │     Storage     │
│Architecture │Architecture │  Architecture   │
└─────────────┴─────────────┴─────────────────┘
│              │              │
└──────────────┼──────────────┘
│
Object Architecture
│
▼
Posting Architecture
│
▼
Register Architecture

Each subsystem has a clearly defined responsibility and communicates through well-defined architectural contracts.

---

# 5. Architectural Subsystems

## 5.1 Metadata Architecture

Responsible for defining, storing, validating, compiling, and managing metadata.

Metadata Architecture provides the declarative description of business systems.

Metadata is the source of truth for platform structure and behavior.

---

## 5.2 Runtime Architecture

Responsible for executing platform functionality and managing runtime services.

Runtime Architecture provides service orchestration, dependency management, lifecycle management, and execution infrastructure.

---

## 5.3 Object Architecture

Responsible for transforming metadata definitions into runtime business objects.

Object Architecture defines identity, references, state management, factories, and runtime behavior.

Objects provide the operational representation of business entities.

---

## 5.4 Storage Architecture

Responsible for persistent storage of platform data.

Storage Architecture defines storage models, identity persistence, physical structures, and storage abstractions.

Storage mechanisms remain independent from business logic.

---

## 5.5 Posting Architecture

Responsible for transforming business documents into register movements.

Posting Architecture defines posting lifecycle, movement generation, posting handlers, posting dependencies, posting context, and posting orchestration.

Posting Architecture does not perform storage operations directly.

---

## 5.6 Register Architecture

Responsible for storing, aggregating, querying, and propagating business facts.

Register Architecture defines:

* Information Registers;
* Accumulation Registers;
* Movement Storage;
* Totals Engine;
* Query Services;
* Register Events;
* Dependency Integration;
* Register Lifecycle.

Register Architecture provides the primary fact storage and aggregation model of the platform.

---

# 6. Architectural Dependencies

Architectural dependencies should always point toward more fundamental layers.

Metadata
↓
Runtime
↓
Object
↓
Posting
↓
Registers
↓
Storage

Cross-subsystem interactions must occur through explicit architectural contracts.

Dependency Graph integration provides controlled propagation of changes across subsystems.

---

# 7. Architectural Data Flow

The primary architectural flow of AcCore is:

Metadata
↓
Runtime Definitions
↓
Business Objects
↓
Business Documents
↓
Posting
↓
Register Movements
↓
Register Aggregates
↓
Queries and Analysis

This flow represents the core information processing model of the platform.

---

# 8. Evolution Strategy

New platform functionality should normally be introduced by extending existing architectural subsystems.

Creation of new architectural subsystems requires architectural justification.

Architectural responsibilities should remain stable over the lifetime of the platform.

Future architectural extensions should integrate with the existing data flow and dependency model.

---

# 9. Future Architecture

The following architectural subsystems are planned:

* Valuation Architecture
* Reporting Architecture
* Processing Architecture
* User Interface Architecture
* Development Architecture
* Capability Architecture

Future subsystems must integrate through established architectural contracts and dependency mechanisms.

---

# 10. Architectural Integrity

Architectural consistency is considered more important than minimizing the number of subsystems.

Subsystems should remain independently evolvable whenever possible.

Implementation technologies may change without affecting architectural responsibilities.

Business logic must remain separated from platform infrastructure.

---

# 11. Final Principle

AcCore is a metadata-driven platform organized as a composition of independent, cooperating architectural subsystems.

Each subsystem has a clearly defined responsibility.

Together these subsystems provide a foundation for storing, transforming, aggregating, valuating, and analyzing business facts while preserving long-term architectural consistency.
