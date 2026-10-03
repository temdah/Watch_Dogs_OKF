---
type: Performance Audit
title: Measuring native patch overhead without confusing it with frame cost
tags:
- shadow-engine
- performance
- audit
- diagnostics
- ownership
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-c681b34977c2
  title: Corrected active-world .75 runtime, H3 H4 safety and H8 section acceptance
- resource: ../../../evidence/catalog.json#E-8d9b4b980f5d
  title: H5 frozen-reference equivalence, bounded query benefit and retained offline gates
- resource: world-quality-validation.md
  title: World Quality Validation Overhead
- resource: ../../../evidence/catalog.json#E-ab6fdb75eac9
  title: Positive .73 runtime scope, accepted H4 and confirmed H3 diagnostic defect
- resource: overhead-measurement.md
  title: Whole-Mod Overhead Measurement
- resource: ../../../evidence/catalog.json#E-7767f6ab4c2e
  title: Subsequent positive71 runtime report and actual capture settings
- resource: ../../../evidence/catalog.json#E-6b3137e855d3
  title: Complete source inventory and O1-O8 findings
- resource: ../../../evidence/catalog.json#E-48f1787e23c9
  title: Mandatory lookup and full-source audit ownership
- resource: ../../../evidence/catalog.json#E-14854c48c29c
  title: Fingerprints of current working sources and preserved artifacts
- resource: ../../../evidence/catalog.json#E-8a0566483f0a
  title: Positive user report, balanced ownership and fixed-setting comparison limits
- resource: ../../../evidence/catalog.json#E-06078fbd86b8
  title: Earlier complete0/4/10 workload comparison
- resource: completion-diagnostic-overhead.md
  title: Completion Diagnostic History Lookup
- resource: renderer-queue-validation.md
  title: Renderer Queue Validation and Overhead
- resource: ../../../evidence/catalog.json#E-0042fc735065
  title: Historical099 observer overload and0910 control provenance
- resource: periodic-summary-transport.md
  title: Worker-Owned Periodic Summary Output
- resource: detail-window-observation.md
  title: Explicit Detailed Observation Windows
- resource: ../../../evidence/catalog.json#E-507569856b8d
  title: Active unity composition
- resource: ../../../evidence/catalog.json#E-0820f977d60c
  title: Module ownership and compile-time boundaries
- resource: ../../../evidence/catalog.json#E-e88c2f23e9a3
  title: Atomic helpers, logging and memory validation
- resource: ../../../evidence/catalog.json#E-ad4735a0faf6
  title: Publication, classification, fixed vehicle quality and limiter preparation
- resource: ../../../evidence/catalog.json#E-8b97f6755321
  title: Separate fixed world-quality pass
- resource: ../../../evidence/catalog.json#E-4937ea837086
  title: Continuous producer and asynchronous completion observation
- resource: ../../../evidence/catalog.json#E-f91ce7e5358a
  title: Current bounded CPU sampling and output
- resource: ../../../evidence/catalog.json#E-6658abb69696
  title: Mandatory owner safety and continuous admission telemetry
- resource: ../../../evidence/catalog.json#E-9a4ab6c06cd6
  title: Renderer ordering, validation and optional queue observation
- resource: ../../../evidence/catalog.json#E-6c0b42188e37
  title: Mandatory external-result ownership and periodic summaries
- resource: ../../../evidence/catalog.json#E-f45567a3ad24
  title: Construction and constant-time runtime routing
- resource: ../../../evidence/catalog.json#E-8e4b6b03d025
  title: Native mailbox worker
- resource: ../../../evidence/catalog.json#E-fdebcf63c883
  title: Bounded bootstrap worker and runtime entry
- resource: ../../../evidence/catalog.json#E-b6e7111dd577
  title: Manual menu and capture-only status watch
---

# Measurement boundary

The Shadow Engine experiments distinguish source work, sampled CPU intervals,
native resource ownership, and visible frame performance. A faster helper is not
automatically a faster frame. Manager/renderer intervals omit preparation,
restoration and some quality work; nested intervals cannot simply be added.
Neither CPU timing nor balanced references proves GPU completion or frame pacing.

# Cost and ownership inventory

