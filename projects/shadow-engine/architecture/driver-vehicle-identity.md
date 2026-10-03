---
type: Runtime Identity Contract
title: Current Driver Vehicle Identity
description: Optional Global full-ID and driver-seat validation for selection and vehicle quality.
tags:
- shadow-engine
- vehicles
- driver
- identity
- lifetime
- compatibility
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-54ba79f66f80
  title: Global 80 proof activation and sampled gameplay safety
- resource: incoming-vehicle-readiness.md
  title: Incoming Vehicle Shadow Readiness
- resource: vehicle-light-provenance.md
  title: Vehicle Light Component to Renderer Provenance
- resource: ../../../evidence/catalog.json#E-7fe07b671ec3
  title: Immutable Global direct-predicate instruction spans and class IDs
- resource: ../../../evidence/catalog.json#E-b03034d9a7bb
  title: Fault-contained read-only current driver identity
- resource: ../../../evidence/catalog.json#E-ad4735a0faf6
  title: Copied full-ID publication and selection/quality consumers
- resource: ../../../evidence/catalog.json#E-3b328e15d7eb
  title: Preserved named GetCurrentVehicleEntityId and GetDriverID registration table
- resource: ../../../evidence/catalog.json#E-51afa7248b9f
  title: Global instruction evidence and separately identified local CRT export
- resource: ../../../evidence/catalog.json#E-1352c139f3db
  title: Reproducible read-only proof export from the existing Global capture
- resource: ../../../evidence/catalog.json#E-d45752b7873b
  title: Captured-span, metadata, profile-isolation and byte-fault checks
- resource: ../../../evidence/catalog.json#E-4d85852a0d8b
  title: Explicit optional profile coverage
- resource: ../../../evidence/catalog.json#E-ddc2a9521b6d
  title: Live C1-D1 failed pawn-owner comparison
- resource: ../../../evidence/catalog.json#E-102a0034307d
  title: Static direct CPawn driver predicate and receiver proof
- resource: ../../../evidence/catalog.json#E-45d8515a6ae4
  title: Instrumented actual-reader synthetic cost fixture
- resource: ../../../evidence/catalog.json#E-c63739873329
  title: 81 actual-reader allocated-fixture cost baseline
- resource: ../../../evidence/catalog.json#E-b10f21ea8b6e
  title: 82 actual-reader allocated-fixture cost comparison
- resource: ../../../evidence/catalog.json#E-7672703021a6
  title: Global82 driver quality separation and sampled limiter admission
---

# Scope and evidence

The .82 C1-D2 reader implements the Global direct CPawn driving predicate.
It replaces the .80/.81 keyed-association route whose pawn-owner equality failed
in all four captured finite-limit lookups. Static native evidence, fault/race
fixtures and reproducible builds support the correction. A later Global capture
confirms four successful selection and four quality lookups at limit1/extras0:
eight driver-headlight rows retain native/request/resource4096 while another
vehicle is capped to512. The visual report agrees. Full transition coverage and
FPS non-regression remain unproven; reported traffic flicker belongs to the
[selection/admission review](vehicle-shadow-selection.md).

Only `supported-04DF` has an optional `DriverIdentityProfile`. The other four
profiles retain ordinary policy. No driver RVA uses a shadow relocation delta.
Full entity IDs are 64-bit generation-bearing values; CVehicle addresses are
separate comparison tokens, never a substitute for those IDs.

# Native mapping

All addresses are Global RVAs. The owning source/profile and evidence IDs above
provide exact spans and reproduction inputs.

