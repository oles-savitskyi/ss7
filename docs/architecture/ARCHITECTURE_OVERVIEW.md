# ARCHITECTURE_OVERVIEW.md

## Purpose

This document provides a high-level overview of the AcCoreD architecture.

It describes the major architectural subsystems, their responsibilities, and relationships.

Detailed implementation rules are defined in dedicated architecture documents.

---

# Architecture Vision

AcCoreD (Accounting Core Development) is a metadata-driven accounting and business application platform.

The platform is designed to support:

* accounting systems;
* ERP systems;
* CRM systems;
* HRMS systems;
* inventory management systems;
* industry-specific business solutions.

The architecture prioritizes:

* metadata-driven configuration;
* extensibility;
* auditability;
* deterministic processing;
* storage independence;
* UI independence.

---

# Architectural Baseline

Current architecture baseline:

```text id="ac23b1"
architecture-core-2.3
```

Architecture status:

```text id="ac23b2"
Foundation Complete

Metadata Architecture Complete

Runtime Architecture Complete

Object Architecture Complete

Storage Architecture Complete

Posting Architecture Complete

Register Architecture Complete

Valuation Architecture Complete
```

---

# Architectural Layers

The AcCoreD platform is organized into the following architectural layers.

```text id="ac23b3"
Metadata Layer
        ↓
Runtime Layer
        ↓
Object Layer
        ↓
Storage Layer
        ↓
Posting Layer
        ↓
Register Layer
        ↓
Valuation Layer
        ↓
Reporting Layer
```

Each layer builds on services provided by lower layers.

---

# Architecture Map

```text id="ac23b4"
Metadata
        ↓
Runtime
        ↓
Objects
        ↓
Storage
        ↓
Posting
        ↓
Registers
        ↓
Valuation
        ↓
Reporting
```

---

# Core Architectural Subsystems

## 1. Metadata Architecture

Defines application structure using metadata.

Responsibilities:

* metadata model;
* metadata compilation;
* metadata validation;
* metadata references;
* metadata semantics.

---

## 2. Runtime Architecture

Provides execution infrastructure.

Responsibilities:

* lifecycle management;
* service management;
* dependency resolution;
* execution context;
* runtime services.

---

## 3. Object Architecture

Provides business object model.

Responsibilities:

* catalogs;
* documents;
* business objects;
* object lifecycle;
* object services.

---

## 4. Storage Architecture

Provides persistent data storage.

Responsibilities:

* storage model;
* document storage;
* register storage;
* totals storage;
* persistence infrastructure.

Storage Model:

```text id="ac23b5"
Hybrid Storage Model
```

Identity Model:

```text id="ac23b6"
ULID
```

---

## 5. Posting Architecture

Transforms business events into accounting facts.

Responsibilities:

* posting lifecycle;
* posting handlers;
* posting context;
* posting dependencies;
* movement generation.

Output:

```text id="ac23b7"
Register Movements
```

---

## 6. Register Architecture

Provides quantity and state accounting.

Responsibilities:

* information registers;
* accumulation registers;
* totals engine;
* register query model;
* register dependencies.

Core Artifacts:

```text id="ac23b8"
Register Movement

Register Totals
```

---

## 7. Valuation Architecture

Provides cost accounting and valuation processing.

Valuation Architecture is independent from quantity accounting while operating on the same economic objects.

Responsibilities:

* valuation layers;
* valuation methods;
* valuation adjustments;
* valuation allocations;
* cost movements;
* cost balances;
* valuation rebuild and recovery.

Core Principles:

```text id="ac23b9"
Quantity Is Independent From Cost

Cost Facts May Arrive After Quantity Facts

Cost Is Produced By Valuation Engine

Everything That Has Quantity Must Have Value
```

Core Artifacts:

```text id="ac23c0"
Valuation Layer

Valuation Consumption

Valuation Adjustment

Valuation Allocation

Cost Movement

Cost Balance
```

Processing Model:

```text id="ac23c1"
Valuation Engine
        ↓
Cost Movement

Cost Totals Engine
        ↓
Cost Balance
```

---

## 8. Reporting Architecture

Status:

```text id="ac23c2"
Planned
```

Responsibilities:

* analytical queries;
* reporting model;
* report execution;
* report aggregation;
* presentation models.

---

# Cross-Cutting Architectural Principles

The following principles apply to all subsystems:

1. Metadata-driven behavior.

2. Deterministic processing.

3. Explicit facts.

4. Reproducible results.

5. Auditability.

6. Separation of concerns.

7. Storage independence.

8. UI independence.

9. Extensibility through metadata.

10. Incremental evolution.

---

# Current Architecture Status

Completed architectural stages:

```text id="ac23c3"
Architecture Foundation

Metadata Architecture

Runtime Architecture

Object Architecture

Storage Architecture

Posting Architecture

Register Architecture

Valuation Architecture
```

Planned architectural stages:

```text id="ac23c4"
Reporting Architecture

Integration Architecture

Security Architecture

Deployment Architecture
```

---

# Architecture Maturity

Current maturity estimate:

```text id="ac23c5"
≈ 9.7 / 10
```

Current status:

```text id="ac23c6"
READY FOR NEXT ARCHITECTURAL STAGE
```
