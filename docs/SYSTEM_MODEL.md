# SS7 System Model

**Status:** Draft

**Version:** 0.1

**Language:** English

---

# 1. Purpose

This document defines the conceptual system model of the SS7 platform.

Its purpose is to describe the relationships between the fundamental concepts defined by the SS7 Glossary and Conceptual Model.

The System Model is independent of implementation technologies and serves as the foundation for the platform architecture.

This document is normative.

---

# 2. Principles

The SS7 System Model is based on the following principles.

* The model describes concepts rather than implementations.
* Relationships are more important than implementation details.
* Every architectural component shall realize one or more relationships defined by this model.
* Business functionality is separated from platform functionality.
* The model should remain stable throughout the evolution of the platform.

---

# 3. Fundamental Entities

The system consists of the following fundamental entities.

* Platform
* Core
* Platform Edition
* Platform Capability
* Configuration
* Standard Configuration
* Metadata
* Runtime
* Development Environment
* Business Process

These entities are defined in the SS7 Glossary.

---

# 4. Fundamental Relationships

## 4.1 Platform Composition

The Platform contains:

* Core
* Development Environment
* Platform Editions

The Platform provides Platform Capabilities.

---

## 4.2 Core

The Core defines the common architectural foundation shared by every Platform Edition.

Every Platform Edition contains the same Core.

---

## 4.3 Platform Editions

A Platform Edition exposes a defined set of Platform Capabilities.

Platform Editions differ only by the capabilities they provide.

---

## 4.4 Configurations

A Configuration is developed for a specific Platform Edition.

A Configuration:

* defines Business Processes;
* defines Metadata;
* uses Platform Capabilities.

A Configuration never modifies the Platform.

---

## 4.5 Standard Configuration

The Standard Configuration is a Configuration supplied together with the Platform.

It uses only public Platform Capabilities.

---

## 4.6 Metadata

Metadata describes the structure and behavior of a Configuration.

Metadata is interpreted by the Runtime.

---

## 4.7 Runtime

The Runtime executes the behavior described by Metadata.

The Runtime remains independent of any specific business domain.

---

## 4.8 Development Environment

The Development Environment supports the creation, testing, maintenance, and deployment of Configurations.

---

# 5. Relationship Model

The conceptual relationships between the entities are summarized below.


Platform
│
├── contains ───────────────► Core
│
├── contains ───────────────► Development Environment
│
├── distributes ────────────► Platform Editions
│
└── provides ───────────────► Platform Capabilities
                                      ▲
                                      │
                         Configuration uses
                                      │
Configuration ─────── defines ───────► Business Processes
        │
        └──────────── defines ───────► Metadata
                                              │
                                              ▼
                                          Runtime executes


---

# 6. Layered Model

The conceptual organization of SS7 consists of four layers.


Business Layer
        │
        ▼
Configuration Layer
        │
        ▼
Platform Capability Layer
        │
        ▼
Core Layer


Responsibilities belong to the lowest layer capable of fulfilling them.

Business-specific behavior belongs to Configurations.

Reusable functionality belongs to Platform Capabilities.

Fundamental architectural responsibilities belong to the Core.

---

# 7. Evolution Rules

The system evolves according to the following rules.

New business requirements should first be implemented within Configurations.

If a responsibility becomes reusable across multiple Configurations, it may be promoted to a Platform Capability.

Changes to the Core require architectural justification and should remain exceptional.

Platform Editions evolve by extending available Platform Capabilities without modifying the Core.

---

# 8. Architectural Consequences

The System Model defines the conceptual responsibilities of the platform.

The architecture of SS7 shall realize this model without changing its semantics.

Implementation technologies may evolve, but the conceptual relationships defined by this document should remain stable.

---

# 9. Final Principle

The architecture of SS7 is derived from the System Model.

Implementation follows architecture.

Architecture follows the System Model.

The System Model follows the conceptual language of the platform.
