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
- id: retired-policy-migration
  resource: ../../../evidence/catalog.json#E-shadow-baseline-20261004
  title: Retired experiment removal and settings migration fixtures
- id: background-runtime
  resource: ../../../evidence/catalog.json#E-shadow89-runtime-20261004
  title: Preserved Global background1024 population capture and unchanged onset report
- id: background-query-review
  resource: ../../../evidence/catalog.json#E-19eafa0c5c81
  title: Occlusion-query mapping and bounded background-quality experiment
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

# Optional background request quality (.89 experiment)

The fixed selected vehicle cap remains the foreground policy. An independent
setting defaults Off and can cap distant vehicle-owned type3 spotlights at
512 or1024. This is a request-size experiment, not an admission/pop-in fix and
not proof of police/headlight semantics for every type3 light. Type1, world,
unknown and ambiguous identities never receive this additional reduction.

The existing synchronous quality boundary reads one atomic policy word.
Background bits20..21 encode Off/512/1024; value3 is invalid. Background remains
independent when the main vehicle setting is Original. Each dimension stays
`min(native request, enabled selected cap, applicable background cap)`. It never
raises a lower native request. Off retains the fixed-cap path without a driver
identity/position lookup; a 3,141-case frozen comparison preserves its output.

While enabled, copy the proven driver identity and local-player position before
acquiring the existing nonwaiting selection token. Unknown or on-foot driver
state disables extra reduction for that pass; this first experiment does not
claim on-foot activation. Preserve selected quality when either owner or full
entity ID matches the driver. Global driver/anchor proofs bound activation;
other profiles do not gain guessed offsets.

For each exact quality owner, walk only the existing descriptor-hash chains
across four renderer epochs. Require full vehicle/entity identity, fresh finite
position, age at most500ms, no conflicting generation/owner, no tagged
publication gap/overflow and no observed publisher in flight. Records are copied
scalars; retained owner addresses are never dereferenced. The index is bounded
by four banks of512 slots. Failed evidence preserves the ordinary selected cap.

A separate context-owned128-slot scalar history, also protected by the selection
token, keys full owner/entity identity. Enter distant quality at distance>=60,
return to selected quality at distance<=50, and retain the prior choice between
those thresholds. Distances use existing entity coordinates; metre units are
not established. Histories expire after500ms, reset on configuration change or
loss of the pass-wide driver/anchor proof, and fail open when full. No dynamic
allocation, new hook, capacity change, descriptor write or forced resource
release is added. The selected thresholds are experiment parameters, not native
engine limits.

Actual-source fixtures cover both caps, paired spotlights, driver protection,
Original, both hysteresis directions, stale/ambiguous/missing identities and
positions, publisher/token conflicts, table saturation and ID/clock reuse.
Persistence/menu fixtures cover versioned transport and failures. These prove
CPU decisions only. The historical backing-resource reuse caveat below still
applies: native request/resource transitions in both directions and visible
fidelity require runtime acceptance. No FPS improvement is claimed.
[^background-query-review]

## Observed request/resource behavior

One preserved Global .89 run with background1024 enabled contains all1,200
manager and1,200 queue samples over60 seconds, without missing buckets or
partial packets. All27,318 recorded queue rows have matching requested and
post-native CPU resource dimensions;2,294 rows specifically change a native
4096 request to1024, with1024 resources. Consecutive sampled full handles also
show transitions back to4096. These are repeated observations, not counts of
unique shadows or uninterrupted resource histories.[^background-runtime]

The human report says the stark draw-in remained and coverage was too short.
The experiment's50/60 thresholds only choose quality inside the existing native
range. They do not extend the maximum range. Reduced texture size also creates
no extra admission slots:58,926 ordinary-eligible candidate observations in
this capture are unbound. The sampled result cannot identify which of these
caused a particular visible pop, prove GPU completion, establish FPS, or accept
the separate512/Off/restart cases.[^background-runtime]

An outer low-resolution band reaching twice the original maximum requires a
separate native distance-eligibility change. Its reference must be the original
range, not an arbitrary quality-switch threshold. The [native producer and
lighting consumer](wd1-shadow-eligibility.md) explain why enlarging request-size
thresholds alone cannot implement that behavior.

[^background-runtime]: Strict capture decoding, copied settings/status/logs and user observation; preserved ASI matches its experimental delivery. CPU resource evidence is not visual acceptance.

## Retirement boundary

The .91 cleanup removes this distance-based runtime policy, its history and its
menu controls. Ordinary fixed caps continue to apply uniformly to proven vehicle
owners, including the driven car. The experiment's request/resource observations
remain useful evidence: they establish reduced dimensions in one run, not extra
admission capacity or a pop-in fix. Retired saved bits are handled by the bounded
[settings migration](saved-settings.md). The cleanup retains per-light diagnostic
observations for future research; offline equivalence is not visual acceptance.
[^retired-policy-migration]

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

[^background-query-review]: Actual-source policy/persistence/menu fixtures and source hashes for the opt-in request-size experiment; no game execution.

[^retired-policy-migration]: Preserved pre-cleanup source and actual-source baseline fixtures; both native builds reproduce offline, with no game acceptance inferred.
