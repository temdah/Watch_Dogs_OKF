---
type: Diagnostic Method
title: Black Shadow Flicker Attribution
description: Historical first-invalid-boundary tracing and the bounded v2.0.12 intersection
  diagnostic without rendering changes.
tags:
- shadow-engine
- black-flicker
- provenance
- diagnostics
- intersection
status: draft
sources:
- id: private-clean-control
  resource: ../../../evidence/catalog.json#E-e2766fed405b
  title: v2.0.13 clean intersection control
- id: private-configuration-comparison
  resource: engine-capacity-layout.md
  title: Shadow Capacity Layout
- id: private-intersection-runtime
  resource: ../../../evidence/catalog.json#E-f1d21cb670c4
  title: First Global observer capture and bounded negative findings
- id: private-candidate
  resource: ../../../evidence/catalog.json#E-bb40424d0f3d
  title: Candidate preflight, mappings and offline validation
- id: private-implementation
  resource: intersection-diagnostics.md
  title: Bounded Intersection Provenance
- id: private-provenance
  resource: ../../../evidence/catalog.json#E-9aa0701ae5ab
  title: Successful lookups followed by resource-field divergence
- id: private-tail
  resource: ../../../evidence/catalog.json#E-b3e87aaac6dd
  title: Builder-tail checkpoint result
- id: private-task
  resource: ../../../evidence/catalog.json#E-4bcac223e6d8
  title: Task identity rejects record reuse and identifies same-cycle mutation
- id: private-writer
  resource: ../../../evidence/catalog.json#E-a304eb658ae0
  title: Rejected candidate and recovered SliceExecute overwrite
- id: private-fix
  resource: ../../../evidence/catalog.json#E-4bf5a517eef1
  title: Runtime confirmation of the indexed-overwrite correction
- id: private-current
  resource: ../../../evidence/catalog.json#E-1260c58419aa
  title: Zero-rejection session with remaining intersection symptom
- id: private-observer
  resource: ../../../evidence/catalog.json#E-95804568a8f8
  title: Historical observer source, not current installation instructions
- id: private-queue
  resource: ../../../evidence/catalog.json#E-9a4ab6c06cd6
  title: Current F8/F9 queue capture and face guard
---

# Historical method and proven fix

The successful method was first-invalid-boundary tracing, followed by exact
writer recovery. Global/04DF observers followed resource values through lookup,
builder checkpoints/exit, task creation/execution, callback entry and release.
Expected values came from native lookups, not arbitrary previous-frame pointers.
v0.9.2 proved valid lookup results became null or a displaced pointer; v0.9.4
found all 115 F8 failures after the last observed tail lookup. Later async
evidence corrected the assumption that these boundaries were sequential work
on one thread.[^private-provenance][^private-tail][^private-task]

v0.9.7 correlated task pointer, record pointer, lifecycle generation and builder
identity. It found 5,917 queued mutations with unchanged identity and zero record
reuse, plus 17 execute-to-callback changes. This rejected pooled-record reuse as
the dominant cause. A candidate writer at Global `0x0024CEF0` was then rejected
because it never received a tracked record, despite a suggestive indexed store.
[^private-task][^private-writer]

Static recovery found the real unbounded stores at Global `0x002CC316` (non-null)
and `0x002CC32B` (null). Their inputs are result base, queue-entry/result index
and result value. The native array has 17 qwords at record `+0x70..+0xF0`;
indices 17-21 overwrite independent fields `+0xF8/+0x100/+0x108/+0x110/+0x118`.
Native collection owns only indices 0-16.[^private-writer]

v0.9.9 retained native stores and routed extra results into separately owned
storage, not suppression. Its runtime had zero tracked field divergence, repair
demand or displaced-resource sidecar demand; the tester reported the original bridge
black flicker apparently gone. Old repair was containment, not the final fix.
The remaining result lifetime issue is separately covered by the
[current lifecycle contract](external-slice-results.md).[^private-fix]


# Intersection evidence and limits

A remaining intersection symptom was reported in 2.x after the earlier bridge overwrite correction. A repeated original-v1.2.0 control was clean; negative bounded CPU audits do not invalidate that visual difference.

The .11 run retained the symptom with zero result rejections. Its F8/F9 queues describe entries, face/map ranges, handles and lifecycle totals, but neither the old lookup-to-use field trace nor the ground draw. Cumulative clamps and keypress names are not causal or frame-perfect evidence.

The .12 Global recorder observed 1,252 nonnull lookups across all three native callers with zero boundary mismatch. Its ring retained 1.781 s before the marker and 1.500 s after, but the exact flash frame remained unknown. Anomaly, contention and slot-miss counts were zero. Ownership balanced 110,139 external results with zero rejects/stale/late or release/reset failures. Nineteen clamped submissions dropped 22 record occurrences; the marked queue itself was 26/30 faces without clamping. No resource was tied to the ground receiver, so neither the original overwrite nor a rejection storm explained this capture.

The .13 current-code/original-configuration control was visually clean: 1,867 lookup observations, 7,475 independent field comparisons with no differences, and 622 queue submissions with zero clamps/drops and at most 22 faces. F9 balanced 13,549 external results with zero rejection/stale/late. The BLACK_F8 label did not mean flicker occurred. Later capacity/admission isolations and their remaining limits are recorded in [capacity layout](engine-capacity-layout.md); a clean run without high-index use cannot establish high-index safety.

# Attribution method

The [intersection recorder](intersection-diagnostics.md) owns event fields, mapping, bounded buffers, TLS and worker output. It observes native returns and valid synchronous boundaries without repairing resources. It does not identify ground/GPU receivers, dispatch ownership, actual cache assignments or pass bindings.

Integrity evidence compares expected native lookup values and neighboring resource fields at initialized, same-lifetime boundaries, using constructor generation, producer/builder identity, thread and timestamp. Task identity can separate same-cycle mutation from record reuse. Builder identity is observational and must not become a restored publication gate.

Rendering evidence needs actual per-cycle clamps/skips, proven full light/owner identity, face/map/pass/handle association, scheduled/completed work and cache/dynamic assignment. Unknown vehicle/world identity stays unknown. Derived queue prefix ranges do not prove native or GPU binding.

- Valid lookup becoming wrong before use brackets a writer interval.
- Missing lookup points toward creation/streaming.
- Intact fields plus proven sampled skipped/reassigned resources implicate refresh/admission coherence.
- Otherwise, receiver draw, shadow/mask binding and texture contents remain separate targets.

Copied evidence must remain bounded and generation-aware, with explicit overflow/contention and sparse anomalies. Background output never dereferences stored engine pointers. Avoid global resource/submit scans, per-face VirtualQuery and continuous file logging. Historical .9.7 exposed a TinyCC return-value sparse-gate pitfall; the established atomic sparse-gate helper avoids accidentally dense logging. Historical observer and repair code is provenance, not an active repair or portable regional approval.

[^private-fix]: Runtime confirmation of the indexed-overwrite correction

[^private-provenance]: Successful lookups followed by resource-field divergence

[^private-tail]: Builder-tail checkpoint result

[^private-task]: Task identity rejects record reuse and identifies same-cycle mutation

[^private-writer]: Rejected candidate and recovered SliceExecute overwrite
