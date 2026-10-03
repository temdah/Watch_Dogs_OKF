---
type: Reverse Engineering Reference
title: WD2 Local Shadow Admission and Fade Consumption
description: General shadow admission, static refresh, output ordering and distance-fade shading
  parameter ownership.
tags:
- shadow-engine
- wd2
- renderer
- admission
- fade
- cache
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-da387975b539
  title: Fresh ordering helpers, writable descriptors and LightData consumers
- resource: ../../../evidence/catalog.json#E-8f9255a4faf6
  title: Candidate construction, manager admission and downstream work construction
- resource: ../../../evidence/catalog.json#E-2f3b6655344c
  title: Candidate-to-cache matching and refresh policy
- resource: ../../../evidence/catalog.json#E-f41f9de99470
  title: Static cache configuration ownership and clamps
- resource: ../../../evidence/catalog.json#E-3320ed939b72
  title: StaticShadowMap resource naming
- resource: ../../../evidence/catalog.json#E-58dd84014ecf
  title: Light-property registration
---

# Scope and object vocabulary

Static evidence for the imported WD2 identity in
[WD2 reference](wd2-shadow-reference.md); all addresses are analysis VAs.
Offsets and masks are hexadecimal unless stated otherwise. Prose counts and
byte sizes are decimal; hexadecimal sizes carry an 0x prefix.
**L** is a full native light descriptor, **P=L+10** its registered property base,
**C** a temporary renderer candidate. Do not conflate the same numeric offset
on these different objects or transport them into WD1.

The pipeline is owner lamp eligibility -> candidate/fade construction ->
general shadow admission -> cache/update work -> lighting submission. The
[vehicle manager](wd2-headlight-selection.md) sets L+11 and L+74 before this
general path. Candidate eligibility is not synonymous with an admitted map,
submitted update, completed GPU result or visible shadow.

# Candidate factor producer

`186e2a620` allocates a candidate through `186d91450`, stores L atC+8 and the
pose atC+10, and initializes **C+70=1**. For enabled local-shadow light types
other than 0/2 and not the rain-occlusion flag, it combines:

* An optional clamped 0..1 value selected from context+30's four-float bank by
 **L+30 / P+20**, registered as `iShadowFadeFactorCurveIndex`.
* A distance factor with max distance **P+150** and fade length
 **P+150 * P+154**: `saturate((maxDistance-distance)/fadeLength)`.
 Fade length at/below native cutoff 0.001 (DAT183517578) produces a hard
 distance cutoff instead.

Distance is between a supplied pose-offset point and context XYZ; its complete
caller-owned camera/player meaning is not independently established here.
The configured fade is distance attenuation, not elapsed time after a vehicle
changes admission status. The result is published in the native candidate list.

Accessors: `186bf0040` readsP+150; `186befff0` returnsP+150*P+154;
`185bf3f00` returnsP+20. Raw setter `186bfbe80` clamps the curve index to[-1, 3].
Registration also pairs a fade accessor with `186bfbe60`, whose recovered
instruction writesP+168, not the product read by `186befff0`. Do not assume
calling a similarly named reflected setter changes computed fade length;
the intervening authoring/serialization contract is unresolved.

Context builder `186e2b450` resolves a rendering-global object through 183e33370
and token 183e33470, then copies floats+130/+134/+138/+13C into context+30..3C.
Initializer `18832ee10` constructs that registry and initializes the token to-1.
Registry table183920DC0's `186bd34d0` acquires a token through `186c4a1a0` into
owner+110 (183E33470 for this singleton); `186bd3ac0` releases it through
`186c4ce90` and restores-1. `186c00a30` and raw `186c0d050` are shared registry
forwarding functions, not named fade writers. `186c4a1a0` allocates an0xFB0-byte
payload and invokes initializer `186bd0760` when no existing payload is supplied.
That initializer zeroes the four floats at 130..13C. This closes payload/default
ownership, not the runtime writer that supplies animated factors.
The runtime writer/semantic owner of those four values is not established. Their existence
does not prove temporal headlight handover. Another matching-offset lead,
`186bd01a0`, initializes 21 repeated float 4 tuples; caller `1869c35c0` embeds
that array at its own+178. This is not evidence of a four-factor bank writer.
`186dc4c90` instead drives physical
light intensity/day-night/curve/flicker using the separate L+2C index; it must
not be repurposed as a shadow-only transition control.

# General admission and resource ownership

`186e24e40` consumes a linked sequence of C records and produces 24-byte output
records: candidate pointer+0, optional static-cache record+8, update-selection
byte+10. It checks shadow eligibility, type, positiveC+70, normalized coverage-
likeC+80 and configurationC10. Budget comes from MaxDynamicShadowMaps atBF0;
helper `186ead7f0` returnsBF0+2*390. Admission decisions use incoming order;
the later output sort is not a nearest-car prioritizer.

