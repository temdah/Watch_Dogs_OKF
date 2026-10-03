---
type: Internal Diagnostic Contract
title: Vehicle Cost and Movement Observation
description: Bounded CPU timing, copied movement trends, admission reasons and quality-skip
  evidence without policy changes.
tags:
- vehicles
- diagnostics
- performance
- shadows
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-85cf818e5411
  title: Capture-owned clocks and frozen-copy movement analysis
- resource: ../../../evidence/catalog.json#E-ad4735a0faf6
  title: Candidate and resource sample ownership and freeze observations
- resource: ../../../evidence/catalog.json#E-f4a82f305d4e
  title: Actual-source synthetic observation and unchanged policy tests
---

# Scope

The separate [workload capture](workload-capture.md) now uses a three-second
lead-in and five-second recording window (originally ten seconds in .62).
It measures successful presentation cadence independently of renderer calls,
retains these four-window reports, and records linear native-distance trends.
The later Global player-position proof and bounded approach policy are recorded
in [incoming readiness](incoming-vehicle-readiness.md). The derivative fields
described here retain their historical native-distance meaning.

Internal 59 retains 58 selection/quality policy and the unchanged Global Lua
repair. Existing 58 tools and the vehicle-sample action request four paired
manager/renderer windows across roughly 1.5 seconds. No new menu, key, native
hook, engine address, camera input or predictive selection is introduced.

Module 18 owns snapshot clocks and frozen-copy analysis. Manager and renderer
tickets hold the existing capture lock until completion; the worker formats
only completed copied data. Timings call QPC only for active sample tickets.
No per-call timing or per-job file output occurs outside those windows.

# What each capture measures

* STAGE_VEHICLE_COST: elapsed CPU-side wall time for limiter preparation,
 native manager call and candidate-link restoration; settings, candidates,
 suppressed/admitted counts and sampled freeze state accompany the timing.
* STAGE_SHADOW_COST: native renderer submission elapsed time, sampled world
 enable/cap and quality-lock-skip deltas across that sample interval.
 Asynchronous completion and GPU rendering are not included.
* STAGE_VEHICLE_ROPE: up to 32 representative vehicle lights per sample in
 candidate order, joined to the preceding sample by full light handle and
 owner. Unique recent observations and 50..2000 ms publication-adjusted
 intervals are required. Negative squared-distance derivative means closing,
 positive means opening. This is not linear speed, smoothing or predicted
 time-to-arrival. Unknown/absent observations do not infer a direction.
* Admission reason distinguishes unknown binding results, native admission,
 policy-kept/native-omitted, disabled/fail-open native omission and policy
 exclusion during complete/degraded evidence. It reports one representative
 light, not whole-vehicle visual truth. Existing protected-group summaries
 and queue/resource records remain available.

The residency lock owns additional Internal freeze streak counters. They use
the existing sample tick, do not alter selection, and track observed consecutive
degraded calls plus their elapsed span. Reset/count changes clear the current
streak; peak counters are cumulative. Lock-unavailable calls cannot observe
that state. Streak duration is not proof a particular vehicle was delayed.

Quality-lock failure counters increment only on the existing failure paths.
Sample deltas can include concurrent calls; they do not identify a particular
light as skipped. Existing native/request/post-return resource dimensions must
be correlated to investigate low/high-resolution flicker. These are CPU resource
metadata, not independently captured GPU texture descriptors.

# Interpretation and testing limits

Four calls are a bounded probe, not a statistically representative frame-time
profile. Same-scene comparisons require unchanged settings and equivalent workloads. Capturing itself
adds copying and can perturb registry contention; preparation timing excludes
the preceding manual snapshot, but not all observer effects. Missing timers or
frequency report -1 rather than zero. No FPS improvement is claimed.

Vehicles absent from the incoming candidate list cannot be diagnosed from these
records alone. More than 32 owners can truncate movement rows. The diagnostic
can locate useful leads, not promise complete explanation in a single run.
Native fade, configurable distance controls and GPU timing remain distinct
research boundaries; prediction itself is described by incoming readiness. The Lua repair's outstanding startup/lifecycle gates remain.