| Role | Mapping and evidence |
| --- | --- |
| Local player | Existing `006F1D95` binding reads root array element 0 -> controller+8 -> data+10 -> reference `{full ID, entity}`. This identifies the local player, not the camera or nearest car. |
| Pawn ownership | CPawn+10 refers to its owning CEntity/full ID. Global `00948460` accesses CPawn+40 as separate state; it does not establish equality with the player CEntity. |
| Direct driving predicate | `00948370–00948451` reads CPawn+90 vehicle reference, requires vehicle entity+60 bit16 set and bit3 clear, obtains CVehicle and compares the first role-1 seat occupant full ID against the pawn's ID. |
| Receiver proof | `00AE6530–00AE6578` obtains CPawn using its class metadata/query ID before calling the direct predicate. This proves the receiver independently of the API name. |
| Class identity | CPawn initializer `009B5A10` supplies `03B874C4 = 911DD85F`; CVehicle initializer `009B6630` supplies `03B87A34 = 8B611803`. Initialization can be lazy. |
| Component lookup | `00849270` uses entity+68 component array, +70 count and +78 cache. `0086DF50` searches eight `{class ID,index}` pairs, then backing pairs at cache+40/+48, and changes LRU order. The patch only copies existing pairs and bounds-checks indices. |
| Actual driver | `0093DEF0` scans CVehicle+1F8/count+200, stride90, for the first role-1 seat at+48; `00B9B3E0` reads its full occupant ID at+58. This must equal the fresh pawn/player ID. A vehicle reference alone cannot distinguish driver from passenger. |
| Batch identity | The owned vehicle-light batch copies CVehicle+10 reference+0 full vehicle ID alongside its numeric CVehicle token. Conflicting full IDs invalidate the join. |

Startup validates eight immutable instruction spans (893 bytes) covering the
direct predicate, its CPawn caller, both class initializers, component lookup/cache,
and driver-seat/occupant helpers. `DRIVER_IDENTITY_READY` reports static proof,
not a successful current-driver lookup. Mutable class IDs are checked per lookup,
allowing later initialization to recover. No CRT export or entity-manager proof
is needed by this reader.

# Ownership and failure contract

`driver_copy` uses self-process `ReadProcessMemory`, requires complete copies and
rejects invalid arithmetic. One synchronous lookup checks fresh player/pawn
reference agreement, direct vehicle reference and native flags, cached CVehicle
ownership and the first driver-role seat. Referring pointers, full references,
component containers, flags, root and seat are rechecked before publication.

When two fields refer to the same reference object, the reader reuses its initial
scalar copy and performs one full recheck while checking both referring fields.
Distinct references receive separate validation. Small adjacent root/seat fields
are copied together without widening the allowed object bounds.

All live addresses remain local to the lookup. There are no native resolver calls,
reference creation, cache writes, pinned objects or cross-call driver cache.
Rechecks detect observed changes; they do not provide atomicity or native lifetime
ownership. Defensive budgets are256 components/cache entries and64 seats, not
claims about native capacity. Missing caches, uninitialized class IDs, failed or
partial reads, excessive counts, mismatches or changed containers return unknown.
Ordinary policy then applies; no nearby vehicle is guessed to be the driver.

# Consumers and diagnostics

Selection resolves fresh identity per classification and joins both full vehicle
ID and CVehicle token before excluding the driver from traffic ranking, resident
slots and patch headlight suppression. The .83 C1-D3 cleanup retains this reader,
its full-ID publication and limiter policy unchanged.

The temporary .80–.82 quality exemption served the now-confirmed driving test.
In .83 the selected vehicle cap applies to the driven car too. Quality no longer
calls the driver reader, stages driver-dependent cap decisions or stores the
extra quality-table entity ID. Selection retains its own full-ID records.
No request is upscaled; the [ordinary quality contract](vehicle-shadow-quality.md)
retains its exact-owner/handle and uncertainty boundaries.

Selection traces still capture actual lookup rejection stages and driver identity
without added native reads or per-call logging. Frozen records serialize on the
worker. Quality's policy/owner/cap outcomes remain in `STAGE_VEHICLE_QUALITY` and
`STAGE_VEHICLE_QUALITY_RECORD`, with existing native/post-policy/resource dimensions.
The session-only extra-slot toggle remains compatible with SE7 tools; it changes
traffic extras, not physical maps. Admission, capacity, scheduling, resource reuse
and fade remain independent.

