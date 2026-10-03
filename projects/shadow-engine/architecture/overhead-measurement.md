---
type: Internal Diagnostic Contract
title: Whole-Mod Overhead Measurement
description: Accepted72 H1/H2 measurement baseline, runtime coverage limits and one-time H5
  world-validation selection.
tags:
- shadow-engine
- overhead
- measurement
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
  title: Valid inactive .73 cost windows, accepted H4 and H3 correctness blocker
- resource: detail-window-observation.md
  title: Explicit Detailed Observation Windows
- resource: periodic-summary-transport.md
  title: Worker-Owned Periodic Summary Output
- resource: ../../../evidence/catalog.json#E-e7bd6b8dce8a
  title: Positive72 runtime report, fixed-setting captures, safety balance and H5 decision
- resource: ../../../evidence/catalog.json#E-baed3422a50f
  title: Delivery hashes, retained behavior, offline results and runtime gate
- resource: ../../../evidence/catalog.json#E-681ded4c7bc4
  title: Complete sanitized interface, ownership, coverage and interpretation contract
- resource: ../../../evidence/catalog.json#E-5f8b75cd9631
  title: Pre-edit source/knowledge and preserved runtime evidence
- resource: ../../../evidence/catalog.json#E-822325232d9e
  title: Dirty71 source snapshot and newest log identity
- resource: ../../../evidence/catalog.json#E-bd50d0b23306
  title: Explicit timing interface and uninstrumented fixture boundary
- resource: ../../../evidence/catalog.json#E-cf8aad4eafd1
  title: Measurement state, admission, sampling and copied reports
- resource: ../../../evidence/catalog.json#E-f91ce7e5358a
  title: Worker request, close, drain and durable completion
- resource: ../../../evidence/catalog.json#E-6c0b42188e37
  title: Mandatory ownership lookup and lifecycle timing
- resource: ../../../evidence/catalog.json#E-c00344dc42c3
  title: Actual-source bounded timing and race checks
- resource: ../../../evidence/catalog.json#E-2347b2daa639
  title: Actual ownership with diagnostic compilation enabled and disabled
- resource: ../../../evidence/catalog.json#E-c38ab69eeed1
  title: Preserved historical technical evidence
---

# Scope

Version .72 introduced bounded measurement and diagnostic-independent
ownership; the corrected .75 control supplies the later scoped runtime evidence. The instrumentation measures sampled wall intervals, not exact whole-mod CPU, GPU cost or FPS. Later .74 H3 correction was exercised in .75; there was no separate .74 game test or all-profile acceptance.

# Ownership and admission

Internal module 12 follows module 10 and owns `ShadowEngineContext.overhead`.
Storage is allocated on the worker's first capture request, atomically published
and retained for process lifetime. Its arrays contain scalar timing/count/thread
data; tickets never retain engine objects. Release excludes the module and its
state. The explicit header provides no-op probes to standalone fixtures.

One worker requests, closes and reports. Positive active tokens are never reused;
zero closes admission. A callback reads the token, increments a process-lifetime
inflight count and rechecks the token before touching window data. A delayed old
entrant therefore cannot write into a new window. Inflight is never reset.
Each accepted ticket exclusively owns one slot until its final scalar publish
and decrement. Pauses retain ownership while excluding selected native calls.
No lock is held across native execution and no engine thread waits for capture.

Closing prevents new admission. The worker polls until admitted tickets drain
before reporting or reusing arrays; a delayed callback retains its storage and
keeps the capture busy. A once-only delayed-drain record explains missing
completion. It never discards ownership to announce success. Token exhaustion,
allocation/frequency failure or a busy core rejects a new request. Request
failure advances the workload serial and publishes failure without arming ETW
or reporting an old overhead window.

# Sampling and interpretation

The existing action 11 requests 3 s lead-in and 5 s recording. Calibration completes
before the capture clocks start. GetTickCount bounds admission and selects one
first eligible sample per category per 10 ms bucket, at most 500 slots/category.
Only accepted samples call QPC; active calls still pay coarse gates, atomics and
call accounting. Closed probes perform bounded root/state admission checks.
The coarse clock may skip buckets; it is not exactly aligned with the workload
QPC stream. Existing manager/queue samples remain at their separate 10 Hz cadence.

