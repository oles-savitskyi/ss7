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

## Runtime

**Category:** Runtime

**Status:** Stable

**Definition**

The execution environment responsible for interpreting metadata and executing business functionality provided by configurations.

**See also**

- Metadata
- Platform

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