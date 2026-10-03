---
type: Architecture Reference
title: 'Native patch architecture: ownership and binary-equivalence experiments'
tags:
- shadow-engine
- architecture
- cohesion
- ownership
status: draft
sources:
- resource: detail-window-observation.md
  title: Explicit Detailed Observation Windows
- resource: periodic-summary-transport.md
  title: Worker-Owned Periodic Summary Output
- resource: overhead-measurement.md
  title: Whole-Mod Overhead Measurement
- id: module-map
  resource: ../../../evidence/catalog.json#E-0820f977d60c
  title: Unity-module architecture
- id: root-context
  resource: ../../../evidence/catalog.json#E-176d7aee808c
  title: Shared configuration and root context
- id: cleanup-result
  resource: ../../../evidence/catalog.json#E-54d97d70abb6
  title: Internal and Release profile validation
- resource: ../../../evidence/catalog.json#E-c681b34977c2
  title: Corrected .75 runtime, H3/H5 acceptance, H8 closure and settings-continuity request
- resource: ../../../evidence/catalog.json#E-650f8fa72d27
  title: Passed .74 offline gates; no standalone runtime test claimed
- resource: ../../../evidence/catalog.json#E-ab6fdb75eac9
  title: Positive .73 gameplay and H4 with confirmed H3 diagnostic blocker
- resource: ../../../evidence/catalog.json#E-e7bd6b8dce8a
  title: reported-positive72 runtime baseline and measurement scope
- id: cloth-diagnostic-state
  resource: ../../../evidence/catalog.json#E-6d95aa568f93
  title: Diagnostic-build context extension
- resource: ../../../evidence/catalog.json#E-e1ec3ffeb4c9
  title: Unity-module architecture
---

# Scope

Shadow Engine is a native Watch Dogs 1 patch used here as an implementation case
study. Its modules and `ShadowEngineContext` are mod-owned structures. Native
engine resource and job ownership are documented in the linked engine findings.

# Initialization and state ownership

One process-lifetime context separates bootstrap, hook bindings, manager and
renderer observation, resource/pass setup and external-result ownership. Detours
use explicit subsystem state. Static lifetime avoids construction and teardown
hazards while callbacks can still execute inside an injected module.

The TinyCC build uses one translation unit, `shadow_engine_patch.c`, with ordered
include modules. Earlier layers expose interfaces instead of reaching into later
modules through hidden globals. Immutable runtime profiles supply build-specific
addresses; common behavior does not branch on storefront names. Bootstrap orders
discovery, preparation and installation while the relevant subsystem owns policy.

# Diagnostics and safety are separate responsibilities

An Internal/Release split showed why removing observers requires more than
disabling log calls. In the 2.0.71 source audit, a mandatory result lookup assigned
`slot` only inside a diagnostic conditional, while later lifecycle code used it
outside the conditional. The corrected implementation moved that lookup outside
optional observation. A smaller binary alone did not establish equivalent behavior.

Producer tickets carry copied serials and restore thread-local attribution on
return. Lost optional history cannot leave a scheduling scope active. A worker
receives copied telemetry and performs file I/O; it does not later dereference
borrowed native pointers. See [detailed observation](detail-window-observation.md),
[external results](external-slice-results.md), and
[summary transport](periodic-summary-transport.md).

# What structural experiments established

A 2,903-line implementation was split into eight ordered modules and reproduced
the baseline ASI exactly before its version/checksum change. A later refactor
replaced 98 aliases with explicit context accesses and also preserved binary
identity. These experiments support the tested ABI/linkage and ownership changes;
they did not fix the existing FPS regression or demonstrate new engine behavior.
The [binary-equivalence record](../validation/historical-refactor-results.md)
preserves exact controls and limits.

The separate cloth experiment used an independently owned transaction. Failure
of that optional install rolled back its writes without undoing the early shadow
transaction. Journaled rollback is not atomic replacement against concurrent
engine execution; see [patch transactions](patch-transactions.md).