The opt-in workload separates `driverIdentity` and `driverPublication` CPU intervals.
In .83 these belong to selection/diagnostic classification and vehicle batches,
not normal quality processing. Do not add child intervals to their enclosing
parents. Inactive Internal probes have only the ticket/gate cost and no QPC calls;
Release compiles them out.

# .82 cost evidence and .83 cleanup limits

The actual-reader fixture uses46 memory reads for a successful .82 lookup versus
69 for the corrected-ownership .81 success fixture. Across five4000-call rounds,
Internal medians were13.1996 versus18.765075 microseconds; Release medians were
13.49595 versus18.85985. Instrumentation and host scheduling are included; native
game bodies and the new call-site measurement probes are not. These are synthetic
reader costs, not frame times or FPS results. The live .81 rejection returned
after18 reads, so a comparison against its successful fixture does not establish
less work than that failed gameplay run. Pre-driver .79 had no identity reader.

Two fixed-policy Global82 windows at1/512/4096 measure driver lookup means
17.85/21.00 microseconds at242/267 calls per second, and publication means
3.515/3.525 microseconds at3023/3994 calls per second. Multiplying sampled means
by call rates estimates15–20ms of CPU-side elapsed work per second across these
two non-nested categories. This is neither thread CPU time nor per-frame critical
path cost. Publication dominates the measured driver-related work. The visual
report found no slowdown; unavailable presentation capture and no matched baseline
leave small FPS changes unresolved. Current build inputs match the tested candidate.

Full-ID publication still adds four reads per vehicle batch, including limit0.
It remains necessary for exact limiter identity joins after the quality exemption
is removed. Deferring copies until the first valid observation within the same
batch is an unmeasured opportunity, not part of this cleanup; no cross-call driver
cache is introduced. On .82, broad0/4096 publication bypass was additionally unsafe
for the temporary quality exemption because4096 is not a proven native ceiling.

The .83 actual-reader integration proves zero driver-reader calls during quality
while fresh limiter identification remains intact. Removing a quality-only lookup
and its payload reduces source work; it does not establish an FPS gain.

The .82 reader fixtures passed539 checks in each build mode, covering driver/passenger,
entry/exit/switch, alias/distinct references and injected read/race failures.
The integrated fixture uses the actual reader, batch observer, publisher and
quality policy; only the native batch body is stubbed. Startup proof fixtures
pass1868 checks in each mode with zero external module/export queries. Static
profile checks reject every proof-byte and metadata mutation and preserve
five-profile isolation. These do not prove live transition or visual behavior.

# Historical failure and superseded route

The .80 stable Global run activated proof but did not capture a matched driver.
The .81 finite-limit capture rejected `pawnOwner/entityMismatch` four times with
`driverValid=0`; retained headlights were ordinary rank1/role1, not driver-role5.
Captured quality requests were4096 and under cap, so they do not negate the
separately reported512 visual failure. Settings changed during the workload
window, preventing a performance comparison.

The removed route assumed `CPawn+40 == player CEntity` and also reread the final
association through `player.entity`. The separate-state native mapping disproves
that premise; removing only the first guard would not correct the route.
Historical API evidence remains: table030026A0 names `GetCurrentVehicleEntityId`
(wrapper01422560, adapter011F1100, helper009485A0); table03002690 names `GetDriverID`
(wrapper01422550, adapter011F0EC0, helper0093DEF0).

The old association helper reads CPawn+40 state, owner+7E8/key0362B75C=FD1BA782,
and a map via01757DC0/009BBC30 (owner+7F8, table+10/count+18,16-byte slots,
payload+10 full ID). Historical entity lookup0018B620 uses03B5B1A8 and a hashed
full-ID chain;001A55D0/001B6EF0 may create references. Its signed quotient/remainder
hash used127773/16807/2836 and an exact MSVCR100 div proof. Those mappings remain
provenance, not active dependencies. The .82 production reader removes their
traversal, proof spans and unused data rather than retaining an inactive fallback.