The 72 reports identify H1,H2, continuous observation, calls/cadence, occupied buckets,
valid/invalid samples, collisions, sampled threads, late completion and timer
failures. Per-category mean/p50/p95/sample maximum and sampled sum describe
sampled wall intervals. Raw worker calibration reports timer pairs and local
idle/occupied gates; it excludes root-pointer loads and live contention and is
never subtracted. Missing calls mean **not observed**, not free work. A 5 s capture
may miss the 30 s periodic summary, flushes, retirement or other infrequent paths.

H3/H4 integration is implemented in .73. Its measurement reports
identify windowed policy and actual observer coverage, including phase/window
changes during the measurement request. Action 11 measures without arming H3
detail; an idle or changed observation period cannot be labelled continuously
recorded. The .73 runtime windows confirm the independent inactive modes;
H3's separate scheduler-attribution defect does not invalidate those cost rows.

Coverage includes vehicle batch/update/transform/publication/retirement,
manager direct work/admission/limiter prepare/restore, renderer clamp/tails and
each quality pass, producer open, completion producer/scheduler/result/markers,
external store/consume/reset, resource submission, lifecycle wrappers, capacity,
face-cost replacement, capture observers and log writes/flushes.

These are overlapping measurements, not additive CPU accounting:

- Manager/renderer envelopes pause their primary native call. Manager may
  include rare native owner-vector reservation. Batch also excludes separately
  sampled publication; other envelopes include child observers.
- Store includes completion observation/rejected-result retirement; consume
  includes writer checks and native resource submission; reset/tail/constructor
  can include nested markers, draining and logs. Resource submission has its own
  native interval. Never sum those intervals with their parents.
- Native manager/renderer intervals include existing workload timer helpers;
  native scheduler intervals may contain asynchronous submission. Native wall
  durations are not patch-only CPU, job completion latency or GPU time.
- Tail/capture/lifecycle categories combine phases or wrappers. First eligible
  sampling can favor before/begin phases or early scheduler entries. Bursts and
  threads are not randomly sampled; means times total calls are not exact totals.
- Existing workload intervals now include some new probe cost. Comparing 71 and 72
  requires matching settings/workload and acknowledging that observer difference.

Frozen worker formatting is outside the capture window, so completion reporting
cannot recursively time itself.72 log transport and frequency are unchanged;
73's transport change belongs to H4 and is accepted within its tested scope.
This does not time every instruction in the mod, exact total CPU, displayed FPS
or GPU work. ETW unavailability does not invalidate these separate CPU intervals.

# Ownership independent of diagnostics

`store_external_slice_result` now performs its mandatory lifecycle lookup outside
the optional diagnostic compile guard. Internal ordering remains intersection
observation, mandatory lookup, completion observation, then ownership validation.
The result sidecar, writer/consumer exclusion, lineage, quarantine and exact
resource retirement remain mandatory regardless of telemetry compilation.
This corrects the source-confirmed diagnostics-disabled uninitialised-pointer
defect; it does not attribute a previous Internal crash or visual fault.

Offline validation passes 585 core checks,57 actual-unity workload/probe checks
and 28 ownership scenarios per diagnostic mode. The Internal ownership fixture
also drains 28 active captures without leaking tickets.

Actual-source fixtures cover enabled/disabled ownership, invalid/null/non-null
results, duplicate acquisitions, stale/late entries, consumer closure after
writer claim, quarantine and pending reset. Core checks cover bucket bounds,
close/rearm admission races, late drain, duplicate end, allocation/timer failure,
clock wrap and native pause. Offline proof is separate from game acceptance.



# Recorded comparison

Both .72 captures used 0 / vehicle 4096 / world 4096, 50 manager and 50 queue samples, and 320 valid frequent-category samples at the observed 64 Hz coarse-clock cadence. Invalid timing, late endings and QPC failures were zero. The ownership snapshot balanced 206,655 results (174,771 nonnull plus 31,884 null), with 206,655 consumed and 174,771 released. Lua .57 activation was recorded. ETW access error 5 supplied no FPS; positive general runtime feedback did not independently repeat every .71 visual classification.

