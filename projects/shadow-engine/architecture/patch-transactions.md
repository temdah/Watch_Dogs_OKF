---
type: Architecture Reference
title: Patch Transaction Model
description: Immutable preflight plans, journaled executable writes, and bounded rollback guarantees.
tags:
- shadow-engine
- patching
- transaction
- rollback
status: draft
sources:
- id: private-detour-publication
  resource: ../../../evidence/catalog.json#E-e88c2f23e9a3
  title: Original trampoline publication before executable entry write
- id: private-transaction-module
  resource: ../../../evidence/catalog.json#E-b100e7b70c2c
  title: Patch transaction implementation
- id: private-orchestration-module
  resource: ../../../evidence/catalog.json#E-1576d48ce50e
  title: Patch orchestration implementation
- id: private-cloth-diagnostic-module
  resource: ../../../evidence/catalog.json#E-a3a09f241a70
  title: Optional cloth diagnostic transaction
- id: cloth-transaction
  resource: ../../../evidence/catalog.json#E-02e8b268f2e5
  title: Patch transaction implementation
- id: cloth-orchestration
  resource: ../../../evidence/catalog.json#E-32761c3b66e0
  title: Bootstrap orchestration
---

# Prepare, then commit

Runtime preflight resolves one complete profile, recovers helpers, and validates
all mutation sites without changing engine memory. Orchestration commits only a
prepared immutable plan.

# Rollback

Executable writes are journaled before mutation. A failed phase restores bytes
in reverse order, clears any published trampoline pointers, and releases
transaction-owned allocations.[^public-transaction]

v2.0.12 publishes the callable original trampoline before writing the detour
entry, so an immediately entering callback cannot observe a not-yet-published
original. The same journal clears the pointer on complete rollback. If any
executable restore fails, allocations and bindings remain alive. The optional
intersection TLS slot is freed only after complete rollback. Synthetic native
tests exercise failed entry-write and successful-install rollback paths.

# Phase boundary

Early construction and deferred downstream installation are separate
transactions because the game creates required engine objects between them.
This is journaled rollback, not atomic code replacement against concurrently
executing threads. The model does not claim that
engine-owned objects created between phases can be rolled back.

[^public-transaction]: Patch transaction implementation

# Historical optional diagnostic boundary

The separate cloth diagnostic transaction ran after the early shadow transaction and owned only its GEOM hook and trampoline. A failed diagnostic install rolled back that diagnostic without undoing the shadow transaction. This is historical experimental architecture, not a cloth hook in the current Shadow Engine build. The older claim that each phase is atomic is superseded: journaled writes do not provide atomic replacement against concurrent native execution.
