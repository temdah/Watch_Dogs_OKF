---
type: Validation Reference
title: Known Failure Boundaries
description: Rejected assumptions and runtime signatures that constrain future Shadow Engine
  changes.
tags:
- shadow-engine
- failures
- regressions
- diagnostics
- safety
status: draft
sources:
- id: expansion
  resource: ../../../evidence/catalog.json#E-f45567a3ad24
  title: Current expansion safety checks
- id: historical-regressions
  resource: https://github.com/temdah/Shadow-Engine/blob/2082a3bec1bfc4213ae4572b0e14b4f20c17906b/docs/okf/experiments-and-regressions.md
  title: Historical public regression ledger
- id: historical-crashes
  resource: https://github.com/temdah/Shadow-Engine/blob/2082a3bec1bfc4213ae4572b0e14b4f20c17906b/docs/okf/crash-investigation.md
  title: Historical public crash investigation
- id: pipeline
  resource: ../architecture/shadow-pipeline.md
  title: Shadow Engine Pipeline
- id: regressions
  resource: ../../../evidence/catalog.json#E-1eefc2abcbab
  title: Historical experiments and regressions
- id: crash-audit
  resource: ../../../evidence/catalog.json#E-9196ad8b12df
  title: Historical crash investigation
- resource: ../../../evidence/catalog.json#E-d9694ed25b9c
  title: Current expansion safety checks
- resource: ../../../evidence/catalog.json#E-c38ab69eeed1
  title: Preserved historical technical evidence
---

# Hard boundaries

* Renderer type 3 is shared by vehicle and world spotlights; class-wide filtering
 removes valid world shadows.
* `B4`, `A8`, candidate count, queue records, and cumulative faces are different
 quantities. None is a synonym for physical map capacity.
* Raising logical owner limits without pre-reserving the contiguous owner vector
 can move `0x700`-byte records after raw pointers were published.
* Pass 16 is reserved for `LongRangeShadow`; extra local maps skip it.
* Added pass objects must exist before table finalization. Missing key `0x220C`
 identified absent pass 17; later demand can similarly expose the next absent key.
* Late shadow-map construction is outside the proven safe lifecycle.
* Native inline slice results stop at index 16. Indices 17+ require external
 result storage and balanced consumption/release.
* `PostCallObjectRenderers` schedules frame-graph work; it is not a completion
 barrier.
* Render-record release RVA `0x003C1350` is also too early. v 2.0.3 crossed the
 bridge without crashing but accumulated 20,130 stale and 11 late completions
 by the second F9 capture, with visual, audio, and frame stutter.
* Calling the native resource wrapper after `ExecuteFrameGraph` returns is
 rejected: v 2.0.2 balanced ownership but produced Windows Application Hang 1002.
* The first native result-wrapper call with a non-empty external mask is not a
 complete barrier. v 2.0.4 balanced ownership and avoided crash/stutter but
 ended with 25,945 stale and 13 late completions. Map loop-exit/last-result
 ordering before moving the consumer again.
* Static recovery maps the later pre-finalizer sequence at Global `0x003E19E3`,
 after three additional resource-wrapper submissions. v 2.0.5 runtime rejects
 it as a complete barrier: 17,496 stale and 10 late completions remained with
 rapid bridge headlight/shadow turnover. Static instruction order does not
 prove asynchronous worker completion.
* Rejecting a non-null Slice result without submitting its matching native
 release drops an acquired resource. A rejected store is fail-closed only
 when that ownership is explicitly retired.
* All 46 queue relocations do not share one stride. The uniform-stride v 1.2.2
 candidate populated queue data but dispatched zero shadow jobs.
* Unknown or ambiguous executable builds remain read-only and fail closed.

# Disproven shortcuts

Do not repeat these conclusions without new ownership evidence:

* type 3 equals vehicle headlight;
* a direction-matched lamp pair proves a common vehicle owner;
* more cached owners produce more high-resolution shadows;
* near-full face occupancy proves the face guard clamped work;
* a successful allocation or registration proves downstream consumption;
* absence of a shutdown marker proves a crash;
* a uniform delta across one old/new layout pair proves every embedded region.

# Diagnostic signatures

* All shadows absent, queue populated, zero native/external result stores:
 inspect map/pass lookup and queue mapping before changing capacity again.
* Coarse or low-cadence world shadows with cached owners saturated and no face
 clamp: inspect manager admission/cache competition.
* Missing pass key followed by reset fault: inspect construction timing, full
 pass range, and table finalization.
* Any stale, late, or rejected completion after the frame-graph repair: capture
 the complete log. Exact rejected cleanup can contain the leak while an early
 completion boundary still produces degraded churn.
* A reproducible ground-local intersection blink remains unattributed. Its
 v 2.0.4 capture coincided with full 30/30 face pressure and active clamp/drop
 behavior, but not with the later stale/late burst.
* `rejectedNonNull` unequal to `orphanReleaseResources` plus
 `orphanReleaseFailures`, or any nonzero orphan/release failure: unmatched
 resource ownership; stop the release test.
* Owner base movement during admission: stop; published pointers may be stale.

Use the [pipeline](../architecture/shadow-pipeline.md) to find the first broken
stage and compare it with a frozen known-good log.[^pipeline]

[^current-status]: Current project status
[^expansion]: Current expansion safety checks
[^historical-regressions]: Historical public regression ledger
[^historical-crashes]: Historical public crash investigation
[^pipeline]: Shadow Engine pipeline

Stale/late diagnostic counts alone do not establish a crash. Balanced accepted
and rejected ownership can contain resource loss while revealing an invalid
publication/completion boundary; retain both facts without calling clean ownership
complete asynchronous safety.

# Historical controls that did not establish a capacity limit

The v1.2.5 diagnostic path traversed transient post-admission pointers even with tracing disabled. Gating that traversal in v1.2.6 did not eliminate the crash, so the diagnostic change alone did not identify or repair the remaining failure. Its maximum observed cache count of 16 initially suggested a fixed-width limit, but allocator inspection instead found a dynamic vector governed by A8; reaching 16 was not proof of a physical allocation boundary.

The same report described a descriptor resolved from a light object's handle at `+0x50` and then used without a null check. A missing descriptor explains the immediate invalid use; stale/unregistered ownership was a hypothesis, not an established upstream cause. Different earlier crash addresses, including an apparent mid-instruction address, likewise did not prove a single failed capacity comparison.

A v1.2.7 control selecting four generic type-3 records avoided the reproduced failure despite 163 raw candidates. That bounded observation did not establish four as an engine maximum or make class-wide filtering safe: world spotlights also used type 3. A separate traffic-enabled v1.2.2/B4=21 retest reproduced an earlier object-reset fault without coarse fallback. It associated heavier enabled work with failure in that old implementation; it did not prove B4 alone caused the corruption.
