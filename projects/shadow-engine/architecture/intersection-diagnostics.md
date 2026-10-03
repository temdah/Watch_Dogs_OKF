---
type: Diagnostic Contract
title: Bounded Intersection Provenance
description: Opt-in CPU resource-field and queue history without rendering-policy or resource-ownership
  changes.
tags:
- shadow-engine
- diagnostics
- intersection
- provenance
- lifecycle
status: draft
sources:
- id: public-recorder
  resource: ../../../evidence/catalog.json#E-258f774a106c
  title: Bounded recorder and lookup observer
- id: public-profiles
  resource: ../../../evidence/catalog.json#E-4d85852a0d8b
  title: Immutable regional validation data
- id: public-harness
  resource: ../../../evidence/catalog.json#E-31a1d6a6b529
  title: Actual-source synthetic recorder and preflight tests
- id: public-corpus
  resource: ../../../evidence/catalog.json#E-ebc961aaf6ec
  title: Independent regional byte gate
- id: public-ownership
  resource: external-slice-results.md
  title: External Slice Results
---

# Purpose and scope

Introduced in .12, this opt-in CPU recorder captures resource-field and queue history around a user marker. It adds no resource ownership or rendering-policy change and does not assert whether a symptom is an indexed overwrite, rejection, queue drop or GPU defect. The .13 capacity/admission control retained the recorder byte-for-byte. Historical runtime findings are owned by [black-flicker attribution](black-flicker-diagnostics.md).

# Recovered lookup boundary

The native shared-texture lookup takes manager, key and descriptor and returns
a resource pointer; the observer borrows that value, never acquires or repairs
it. Three builder CALL rel32 sites return values stored into record +0x100,
+0xF8 and +0x110. Global return RVAs are 0x003DDD9C, 0x003DDFC0 and 0x003DE059.
The native stores begin 12, 0 and 4 bytes after those returns respectively.
They must all resolve to one target and match their regional record register.
The observer associates only these callers with a currently active builder
using a nested Windows TLS scope plus constructor generation. Other calls
remain passthrough; no global resource-to-record search is added.[^public-recorder]

Static corpus checks recover shared target Global 0x00430A80, VMPless
0x00976800, Complete 0x01DBCE90 and Asia 0x009A5CF0. Asia uses R13 record stores
and a different 15-byte prologue; the other checked profiles use R15. These are
byte-level findings, not current live-hook approval. A4EE has no mapped fixture
and remains manual-required; its historical preflight log cannot validate this
hook. Synthetic five-profile tests prove rejection logic only.[^public-profiles][^public-corpus]

Complete read-only validation runs before any early mutation and again before
the deferred lookup detour. The transaction owns the trampoline/binding. A
complete rollback releases the diagnostic TLS slot; an incomplete executable
restore preserves TLS and bindings for potentially reachable hooks.

# Capture lifetime and controls

Module 17 exclusively owns `ShadowEngineContext.intersection`: process-lifetime
8,192-event ring, 128 reserved first mismatch candidates and 256 identity slots.
No engine object is retained. State is idle (0), recording (2), frozen/retry (3)
or worker-owned (4); rearm cannot overwrite a frozen or flushing buffer.

F7 arms or stops, F8 marks the event, F9 finishes early or retries a failed
flush. F8 alone does not arm. Default is off. Render polling freezes after
1.5 seconds past F8, or 60 seconds without a marker; paused/no-render intervals
can delay polling. Prehistory is event-bounded, not a guaranteed time duration.
F8/F9's existing snapshots and F10 remain intact. The recorder itself has no on-screen overlay; tools actions can invoke its controls.

A single-attempt diagnostic lock protects copied metadata. Contention drops
observations and increments a counter, never waits or gates native work. The
worker writes only frozen copies to `ShadowEngineIntersection-<PID>-<capture>.log`.
Main-log begin/end/failure markers are sparse; no per-event rendering-thread
file logging is added. Thread-pool creation/write failures leave copies available for explicit F9 retry.

# Record interpretation

`IX_EVENT` kind: 1 constructor, 2 builder enter, 3 lookup return, 4 builder exit,
5 producer entry, 6 producer return, 7 pre-finalizer, 8 release entry, 9 queue
summary, 10 queue entry, 11 external completion, 12 user marker.

Fields are copied at +0xF8/+0x100/+0x108/+0x110/+0x118. Expected values exist only
for the three observed lookups; a null return is a valid expectation. A lookup
event excludes its own not-yet-performed native store from mismatch testing.
Builder entry and constructor generation changes invalidate old expectations.
Field tuples are not atomic. A mismatch is a candidate transition, not proof of
corruption; native clearing/replacement must be distinguished before a fix.
Completion events record identity/value only and never dereference a job's raw
result-base pointer. There are no new per-face memory queries.

For queue summaries `data` is original entries, admitted entries, requested
faces, admitted faces. For entries it is index, face count, derived prefix-map
start/end (end exclusive), dropped flag, candidate first-map handle. Face
object pointers are copied but not followed. Complete entry samples are at most
10 Hz; dropped trailing entries are recorded each clamped queue call. Prefix
map ranges and handle values are derived, **not proof of native/GPU binding**.
Only the first derived handle is logged; this is not full per-face pass binding.

Constructor generation, producer cycle, builder identity, thread, tick and
sequence correlate observations. No task-dispatch hook, vehicle owner classifier,
ground receiver draw, GPU texture contents or cache assignment attribution is
implemented. Intact CPU pointers do not establish GPU correctness. Continue to
receiver/draw-specific investigation if this capture does not bracket a defect.

# Validation boundary

Actual-source native tests cover disabled passthrough, nesting, valid-null and
lookup-before-store expectations, generation reuse, contention, bounds, dropped
entries, freezing, retry and real thread-pool flushing. Source contracts forbid
resource ownership/waits and check preflight/worker boundaries. The corpus adds
seven checks per available profile (71 total); A4EE remains manual-required.
All current live hook, performance, intersection and bridge observations must
come from manual runtime tests. This is an experimental diagnostic, not a fix.

[^public-recorder]: Bounded recorder and lookup observer
[^public-profiles]: Immutable regional validation data
[^public-harness]: Actual-source synthetic recorder and preflight tests
[^public-corpus]: Independent regional byte gate
[^public-ownership]: Retained producer-owned lifecycle
