# POSTING_ARCHITECTURE.md

## 1. Purpose

Purpose of the Posting Architecture.

Definition of posting as the transformation of business objects into register movements.

---

## 2. Scope and Responsibilities

Responsibilities:

* document posting;
* document unposting;
* document reposting;
* movement generation;
* movement validation;
* dependency management;
* posting events.

Out of scope:

* document storage;
* register storage;
* totals calculation;
* query execution;
* reporting.

---

## 3. Architectural Principles

### 3.1 Metadata-Driven Design

Posting behavior is defined by metadata and implemented through posting handlers.

### 3.2 Document as Source of Truth

Documents are the authoritative source of accounting state.

Movements are derived artifacts.

### 3.3 Posting Result = MovementSet

Posting handlers never write directly to registers.

The result of posting is always a MovementSet.

### 3.4 Atomicity

Posting is an atomic operation.

### 3.5 Contract-Based Validation

All generated movements must satisfy register posting contracts.

### 3.6 Dependency Awareness

Posting must support dependency tracking and reposting.

---

## 4. High-Level Architecture

### 4.1 Core Components

* Posting Engine
* Posting Context
* Posting Handler
* Movement Builder
* Movement Validator
* Dependency Graph
* Event Publisher

### 4.2 Architecture Diagram

Document

→ Posting Engine

→ Posting Handler

→ MovementSet

→ Validation

→ Storage Layer

→ Totals Engine

---

## 5. Integration with Other Subsystems

### 5.1 Metadata Architecture

### 5.2 Runtime Architecture

### 5.3 Object Architecture

### 5.4 Storage Architecture

### 5.5 Register Architecture

---

## 6. Posting Lifecycle Overview

Summary of posting lifecycle.

Reference:

* POSTING_LIFECYCLE.md

---

## 7. Movement Model Overview

Summary of Movement and MovementSet concepts.

Reference:

* MOVEMENT_MODEL.md

---

## 8. Validation Overview

Summary of validation strategy.

Reference:

* MOVEMENT_VALIDATION.md

---

## 9. Dependency Management Overview

Summary of dependency graph model.

Reference:

* POSTING_DEPENDENCIES.md

---

## 10. Events Overview

Summary of posting-related events.

Reference:

* POSTING_EVENTS.md

---

## 11. Related Documents

* POSTING_LIFECYCLE.md
* POSTING_CONTEXT.md
* POSTING_HANDLERS.md
* MOVEMENT_MODEL.md
* MOVEMENT_VALIDATION.md
* REGISTER_POSTING_CONTRACTS.md
* POSTING_DEPENDENCIES.md
* POSTING_EVENTS.md