| Path | Work and interpretation |
| --- | --- |
| Bootstrap | Profile validation and transactional installation are startup costs, not steady frame costs. |
| Vehicle publication | Whole-batch identities remain necessary for quality policy even with the limiter disabled. Disabled selection can skip copying, ranking and link writes without removing publication. |
| Quality | A 4096 cap still inspects identities. World missing-identity behavior differs from vehicle passthrough; a common shortcut must not erase that distinction. |
| Teardown | Tracking up to 128 copied owners from F10 observations is diagnostic coverage, not a native lifetime pin. |
| Pressure observation | Up to 256 binding inspections and memory-region queries are optional observer work. |
| Renderer queue | The face clamp validates the complete bounded prefix, up to 31 queue entries; individual objects still require valid memory. |
| External results | A 2048-slot sidecar and bounded 65536-poll writer drain protect ownership. Actual contention was not established; deleting checks would change safety. |
| Completion history | Atomics, correlation and QPC have a cost. Restricting detailed history to capture windows also changes what history and peaks are observable. |
| Logging | Open/write/close on a game callback can introduce latency. Copied periodic summaries can move I/O to a worker; urgent/manual output has a separate contract. |
| Lua controls | A 250 ms mailbox worker is separate from renderer callbacks. Menu activity and rendering cost require separate attribution. |

# Changes tried and their limits

- A disabled-diagnostics build exposed a real ownership bug: a result slot was
  assigned only inside an Internal conditional but used outside it. Moving the
  mandatory lookup outside optional diagnostics repaired the source contract in
  .72. The Release build also omitted Lua repair, so it was not an isolated A/B
  control for observer cost.
- Known-serial completion lookup became direct after proving the sole publisher's
  masked ring position. Unknown-serial events still search oldest pending and
  count ambiguity. This is a mod observation protocol, not a native job fence.
- Capture-only detailed correlation needs explicit coverage labels: a manual
  report cannot claim complete historical peaks outside the recorded window.
- Fresh call-local memory-region scopes and a hoisted identity hash reduced
  repeated validation. They retain object checks and do not cache permissions
  across callbacks. Fragmented mappings can still require extra region queries.
- Periodic summaries transport copied scalars to a worker and release their slot
  before I/O. They do not retain native pointers for later dereference.
- Testing dimensions before inspecting over-cap entries can reduce work, but it
  changes diagnostic counters. Inspected-entry coverage must be separate from
  complete-capture counts; under-cap entries are not silently counted as inspected.

No measured case established that enlarging caches, changing sidecar capacity or
removing mandatory checks would improve frame rate safely. The implementation
details and proofs are owned by [queue validation](renderer-queue-validation.md),
[known-serial lookup](completion-diagnostic-overhead.md),
[detail windows](detail-window-observation.md),
[periodic transport](periodic-summary-transport.md), and
[world validation](world-quality-validation.md).

# Recorded comparisons

The accepted .75 control used 0/4096/4096 policy. It had 13/13 periodic packets,
214151 balanced acquisitions/retirements, and a world interval mean of 29.796250
microseconds over 320 samples. Independent fixtures made 6719 checks; an ideal
region layout reduced about 60 queries to 1–2. Different workloads and fragmented
layouts limit extrapolation. An earlier .75 run used 4/2048 with world quality
disabled; its 0.138438 microsecond interval was not an equivalent comparison.

In .70, limit 4 had mean preparation 71.200 microseconds and native queue 592.702
microseconds with 21.68 faces. Limit 0 had preparation 0.604 microseconds and
queue 660.006 microseconds with 26 faces. Lower policy work did not imply lower
native work. These samples do not establish the cause of a stutter.

In .69, limits 0/10 both averaged 26 faces and 9.52/9.20 known owners, despite
0/48.32 suppressed lamps. Limit 4 averaged 20 faces and four owners. Preparation
means were 0.500/65.914/55.522 microseconds for 0/10/4. This illustrates why a
suppression count alone does not measure admission, physical occupancy or savings.

The .71 run balanced 144804 acquisitions/retirements. ETW access error 5 prevented
the intended frame measurement; it supplies no FPS result. Separately, .9.9
recorded about 5.3 million broad wrapper observations for 8704 consumer
submissions. Removing that broad observer in .9.10 was followed by a reported
recovery. That is a useful observer-cost warning, not a general overhead estimate.

# Reproduction requirements

Compare exact binaries, policy values, observer coverage, scene/route and capture
duration. Preserve native return behavior and ownership checks while changing
one cost boundary. Report source reductions, synthetic checks, CPU measurements
and human visual results separately. See [overhead measurement](overhead-measurement.md)
and [frame capture failures and limits](workload-capture.md).
