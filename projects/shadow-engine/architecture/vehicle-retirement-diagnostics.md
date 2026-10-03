---
type: Reverse Engineering Map
title: Tracked Vehicle Retirement Diagnostics
description: Common CVehicle teardown boundaries and bounded copied-owner lifetime evidence.
tags:
- shadow-engine
- vehicles
- retirement
- lifetime
- diagnostics
status: draft
sources:
- id: implementation
  resource: ../../../evidence/catalog.json#E-c7f7f2e2c610
  title: Bounded tracked-owner observer
- id: independent-validator
  resource: ../../../evidence/catalog.json#E-61d9c236ca50
  title: Independent four-profile boundary validation
- id: native-harness
  resource: ../../../evidence/catalog.json#E-f4a82f305d4e
  title: Actual-source retirement and transaction fault harness
- id: owner-map
  resource: vehicle-owner-lifetime.md
  title: Vehicle Light Owner and Skeleton Lifetime
- id: runtime-230
  resource: ../../../evidence/catalog.json#E-1f997976aba7
  title: Two-capture Global enrollment with no tracked teardown event yet
- id: evidence
  resource: ../../../evidence/catalog.json#E-0ecd5a4ed0be
  title: Preflight, independent mapping and validation evidence
---

# Tracked vehicle retirement diagnostic

v 2.0.30 retains v 2.0.29 owner capture and v 2.0.15 rendering/lifecycle policy.
It adds one optional common-teardown observer. This is diagnostic evidence,
not a persistent vehicle classifier or native generation identifier.

## First Global runtime result: two captures

The installed v 2.0.30 candidate and Global profile match. Two complete F10s
produce 28/65 exact owner correlations and 2/10 current vehicle groups.
The lifetime registry grows 2 to 11 owners, with 93 exact sample links and
zero gaps/overflow, teardown entries/returns, changed tuples or reappearance.
One initial police-pattern owner persists; the other is merely unobserved.
Nine new traffic owners enroll only in capture 2.

This proves live enrollment/snapshot linkage and hook installation, NOT
execution of the common-teardown callback. No all-calls counter exists, so
untracked invocation cannot be inferred. Retention, delayed cleanup, pooling
and alternate paths remain possible but unproven. No native generation or
complete retirement coverage is established.

The captures were about 20 seconds apart; this does not establish whether
cleanup should have occurred. Hook entry/return and alternate lifetime coverage
remain unobserved, so repeated absence is not proof of destruction.

Latest automatic shadow lifecycle balances 34963 results and 29240 resources,
with zero stale/late, store/release/orphan failure or reset-pending. Not an F9
or full-pressure visual gate.

## Native boundary and evidence

The common CVehicle teardown accepts one vehicle pointer and returns void
(Windows x64 ABI). Static Global class/decompilation evidence identifies the
role; four independently mapped images agree on the entry, light-array cleanup
and base-teardown tail. Global installation and capture linkage now work live;
tracked native teardown execution remains unobserved, as detailed above.

| Runtime | Common teardown | Array cleanup callee | Base teardown callee |
| --- | --- | --- | --- |
| Global/04DF | 0x0098EFD0 | 0x000BA290 | 0x007CE970 |
| VMPless | 0x00569460 | 0x0011E170 | 0x002E5060 |
| Complete | 0x019B3300 | 0x0011ACA0 | 0x0174A0D0 |
| Asia | 0x00610DA0 | 0x0010BEE0 | 0x00204AD0 |

The native array cleanup receives the vehicle light-array header at +0x148,
count at +0x150 and element stride 0x130. The final tail targets base teardown.
These callees are static semantic mappings, not APIs called by the patch.
The common boundary is reached from the deleting wrapper and multiple derived
cleanup routes; coverage of every derived path and live array replacement is
not established. Return means common teardown returned, NOT allocation freed.

Runtime preflight checks image bounds through +0x37C and exact spans at
+0x0 (37 bytes), +0x2BF (27), +0x2E1 (13), +0x355 (35).
The independently validated first 18 bytes contain complete non-relative
instructions and are the only overwritten span. Immutable profile data owns
regional RVAs. A4EE has no mapped observer and stays disabled/unverified.
Missing new boundary proof preserves previous owner diagnostics. Installation
uses the existing transaction and rollback; every four-hook write failure is
tested. Static byte success does not replace affected-profile manual tests.

## Ownership, synchronization and consumers

The separate vehicle_lifetime subsystem owns at most 128 copied owner records
for the process lifetime, with no eviction. Only fully matched F10 batch-owner
samples enroll an owner. Numeric vehicle, vtable, array and skeleton tokens
are copied; no retained token is dereferenced. No all-vehicle scan is added.

A single-attempt CAS grants exclusive diagnostic access. Contention skips only
the observation and increments cumulative gaps; it never waits on the engine.
The observer finds already-enrolled numeric owners, records an entry ticket,
releases diagnostic access, invokes native teardown exactly once, then records
its return using that ticket. No object reads, logging, resolver/release calls
or held diagnostic token cross the native call. Nested different-owner calls
are supported; same-owner overlaps are explicit.

States: 0 sampled, 1 common teardown entered, 2 common teardown returned.
Monotonic observation sequences order copied samples and teardown events;
they are NOT native generations. Reappearance after state 2 and changes to the
copied vtable/array/count/skeleton are investigation leads. A missed return
does not manufacture state 2. Sequence exhaustion, contention and full storage
are visible exclusions, not evidence of safe lifetime coverage.

The existing F10 worker takes one bounded frozen snapshot under the token,
then releases it before formatting. Live records may advance while logging;
throughSequence identifies the cutoff. Existing renderer/component/owner/
lineage output is retained. No engine resource is owned by this subsystem.

## Markers and acceptance

- STAGE_VEHICLE_LIFETIME_OBSERVER: boundary enablement and tracked cap.
- STAGE_VEHICLE_LIFETIME_LINK: original F10 owner index to slot/observation sequence.
- STAGE_VEHICLE_LIFETIME_SUMMARY: snapshot availability, cutoff, gaps and overflow.
- STAGE_VEHICLE_LIFETIME_RECORD: copied identity, state, enter/return sequences,
 counts, ticks/threads, overlap, changed-tuple and reappearance leads.

All markers keep generationProven=0 where lifetime is summarized. Lack of a
sample is not destruction. Nonzero gaps/overflow limit conclusions; a full
table never silently replaces an old pending owner.

Offline gates: 90 Python tests, four actual-source native harnesses,
warning-clean reproducibility, source policy, rollback faults, four mapped
regional byte gates (71 core checks each plus independent observer spans).
A4EE remains manual-required. No live or visual acceptance is inferred.

The historical test compared two simultaneous active owners, then driving
away and later traffic. That route did not guarantee destruction or address reuse.

Retained: all prior diagnostics and render/lifecycle policy. Changed: one
optional numeric-token teardown observer and bounded F10 snapshot. Removed:
nothing. Regressed: no offline failure found; runtime unknown. No limiter,
2048 tier, cache, atlas, traffic control, admission or capacity change.
