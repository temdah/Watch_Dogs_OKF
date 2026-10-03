---
type: Diagnostic Implementation Contract
title: Completion Diagnostic History Lookup
description: Retained known-serial lookup and the retained .74 correction separating producer
  scope from optional history.
tags:
- shadow-engine
- diagnostics
- overhead
- concurrency
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-c681b34977c2
  title: Corrected .75 runtime, H3/H5 acceptance, H8 closure and settings-continuity request
- resource: ../../../evidence/catalog.json#E-650f8fa72d27
  title: Passed .74 offline gates; no standalone runtime test claimed
- resource: ../../../evidence/catalog.json#E-ab6fdb75eac9
  title: Positive .73 gameplay and H4 with confirmed H3 scheduler attribution defect
- resource: detail-window-observation.md
  title: Explicit Detailed Observation Windows
- resource: periodic-summary-transport.md
  title: Worker-Owned Periodic Summary Output
- resource: ../../../evidence/catalog.json#E-e7bd6b8dce8a
  title: Positive72 feedback, complete H1/H2 scope and selected H5 world item
- resource: ../../../evidence/catalog.json#E-7767f6ab4c2e
  title: Positive71 stability/fidelity report, actual settings and preserved logs
- resource: ../../../evidence/catalog.json#E-8951a243a384
  title: Lookup-first proof, independent review and unchanged observation boundaries
- resource: ../../../evidence/catalog.json#E-5a2ca9716e6c
  title: Candidate build, preservation, validation and manual gate
- resource: ../../../evidence/catalog.json#E-01bcce8f8294
  title: Sanitized placement invariant and known versus unknown serial consumers
- resource: renderer-queue-validation.md
  title: Renderer Queue Validation and Overhead
- resource: mod-performance-audit.md
  title: Measuring native patch overhead without confusing it with frame cost
- resource: overhead-measurement.md
  title: Whole-Mod Overhead Measurement
- resource: ../../../evidence/catalog.json#E-4937ea837086
  title: History publisher and lookup consumers
- resource: ../../../evidence/catalog.json#E-176d7aee808c
  title: Diagnostic state owner and power-of-two bounds
- resource: ../../../evidence/catalog.json#E-f2e76494a58a
  title: Actual-source publication and frozen-reference tests
- resource: external-slice-results.md
  title: External Slice Results
---

# Scope

This concept owns the known-serial history lookup. [Detailed windows](detail-window-observation.md) owns producer scope, synchronization and bounded reporting; [periodic transport](periodic-summary-transport.md) owns worker output. Mandatory resource ownership is separate.

# Retained .71/.72 placement and consumers

Internal module 19 owns bounded diagnostic history in the root context. Each
record has eight entries. The sole positive-serial publisher chooses
`history[(uint32_t)serial & (COMPLETION_DIAGNOSTIC_HISTORY-1)]`, clears the old
serial, initializes metadata and publishes the new serial last. A compile-time
guard requires power-of-two history size. The global observation serial is
not a per-record sequence, allocation generation or native completion fence.

v2.0.71 replaces the linear known-serial lookup with that exact ring position
and the same atomic serial equality check. Scheduler faces, producer seal,
pre-finalizer and reset observations supply known serials. Null/nonpositive,
unpublished, overwritten and mismatched identities still return no match.
No new mutable state, pointer retention, allocation or synchronization is added.
All existing Internal profiles share this code; hook/ABI/profile data is unchanged.

The separate asynchronous-completion scan still searches all history entries
for the oldest pending bit and counts ambiguity. It has no known serial input;
replacing it with current-serial indexing would change diagnostic behavior.
In 71/72, counters, timing, history capacity, publication and report formats remain.
Mandatory module 40 generation/cycle validation, result consumption and resource
retirement are unchanged. Release still excludes this diagnostic subsystem.

# Evidence and safety limit

The placement invariant is confirmed from current patch source, not a newly
mapped engine field. Tests compare the old linear reference over valid writer
states, sparse serials, wraparound ring reuse and boundary identities. They also
exercise actual publisher/scheduler/completion observations. A lookup requires
one atomic serial read instead of one through eight; this is operation-count
evidence, not total-mod or FPS attribution.

In the .71/.72 lookup-only change, observation can still race publication/reuse;
serial equality was not a lock or lifetime fence. That historical change did
not repair serial exhaustion. The detail-window implementation protects history with metadata
ownership and rejects exhausted identities under its separate window contract.
The positive 71 report supplies its stability/visual gate;72 adds positive runtime
feedback and bounded measurements at 0/4096/4096. Neither establishes causal FPS
improvement or all-profile acceptance. The retained .74 correction receives
its combined runtime gate in the corrected .75 run. Future feature stages keep their own bounded evidence contracts.

# Runtime evidence boundary

The verified .71 Global run had two complete 5 s windows at limit 4 / vehicle 2048 / world Original with no recorded applied changes. It balanced 144,804 external results and 124,635 resource releases, with zero inspected lifecycle failures or unmatched/ambiguous completions. ETW access error 5 supplied no FPS. One degraded selection sample and cumulative limiter fallbacks did not establish a visual regression. This configuration differs from later 0 / 4096 / 4096 captures.
