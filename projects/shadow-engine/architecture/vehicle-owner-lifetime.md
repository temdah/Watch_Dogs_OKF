---
type: Reverse Engineering Map
title: Vehicle Light Owner and Skeleton Lifetime
description: Sanitized Global ownership chain and remaining lifetime gates before vehicle-specific
  shadow policy.
tags:
- vehicles
- ownership
- skeleton
- lifetime
status: draft
sources:
- id: tracked-retirement
  resource: vehicle-retirement-diagnostics.md
  title: Tracked Vehicle Retirement Diagnostics
- id: batch-proof
  resource: ../../../evidence/catalog.json#E-42554659ff9e
  title: Independent batch byte and regional mapping contract
- id: batch-test
  resource: ../../../evidence/catalog.json#E-f4a82f305d4e
  title: Actual-source ABI, TLS and transaction fault tests
- id: provenance
  resource: vehicle-light-provenance.md
  title: Vehicle Light Component to Renderer Provenance
- id: observer
  resource: ../../../evidence/catalog.json#E-ad4735a0faf6
  title: Existing bounded observer and copied-token safety rules
- id: runtime-229
  resource: ../../../evidence/catalog.json#E-28db6463b490
  title: Three-capture Global owner result and operator-confirmed departure
- id: candidate-229
  resource: ../../../evidence/catalog.json#E-5c12a4e12f45
  title: Owner correlation candidate, preflight and validation
- id: class
  resource: ../../../evidence/catalog.json#E-d08bac4bf506
  title: Global CVehicle class metadata and deleting destructor
- id: retirement
  resource: ../../../evidence/catalog.json#E-fd807ece32a8
  title: Vehicle factory, common teardown and update slot
- id: caller
  resource: ../../../evidence/catalog.json#E-16ccb9c14e8c
  title: Parent update and skeleton construction paths
- id: graphics
  resource: ../../../evidence/catalog.json#E-55d57a0cba77
  title: Graphics class names, skeleton getters and cleanup
- id: skeleton
  resource: ../../../evidence/catalog.json#E-b0817c5c755c
  title: SkeletonObjectUpdate, enclosing construction and common skeleton cleanup
- id: verification
  resource: ../../../evidence/catalog.json#E-abd5652b8b83
  title: Ten independent Global mapped-image and reconstructed-PE checks
---

# Captured Global owner correlation

Three F10 captures completed all four windows with 14, 74 and 84 owner records.
All 172 records matched the enclosing vehicle with flags0x3F and a unique
same-window renderer match. Independent copied-value checks confirm aligned
array membership, the exact native caller and internally consistent owner/
array/skeleton relations. Batch/owner TLS failures, overflow, unreadable probes
and component/handle reuse-or-sharing leads are zero.

Capture 1 contains one police-pattern owner with two headlights and two siren
identities. Capture 2 retains it and adds a separate four-light owner plus seven
type 3-only vehicle pairs. Their components and handles remain disjoint.
The two sampled streetlight controls (different identities across captures)
have zero vehicle-component matches throughout; the second control has two
renderer instances sharing one handle. This is scoped world-light exclusion,
not proof covering every world spotlight implementation.

Capture 3 retains the FIRST captured police-pattern owner with the same array,
skeleton, components and handles; the SECOND owner's four identities are absent
from copied owner and renderer samples. the tester subsequently confirmed driving
away in the original car, resolving the A/B labels and matching this continuity.
Nonobservation still does not prove destruction or native generation.

Capture 3 hits the existing 4096-probe ceiling in all four windows but still
matches every sampled type 1/type 3 renderer row. No sampled headlight/siren
coverage gap is found; this is not an exhaustive vehicle census. Latest auto
lifecycle counters close 4486 external results/3940 resources with zero ownership
errors, stale/late writes or reset-pending. No F9/full-pressure or visual
acceptance is inferred. Dimensions remain 4096.

This establishes capture-time ownership on Global. It does not establish
retirement/replacement/same-address reuse safety. Later production full-handle
publication and .80 driver proof have separate [selection](vehicle-shadow-selection.md)
and [driver](driver-vehicle-identity.md) contracts.

# Diagnostic mechanism introduced in v 2.0.29

The candidate adds one optional 18-byte batch detour while retaining both
component/transform observers, bounded four-window F10, copied lineage and
v 2.0.15 rendering/lifecycle policy. Module 18 owns its target, trampoline,
enabled flag, TLS index and capture-only failure count in the existing context.
No vehicle model database, vehicle scan or persistent owner classifier exists.

| Runtime | Batch RVA | Nested component return RVA |
| --- | --- | --- |
| Global/04DF | 0x0093D730 | 0x0093D8EA |
| VMPless | 0x00517BC0 | 0x00517D7A |
| Complete Edition | 0x01961A60 | 0x01961C1A |
| Asia/Miru | 0x005EF450 | 0x005EF60A |
| A4EE | Unverified; observer disabled | Unverified |

Each location was independently found in its image, not cluster-derived.
Four instruction spans at +0/+0xD9/+0x16D/+0x18C prove argument preservation,
array traversal and nested virtual call. The 18-byte overwritten prologue
contains only complete non-relative instructions. Read-only preflight precedes
transactional installation; missing batch proof leaves older observers intact.
Allocation or write failure follows the existing full transaction rollback.

The pass-through wrapper supplies a stack-local vehicle/skeleton/transform
scope only during F10. A separate TLS slot preserves nested batches. Accepted
bounded owner records copy the vehicle, vtable and array pointer/count at the
native update boundary. Membership uses unsigned subtraction/division/modulo,
not an overflow-prone array end or array scan. Exact caller, skeleton and
transform comparisons reject accidental enclosing-scope association. The
wrapper itself performs no engine-memory probe or logging.

