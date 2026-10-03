---
type: Runtime Policy Contract
title: Vehicle Shadow Quality Boundary
description: Exact vehicle-owned renderer request cap with world and uncertainty passthrough.
tags:
- shadow-engine
- vehicles
- headlights
- sirens
- quality
- resolution
status: draft
sources:
- id: vehicle-tier-result
  resource: ../../../evidence/catalog.json#E-3fbd10671774
  title: Distance-tier implementation and validation
- id: implementation
  resource: ../../../evidence/catalog.json#E-ad4735a0faf6
  title: Vehicle identity publication and renderer quality policy
- id: renderer
  resource: ../../../evidence/catalog.json#E-9a4ab6c06cd6
  title: Synchronous renderer-queue consumer
- id: tests
  resource: ../../../evidence/catalog.json#E-f4a82f305d4e
  title: Actual-source synthetic quality-policy harness
- id: resource-map
  resource: headlight-resource-diagnostics.md
  title: Headlight Shadow Resource Diagnostics
- id: preflight
  resource: ../../../evidence/catalog.json#E-772ef57aaeb2
  title: Quality and police-tag preflight
---

# Publication ownership (.79 experiment)

`publish_vehicle_quality_identity` is called only by the token-owning batch
publisher. All production readers (vehicle quality, world quality and workload
capture) acquire the same `vehicle_selection_lock`. Its atomic acquire/release
owns record visibility; epoch tags are validity labels, not an independent
seqlock. Build 79 removes redundant tag atomics inside this writer while retaining
the tag values/clear-payload-publish sequence, probe order, ambiguity, overflow,
full handles, bank lifetime and nonwaiting fallback. Readers stay unchanged.
This reduces publication work at 0 as well as positive limits, without changing
quality output. Frozen 77 full-state/atomic-operation tests cover the mechanism;
source inspection establishes the lock requirement across callers. Future
readers must hold that same token. No native identity mapping changes.


# Current fixed-cap processing

The dimensions-first and coverage experiments in engine .77/tools .78 optionally proves dimensions first in
each separate quality pass. Requests within both axes of their cap skip payload
and identity inspection; failed proof follows the full original path.
Classification counters describe `inspectedEntries`; F10/workload attribution
remains independent. Frozen .75 differential checks prove unchanged queue output.
The [saved-settings owner](saved-settings.md) supplies applied policy; no separate
Apply action or static active/default label is part of the current tools.

Vehicle quality caps only exact recent vehicle-owned type 1/type 3 requests at
512/1024/2048/4096, or preserves original requests when bypassed. Module 16
publishes limit/cap/bypass atomically; the consumer samples cap and bypass once.
Quality-only edits do not reset residency. Every dimension is min(native, cap),
so selecting 4096 never upscales a lower native request. Unknown, ambiguous,
conflicting, shared and world handles retain native requests.

Queue request dimensions are+0x20A4/+0x20A8; the native synchronous renderer uses
them to acquire a shared texture and writes resource metadata+0x40/+0x44. Capped
queue fields remain through the call and are not restored afterward, avoiding
a request/resource metadata disagreement; native construction overwrites them
on record reuse. A new larger cap relies on native resource rebuilding, never
forced release or mutation of an acquired texture.

Publication commits up to 64 validated observations after native batch return,
under one shared nonwaiting token and one renderer epoch. Readers cannot see
intermediate bulbs from a successful batch. Four-epoch expiry remains; lock miss
preserves native requests. The original equal epoch tags did not synchronize
same-epoch ambiguity writes, motivating the .39 shared token. No token crosses
a native renderer call. .79 removes only redundant publisher tag atomics while
all readers remain token-owned; tags are validity labels, not a standalone seqlock.

The .83 C1-D3 cleanup removes the temporary .80–.82 driven-car quality exemption.
The selected cap again applies to every exact vehicle-owned type1/type3 request,
including the driven car. Limiter protection remains a separate identity consumer.
Quality caps requests in its existing nonwaiting token without a driver lookup or
staged second pass. The quality registry no longer stores the full entity ID used
only by that exemption; full descriptor handles, owner ambiguity and epoch checks
are retained. The selection registry still owns its full entity IDs and rechecks.

Actual policy/owner/decision evidence remains available through
`STAGE_VEHICLE_QUALITY` and `STAGE_VEHICLE_QUALITY_RECORD`; obsolete driver-only
quality trace fields/outcomes are removed. Original/request/resource dimensions
remain independently captured. SE7 tools require no update.

The actual-reader fixture proves zero driver memory reads during quality, both
cars capped to512, and a fresh driver-role5 limiter match afterward. Frozen quality
and publication comparisons retain lower requests, unknown/world passthrough and
atomic publication behavior. These are offline results; the subsequent .83 cleanup report also confirms
correct operation in its tested Global scope. No measured FPS gain is inferred.

# Historical experiments and proof limits

The initial .38 policy fixed 2048; .41 exposed all four caps and covered 88 combined
settings. .45 experimented with distance 4096/2048/1024 then native outside,
staged ends 10/20/40 m and explicit Apply; that mode is retired from current fixed
controls. Every historical tier used min(native, tier). A preserved Global
renderer branch reuses backing resources, so distance transitions still require
upstream invalidation and both-direction request/resource proof. A requested cap
alone does not prove a texture resized; no mismatch follows from static code alone.

Samples retain selected policy alongside per-record requested and post-native
CPU resource dimensions. These are configuration/CPU metadata, not GPU descriptor
or visible-fidelity proof. Four regional consumers are independently mapped;
A4EE remains manual-required. Offline exact mutation, lower-request preservation,
world/ambiguity passthrough and publication tests do not establish all-scene FPS
or visual correctness. .82 driver identification and temporary quality separation were confirmed in
the tested Global case; the .83 normal-quality cleanup is accepted by its subsequent user report.

Entity `bPolice` and light-preset `bEmergency` data exist, but no stable runtime
CVehicle field bridges those tags into the proven owner token. Active type 1
siren-like evidence cannot classify a police vehicle with siren disabled. Police
priority stays disabled; renderer type is not a substitute for class/lifetime proof.