The static-cache branch matches candidate IDs to manager-owned 0x230-byte records
in vector 98/A0. Relevant fields: ID60, integer update age 64, update flag 68.
Unmatched slots become unused (ID=-1). `186dbd1c0` reuses such a slot or grows
below configured countA8, constructing a named StaticShadowMap through
`186dbc2d0`. New entries receive candidate ID, age 10000 decimal, flag 0.

Refresh selection updates those counters/flags. ManagerB1 can select new entries
immediately; when no branch selected an update, greatest age chooses one. Age
is not proved seconds, ID is not proved generation-safe, and flag 68 is written
**before** GPU submission. None is a GPU completion or incoming-ready fence.

`186df59a0` owns cache reconfiguration: countBF4 is clamped 0..8 -> managerA8,
sizeBF8 clamped 32..4096 decimal -> AC, BFC -> B1. Relevant configuration changes
rebuild storage. This is a static shadow cache, not the selected-owner list.
It remains reference-only; no WD1 rendered-shadow cache is established by it.

Downstream `186e2c3a0` attaches existing flagged cache data atC+68 where usable;
the output record's update byte controls new work. It constructs 0x2500-byte work
records and calls `186dc4440`, then `186e1d310` (`Spot Shadow Visibility`).
These functions prepare visibility/clip/caster submission. They do not establish
that an incoming map has finished rendering or provide a temporal budget fade.

# Post-admission ordering

`186da3a60` sorts already admitted 24-byte output records, with predicate:

```
A before B := (A.C.L.flags70 has bit31) OR (B.C.L.type12C == 0)
```

The flag's explicit names are RainOcclusionShadow / Alpha / Delta in
`186e279f0`; type 0 enters the 3/4-cascade builder `186dc2b40`. The comparator does
not read vehicle owner, distance, camera, motion or residency. It groups special
renderer classes; it does not determine which ordinary vehicles win the budget.

Insertion leaf `186d9b330` handles small ranges. Larger paths use
`186d998b0`, `186d99190`, `186d9fac0`, `186da00c0`, `186d99e50`, `186d99d60`,
`186d9ba80`, `186da99e0` and `186d9fba0` for sorting/merging with that same
predicate and intact three-QWORD record moves. `186e322a0` lazily allocates
temporary 24-byte-item sorting storage and halves its request on allocation
failure; that count is **not shadow capacity**.

Ordinary unflagged, nonzero-type records keep relative input order across the
inspected paths. Do not claim blanket stable strict ordering: two flagged or
two type 0 entries can compare before each other under this predicate. Most
importantly, budget allocation happened before this sort.

# Fade reaches actual lighting parameters

`186d526a0` consumes C+8 light, C+10 pose and C+68 shadow record. When the shadow
record exists and has a resource pointer at+40, it binds shadow matrices and
resources, then writes **(C[70], 1-C[70])** into render block **+290/+294**.
Exact pairs occur at 186d54982..991 and186d54FA8..FB7. This is not an unused
candidate scalar or merely a hard eligibility test.

The register-relative stores are+260/+264 because R15 was set to block+30 at
186d53D29. `186d526a0` allocates 0x410 bytes and initializer `186dabe30` assigns
descriptor1840323E0.
Initializer `188333f80` registers callback `186dcd3d0`, naming the binding
**LightData**, data **LightDatas** with registration offsets+30/+40, and textures
**LightShadowTexture** (header3B0/resource3B8) and **LightShadowTextureNV**
(header3C0/resource3C8). Header-relative
offsets 260/264 are not established shader constant-buffer offsets: the factor
pair is 250/254 relative to the separately registered data start+40. The absolute
object offsets 290/294 are unambiguous. The block reaches lighting draw submission
via `186c6b850`. This closes the CPU distance-fade-to-shading-parameter path.

The complementary pair is consistent with blending shadow visibility toward
fully lit, but final shader formula, dithering pattern and temporal filtering
have **not** been recovered. Do not present those as proved. Likewise, a nonnull
CPU resource pointer is not a GPU-completion fence. A fade needs a usable shadow
candidate/resource to remain attached; removing eligibility and then changing
a scalar cannot by itself preserve the outgoing shadow.

# Unresolved boundaries and safe WD1 application

No demonstrated path connects a vehicle losing its selection slot to a timed
fade, replacement-map readiness or physically separate siren pool. The headlight
selector's shadow-only setter does not write the fade bank. General distance
fade and static refresh are independent mechanisms, not evidence of N+2 handover.

Before a WD1 fade intervention, independently recover its shadow-only factor
producer, exact lighting consumer, object ownership, native overrides, usable-map
lifetime and scheduling boundary. A visible outgoing shadow must remain rendered
within the finite N+2 resource budget while its factor changes; the next
candidate being classified is insufficient evidence of readiness. No new wait,
atlas, cache, capacity expansion or direct foreign setter follows from this evidence.
