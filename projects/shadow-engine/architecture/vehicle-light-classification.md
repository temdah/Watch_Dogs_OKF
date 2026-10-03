---
type: Research Plan
title: Vehicle-Light Classification Boundary
description: Evidence and safety boundaries for distinguishing vehicle lights from world Spotlight3
  candidates in quality and selection processing.
tags:
- shadow-engine
- vehicles
- headlights
- spotlight3
- classification
- diagnostics
status: draft
sources:
- id: owner-lifetime
  resource: vehicle-owner-lifetime.md
  title: Vehicle Light Owner and Skeleton Lifetime
- id: light-provenance
  resource: vehicle-light-provenance.md
  title: Vehicle Light Component to Renderer Provenance
- id: retirement
  resource: vehicle-retirement-diagnostics.md
  title: Tracked Vehicle Retirement Diagnostics
- id: diagnostic-module
  resource: ../../../evidence/catalog.json#E-ad4735a0faf6
  title: Bounded F10 vehicle-light capture implementation
- id: pipeline
  resource: shadow-pipeline.md
  title: Shadow Engine Pipeline
- id: admission-review
  resource: ../../../evidence/catalog.json#E-bab653b27bc5
  title: Source and native provenance review of admission-time classification
- id: controlled-toggles
  resource: ../../../evidence/catalog.json#E-db74c94881aa
  title: Six Global controlled light captures and transient-freeze review
- id: historical-control
  resource: ../../../evidence/catalog.json#E-4c3b0033377e
  title: Archived validated traffic-control provenance
- resource: ../../../evidence/catalog.json#E-c38ab69eeed1
  title: Preserved historical technical evidence
---

# Classification authority

Vehicle headlights and world spotlights converge as renderer type 3. Type alone,
flag 0x80, direction-matched pairs, adjacent IDs, descriptor pointer equality or
spatial tuple similarity cannot authorize suppression. Current production uses
the [native batch provenance](vehicle-owner-lifetime.md), full generation handles
and bounded coherent publication described in [selection](vehicle-shadow-selection.md).
The historical .30 admission review identified the requirements below; it is
not a current claim that the classifier remains unimplemented.

Candidate copying exposes next, descriptor and spatial pointers, without a
mapped direct CVehicle backlink in those fields. This does not prove that no
backlink exists elsewhere. The batch supplies borrowed owner/caller/skeleton/
transform/array-membership evidence only until native return. Global update
`0x0099E5D0` conditionally enters batch`0x0093D730` with distance/phase-dependent
cadence; fresh publication cannot be assumed every rendered frame.

The original focused F10 collects matching updates during 100 ms after a completed
renderer sample. Its epoch is neither a game frame nor publication generation;
a retrospective unique match cannot prove that ownership was available before
admission. Current selection therefore publishes independent scalar evidence
before manager classification instead of treating later F10 matches as earlier
successes. A complete same-frame table alone would still miss unchanged,
update-skipped lights.

# Lifetime and uncertainty

Readability of an old owner pointer does not establish identity or exclude
concurrent replacement. Repeated address/array/vtable equality cannot exclude
same-address reuse. Hysteresis retains preference, never stale classification
authority. Full 64-bit descriptor generation protects ordinary slot reuse, but
handles may be shared across spatial instances, requiring uniqueness/conflict
checks. Native copy/lookup resolvers may allocate, change dirty state or publish
buffers; they are not safe guessed read-only admission APIs.

Missing, expired, shared, conflicting, unreadable or incomplete ownership must
preserve native behavior. Arbitrary millisecond TTLs do not prove native lifetime.
A nonwaiting copied snapshot synchronizes patch records, not native allocations.
Headlight groups require current complete evidence; no all-vehicle census,
per-model database or invented Spotlight 4 type is needed. Type 1 vehicle ownership
is distinct from semantic siren classification and physical resource isolation.

Earlier eligibility writes would additionally need writable-versus-published
ownership, every relevant writer/consumer, dirty propagation, invalidation and
exact fail-open/rollback behavior. [WD1 eligibility](wd1-shadow-eligibility.md)
records the remaining gap. A destructor hook is one possible invalidator, not a
mandatory goal when the handle publication lifetime already establishes safety.

# Diagnostic boundary and controlled evidence

The original F10 manager capture reads at most 256 nodes synchronously, preserves
native list order/count, then annotates copied values from 0x18-byte native
bindings after admission. Four windows at 500 ms spacing normally complete over
1.5 s; one worker writes frozen copies, no deferred pointer reads. Captures have
no fixed session count, but busy presses are ignored until flush completes.
`observedTuple` is intentionally unnamed: earlier direction/position claims
require actual native field-consumer proof.

The .15 Global control recorded six four-window captures (24 samples/160 records):
wilderness off/headlights/sirens, then the same states beside a world light.
Headlights add two admitted type 3/0x80 candidates; sirens add one or two type 1/0x80
candidates depending on flashing. Two background spatial identities persist in
all streetlight states. Mixed sirens also change background membership, so set
subtraction alone does not isolate a universal siren tag.

World-associated lights share type 3/0x80 with headlight leads. Stationary vehicle
descriptor/spatial pointers alternate; other descriptors are shared. These are
controlled correlations for one vehicle, without resource dimensions or native
generation fields, not proof of 4096→2048 safety. Later focused-handle/owner
captures and generation recovery are recorded in the linked concepts.

Useful controls compare the same car/camera off/on, motion, a separate world
light and simultaneous vehicles. Light persistence during car-off supports a
world hypothesis; movement with the car supports a vehicle hypothesis. Neither
becomes actionable without native attachment/publication ownership. Traffic
isolation is tooling, not classifier logic; it does not suppress every special-
event vehicle or establish native scene completeness.

Quality, camera/receiver visibility, siren roles, native capacity and resource
lifetime remain separate questions. Unknown passthrough protects world lights
without guaranteeing their survival under native capacity competition.

# Historical approximate classifiers and conservative fallback

The v1.2.17 prototype used player coordinates supplied through NexusTools, consecutive left/right light IDs and nearby world positions as an approximate vehicle-pair discriminator. Unknown records and incomplete pairs remained eligible; missing player position restored full native passthrough. These rules limited the effect of uncertain classification but did not establish a common vehicle owner or native lifetime.

Its first reported test had valid player coordinates, but the attempted component-registry query recognized no candidates in that renderer state. Full passthrough was therefore the intended safety fallback, not evidence that distance ranking had failed. The capture showed provisional component handles `430C0000`/`43430000` on vehicle-labelled records and `43820000` on observed world spotlights. The v1.2.18 prototype combined those observations with complete consecutive-ID/proximate pairs. Those captured handle values were not universal type or ownership identifiers; current exact-owner publication supersedes the approximation.