`STAGE_VEHICLE_BATCH_LINK` uses the existing serial/index/epoch to pair copied
owner evidence with component/renderer records. Flags are scope=1, readable
header=2, exact caller=4, skeleton=8, transform=16, membership=32; only 0x3F
reports matched. Summary groups current matched owner pointers. These are
capture-time relations, not retirement/generation proof. No borrowed pointer
reaches the worker for dereferencing. Retry observations retain the initial
owner sample; they do not claim continuously revalidated owner lifetime.

TLS entry/restore failure disables further batch-scope reads, preventing an
expired stack address from becoming eligible evidence. No wait, native
resolver/getter call or engine state write is added. Limiter, resolution,
cache, atlas, admission, capacity and lifecycle remain unchanged.

85 Python tests and four actual-source native harnesses pass, including
nested owner separation, capture integration, caller/array/skeleton/transform/
serial exclusions, TLS failures, and rollback at every one of three detour
writes. Old two-detour fallback remains tested. Warning-clean reproducibility,
compiled version/exports, policy/isolation and four-image gates pass.
These do not establish live hook safety, native generation or visual acceptance.

# Confirmed Global ownership chain

These static Global/supported-04DF mappings are tied to v 2.0.28's runtime
return-address evidence. v 2.0.29 now confirms live batch-owner correlation
within the scope above, without promoting captured pointers to native lifetime authority.

Native class getter `0x009B6630` registers the literal name `CVehicle`.
Vtable `0x02F4A1C0` contains that getter at +8 and update `0x009AB5C0` at
+0x160. The factory at `0x009F0A00` allocates 0x3F0 bytes, calls common
construction `0x0098E9B0`, then installs this table. Other derived tables share
the update: do not turn one exact vtable into an all-vehicle classifier.
[^class][^retirement]

`CVehicle` update `0x009AB5C0` passes the same object to `0x0099E5D0`, which
passes it to light batch `0x0093D730`. The batch traverses the object's light
array at +0x148/count +0x150 with stride 0x130. Its callsite `0x0093D8E7`
invokes component virtual +0x30, with return `0x0093D8EA` observed in all 113
copied v 2.0.28 records. Thus the enclosing argument is a CVehicle owner in this
native path, not merely an arbitrary grouping container.[^caller][^capture]

The batch ABI is `(vehicle, float delta, skeleton, worldTransform,
float distanceSquared)`: RCX, XMM1, R8, R9 and fifth stack argument. This is
different from the nested component update ABI. Parent `0x0099E5D0` obtains
the skeleton through vehicle +0x48 object's virtual +0x140; it obtains the
world transform through the existing entity link. It also applies native
distance/phase-dependent update cadence and delta accumulation. None of that
is a shadow-resolution policy or evidence supporting cadence changes.
[^caller]

# Skeleton is graphics-owned, not a CVehicle base pointer

`CGraphicComponent` class getter is `0x007EF6B0`; its +0x140 getter at
`0x007BD890` returns `[graphic+0x110]+0x1B0` when nonnull. The getter may first
call a state-update helper depending on flags: never invoke it as a read-only
lookup. Construction `0x007E13B0` allocates a separate 0x2E0-byte object and
stores it at graphic +0x110. That object's construction `0x007DD620` installs
the observed table `0x02F13700` at +0x1B0 and is associated with the named
`SkeletonObjectUpdate` job.[^graphics][^skeleton]

There is also an embedded path. `CAnimatedGraphicComponent`, named by getter
`0x007FB300`, constructs the same object at graphic +0x120; its skeleton
getter `0x00784EA0` returns the embedded +0x2D0 address. Therefore subtracting
0x1B0 from a sampled skeleton gets a skeleton/job owner subobject, **not a
CVehicle** and not necessarily an allocation base. The shared table identifies
this interface/type; separate skeleton addresses remain observed instance
grouping keys, with no generation proof.[^caller][^graphics][^skeleton]

# Retirement boundaries and limits

| Global RVA | Confirmed static role | Safety limit |
| --- | --- | --- |
| 0x009EB560 | CVehicle deleting-destructor wrapper, then optional deallocation | Not the only derived cleanup route |
| 0x0098EFD0 | Common vehicle teardown; passes +0x148/+0x150 and 0x130 element size to array cleanup | Complete reallocation/replacement and concurrency coverage unproven |
| 0x007D6E80 | CGraphicComponent cleanup virtually deletes the +0x110 owner | Shared graphics path, not vehicle-only |
| 0x007D7430 | Standalone skeleton/job-owner destruction enters skeleton cleanup at +0x1B0 | Embedded route can inline this wrapper |
| 0x007DB2B0 | Animated graphics cleanup enters common skeleton cleanup on its embedded instance | Does not use the standalone wrapper |
| 0x0033ED00 | Common skeleton cleanup frees backing buffers and arrays | Shared across graphics users, not a vehicle classifier |

Native code owns allocation/destruction. v 2.0.30 observes the common vehicle
boundary through the [retirement diagnostic](vehicle-retirement-diagnostics.md);
these routines are never mod-invoked release functions. A hook on
the standalone skeleton wrapper alone would miss the confirmed embedded route.
No pointer value, refcount, observed absence or copied handle is promoted to a
native generation. Thread ordering, runtime coverage of retirement, array
replacement and same-address reuse are still open.[^retirement][^graphics][^skeleton]
