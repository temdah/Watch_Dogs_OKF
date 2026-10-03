---
type: Runtime Safety Contract
title: Renderer Queue Validation and Overhead
description: Synchronous queue-field validation reuse with unchanged face admission and resource-object
  checks.
tags:
- shadow-engine
- renderer
- safety
- performance
- validation
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-9a4ab6c06cd6
  title: Queue clamp and face-cost reader
- resource: ../../../evidence/catalog.json#E-e88c2f23e9a3
  title: Unchanged individual memory validation
- resource: ../../../evidence/catalog.json#E-643d5590b1e1
  title: Actual-source renderer tests and frozen pre-change reference
- resource: engine-capacity-layout.md
  title: Shadow Capacity Layout
- resource: workload-capture.md
  title: Bounded Shadow Workload and Presentation Capture
- resource: ../../../evidence/catalog.json#E-8a0566483f0a
  title: reported positive70 report, preserved logs and fixed-setting test preference
- resource: ../../../evidence/catalog.json#E-59f409d3f755
  title: Recorded knowledge lookup and selected single-change scope
- resource: ../../../evidence/catalog.json#E-4d8170434fc6
  title: Candidate preservation, validation and manual delivery gate
- resource: ../../../evidence/catalog.json#E-5a0d93f0056f
  title: Sanitized function, ownership and safety contract
- resource: mod-performance-audit.md
  title: Measuring native patch overhead without confusing it with frame cost
---

# Role and ownership

The shared module 30 clamp reads the native queue count and each entry's face
count, exposing the largest complete prefix that fits the 30-map budget. The
renderer hook restores the original queue count after native rendering so native
cleanup retains all records. The face-cost reader sums readable non-null objects'
cost fields through the queue's face slots. These are patch-source-confirmed
roles; the existing regional layout and hook contracts remain unchanged.

v 2.0.70 creates a zero-initialized `RendererQueueReadScope` on the stack of each
clamp and face-cost invocation. It owns one successful memory-region observation,
valid only for queue fields during that synchronous loop. There is no heap,
shared state, lock, cross-call cache or retained engine-object identity. Neither
loop calls the native engine; the scope expires before returning to its caller.
It is never shared with the original renderer, capture or return-side diagnostics.

# Validation and safety

Every requested field must be non-null, nonempty, free of integer wrap and wholly
contained in a committed region without guard/noaccess protection. A cached hit
uses only the exact range returned by VirtualQuery. A miss queries the current
address and rejects invalid or overflowing returned ranges before caching them.
AllocationBase is never used to infer a wider readable span. Separate readable
regions are not merged, so a straddling field retains its rejection behavior.

Only queue count, entry face counts and face pointer slots use this scope.
Each non-null cost object retains its own `readable_memory` query immediately
before its cost field is read. Queue lifetime cannot establish resource lifetime.
All loop bounds, malformed-count handling, break/continue decisions, totals,
queue writes/restoration and failure counters are retained. No safety ownership
is transferred and no rendering, selection, quality or lifecycle policy changes.

Reuse depends on the synchronous queue-lifetime contract already required by
these direct reads. It does not make arbitrary concurrent unmapping safe; neither
does a separate VirtualQuery immediately before a read. No validation fact may
survive a native call or be reused on a later invocation.

# Validation boundary

The tester reports a stable Global 70 run with no observed stuttering and accepts
continuing overhead work. This is scoped runtime evidence;
the cause of the improvement and quantitative FPS gain are not established.
The preserved run has two complete limit 4/0 windows at vehicle 4096/world
Original and 240,754 balanced external results with zero lifecycle failures or
face drops. ETW supplied no FPS. Whole-mod overhead later closed on .75;
regional acceptance remains a separate gate.

The actual-source harness compares return values, all queue bytes and skip
counters with frozen v 2.0.69 functions, including malformed/overflowing counts,
mixed faces, protected/uncommitted regions and straddling reads. Query counts
distinguish queue validation from unchanged resource checks; a protection change
between calls must be observed by the next fresh scope.

This reduces a demonstrated query mechanism, not a measured whole-mod FPS cost.
Existing workload timings omit some wrapper work and include nested work in
native intervals. They cannot establish total patch overhead by addition.
Runtime performance, visual equivalence and stability remain manual gates.
The four mapped profiles retain their established compatibility checks; A4EE
remains manual-required. The finite overhead stage is closed; see [its register](mod-performance-audit.md).
