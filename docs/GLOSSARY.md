# SS7 Glossary

**Status:** Draft

**Version:** 0.1

**Language:** English

---

# 1. Purpose

This document defines the official terminology of the SS7 platform.

Its purpose is to establish a consistent vocabulary for all architectural, engineering, and user documentation.

Every architectural term used within the SS7 project shall have a single normative definition.

This document is normative.

---

# 2. Scope

This glossary defines concepts that belong specifically to the SS7 platform.

General software engineering terminology and implementation technologies are outside the scope of this document unless they acquire a specific meaning within SS7.

---

# 3. Conventions

Definitions describe concepts rather than implementations.

Definitions should remain stable even if implementation technologies change.

Each architectural term shall have exactly one normative definition.

Documents shall use terminology consistently with this glossary.

Terms are listed in alphabetical order.

---

# 4. Terms

## Architecture

**Category:** Foundation

**Status:** Stable

**Definition**

The fundamental organization of the SS7 platform, including its concepts, principles, components, relationships, and evolution.

**See also**

- Core
- Platform

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

The common architectural foundation shared by every SS7 platform edition.

**See also**

- Platform
- Platform Edition

---

## Development Environment

**Category:** Platform

**Status:** Stable

**Definition**

The set of tools used to create, maintain, test, and deploy SS7 configurations.

**See also**

- Configuration
- Platform

---

## Domain Object

A Domain Object is the architectural representation of a business entity within the SS7 platform.

Domain Objects encapsulate business state, behavior and relationships while executing within the Runtime Environment.

A Domain Object is defined by Metadata and exists as a Runtime Object during execution.

---

## Interface

An Interface is a programming-language construct used to implement one or more architectural Contracts.

An Interface is an implementation detail.

The architecture specifies Contracts rather than language-specific interfaces.

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

A specific distribution of the SS7 platform that provides a defined set of platform capabilities while sharing the common architectural Core.

**See also**

- Platform
- Core
- Configuration

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

## Reference Cardinality

Reference Cardinality defines how many target Domain Objects may be associated with a single Reference Source.

Typical cardinalities include one-to-one, one-to-many and many-to-many relationships.

---

## Reference Integrity

Reference Integrity is the architectural guarantee that every valid Reference either resolves to an existing Domain Object or reports a well-defined resolution failure.

Reference Integrity is maintained across Runtime and Storage boundaries.

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