| Metric | .72 windows | .73 windows | Corrected .75 |
| --- | --- | --- | --- |
| World pass mean us | 29.119 / 30.266 | 59.481 / 34.022 | 29.796250 |
| World median us | 29.2 / 28.7 | Not supplied here | 28.8 |
| Admission mean us | 5.650-5.788 | 0.081 / 0.075 | 0.068750 |
| Tail mean us | 11.972-12.887 | 0.091 / 0.088 | 0.096875 |
| Completion-result mean us | 0.633 / 0.637 | 0.247 / 0.259 | Not supplied here |

World cost exceeded raw timer-pair calibration of 0..0.1 us and local occupied-gate calibration of about 0.04..0.047 us, supporting the bounded H5 investigation without quantifying available savings. One .72 window observed five log writes and timed two at 348.25 us mean; the other observed none. Neither timed flushes, which occurred afterward. Measured face-reader/publication work remained required for safety.

The .73 windows had unchanged OFF epoch 0 and FROZEN epoch 1 modes, proving action 11 did not arm detail. Each retained 50 manager/queue and 320 frequent samples without invalid/late/timer failures. The report described stable gameplay/quality and perceived improvement, while 40+ car bridge pop-in remained unexplained. Ownership balanced 206,340 results and 172,111 releases; H4 delivered 15/15 packets without drops/write failures. Separately, the saved H3 window exposed false known-scheduler attribution after a missed optional seal; positive cost rows did not validate H3 correctness.

The first .75 run used 4 / 2048 / Original. Its disabled-world 0.138438 us mean is excluded from H5, although it exercised 32 missed optional seals without scope-close failures. Corrected .75 used stable 0 / 4096 / 4096 with frozen phase 3/epoch 1, 50 manager/queue samples and 642 world calls including 320 valid timing samples. World p95 was 41.9 us and sampled maximum 174.5 us. It recorded 503,862 exact-vehicle exclusions, zero unreadable/ambiguous cases and zero mutations because native dimensions already fit; the validation/classification pass was active.

Different workloads, threads and native conditions prevent treating these means as causal FPS or whole-mod savings. Corrected .75 balanced 214,151 consumed results and 178,125 releases with zero inspected failures. H3 had 6,483 starts/seals and 34,912 scheduled/matched results, zero missed-seal/TLS/control-close/overlap and unmatched/ambiguous observations; reporting succeeded after bounded drain with heuristic/incomplete coverage. H4 delivered 13/13 without drops/write failures.

H5's independent differential had 6,719 checks across 1,290 world and 16 identity cases against frozen .74. Queue bytes, counters, tokens and identity output matched. Query counts changed 60 -> 1 for dense regions, 60 -> 2 for two regions and 60 -> 60 when fragmented. Six alternating host rounds of 200 calls, each with fresh cache initialization, measured dense means 54.913 -> 1.133 us and fragmented 17.384 -> 17.849 us. The 0.47 us fragmented cost rules out a universal speedup.

Historical log labels identify the experiments: H1 sampled overhead, H2
mandatory ownership outside diagnostics, H3 detailed producer history, H4 copied
periodic transport, and H5 world-validation reuse. These labels identify recorded
controls; they are not a remaining-work checklist. Measurement and detail arming
are independent.

# Historical diagnostic observer effect

An early renderer lookup experiment synchronously logged hundreds of thousands of ordinary null probes. The historical report described FPS falling from above 200 to roughly 30. This was an uncontrolled observer-effect report, not a reproducible performance benchmark for the current mod.

The v1.2.12 replacement kept ordinary null handling to a small predicate and atomically limited file I/O to the first missing Shadow/ShadowAlpha pass with index 17 or higher. This demonstrates why frequent expected events require bounded, selectively armed observation: instrumenting the boundary can dominate the behavior being investigated. It does not quantify the cost of current buffered diagnostic paths.
