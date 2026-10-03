---
type: Reverse Engineering Reference
title: WD2 Headlight Owner Selection and Publication
description: Recovered headlight Update policy, selected-owner lifetime and native shadow-only
  lamp publication.
tags:
- shadow-engine
- wd2
- vehicle
- selection
- ownership
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-da387975b539
  title: Fresh per-VA decompilation, instructions, data and cross references
- resource: ../../../evidence/catalog.json#E-d5a1a137849e
  title: Constructor and destructor ownership
- resource: ../../../evidence/catalog.json#E-7233d9fe8f10
  title: Named profiler getter and table association
- resource: ../../../evidence/catalog.json#E-58dd84014ecf
  title: HeadlightShadowsLevel registration and help contract
- resource: ../../../evidence/catalog.json#E-ad4735a0faf6
  title: WD1 full-handle classification and N+2 selection
---

# Identity and evidence

Applies only to the imported WD2 program identified in
[WD2 reference](wd2-shadow-reference.md). All addresses are analysis VAs;
object offsets and masks below are hexadecimal unless stated otherwise.
Prose counts and byte sizes are decimal; hexadecimal sizes carry an 0x prefix.
The policy and publication calls are static recovered code, not WD2 live/visual
evidence or WD1-compatible addresses. Export files are named `<VA>.txt` in the
cited directory and include instructions alongside decompilation.

# Manager identity and lifetime

Profiler-label builder `186a68c40` is called by initializer `18832b99c`, storing
the label at 18401bbc8. Getter `186a6fc30` reads it and appears in table 1838f43e8
at+40. Constructor `186a6c568` assigns that table, publishes singleton 18401bac8,
initializes 16 DWORDs at+C..48 toFFFFFC00, zeroes 50/58 and calls
`186a74b70(this,1,0,0)`. Destructor `186a6cf50` unregisters with the same helper,
disposes 50/58 storage and clears the singleton.

`186a74b70` manages registration in an update-dispatch list using 18401bad0,
table 1838f4400 and helper 184f8bca5. Table entry 1838f4438 names dispatcher
`186a79a33`, which sets its busy byte+8, traverses registered objects in 18/20,
calls **`186a79adb` for each**, and clears busy. This establishes the actual
Update body. Update reads no elapsed-time argument and does not use the 16
sentinel DWORDs as a demonstrated selection history.

Selected-owner references belong to the manager vector at+50, with packed
count/capacity metadata at+58. At the next Update it validates each old entity
reference (`ref+10`; entity+A0 bit 4 clear, bit 17 set), resolves CVehicle, and
disables its managed shadow lamps. `184aa98c0` releases the vector's elements,
conditionally frees storage, and zeroes pointer/metadata. Selection is then
rebuilt. This is not an incumbent residence list consulted for ranking.

# Settings and candidate policy

`186ec7db0` registers HeadlightShadowsLevel at descriptor 188; getter
`186ead500` reads argument+188 and Update passes DAT184034630+208. Native help
describes 0 off, 1 player's car, 2..4 that many cars. The body checks 0, special-cases 1,
and otherwise uses the setting as its acceptance target without a local 0..4 clamp.
That does not validate values above 4: the publication helper has only four group bits.

| Setting | Actual Update path |
| --- | --- |
| 0 | Disable old managed shadows and stop. Unlike WD1's current 0-unlimited UI. |
| 1 | Resolve the local player's CPawn-associated vehicle; select it if valid. Not nearest-one on foot. |
| Greater than 1 | Gather eligible nearby CVehicles, sort, angular-filter and select up to the setting. |

Local-player reference chain: `186a4f6c0` -> `186a4f6eb` -> `18509df70`, with
player-state lookup `186a4f7ba`. The returned entity reference comes from that
state's+28. `1866b5c26` reads entity XYZ90/94/98. The special setting 1 path uses
CPawn type getter `184b461a0`, component lookup `1866b38e0` and associated-vehicle
accessors `186ab8ee9`/`186ab5be5`.

The multi-vehicle path asks `1868254a1(DAT184011470,D43DDD1A)` for a category
reference vector, then applies these predicates to valid references:

* Entity-origin distance squared from the player reference is strictly less
 than 900 decimal: a 30-world-unit radius. Metric uses all three coordinates.
* Resolve a CVehicle through `186b89619`; type getter `184b47395` names CVehicle.
* Vehicle byte 264 OR80 is set, and byte 190 OR189 is set; reject enum2BC equal 5.
 Accessors `186b6fc6d` and `1849a961d` supply the latter pair. Exact state/enum
 names are not recovered, so these are not labelled engine-on, siren or class 5.
* Apply the conditional view-angle test below, then create a 24-byte candidate.

# View test, distance sort and angular rejection

The view object is obtained from the first registered entry under DAT18400faf0
via `1867b31f0`. Its position is+C/+10/+14 and axis+4C/+50/+54. Only when
`dot(entityOrigin-viewPosition,viewAxis)<0` does Update test vehicle orientation.
It transforms local(0, 1, 0) through the entity transform (`1866b5b20`, `1851c6563`),
normalizes it and rejects when absolute angular separation from the view axis
in degrees is at least `(view[2C]*57.29578+60)*0.5`. The other half-space bypasses
this orientation rejection. Scalar2C is FOV-like but its named owner is unproved.
Do not call this full frustum, headlight cone or receiver visibility.

Candidate layout:

| Offset | Meaning |
| --- | --- |
| 00 | Borrowed CVehicle pointer during this Update |
| 08/0C/10 | Normalized player-minus-entity-origin bearing |
| 14 | Squared player distance to the transformed point below |

`186a714b0` constructs local `((entity[D8]+entity[E4])*0.5,entity[E8],entity[E0])`
and transforms it by the entity matrix at+60. Update uses this point for the
ranking metric, not the origin used in the 30-unit gate. A bumper, bounds or
headlight-center interpretation remains unproved.

Sorter `186a6a2e4`, insertion leaf `186a69d87` and partition `186a6a53c` compare
only candidate+14 ascending. No motion, old-owner priority, identity tie-breaker
or time field is read. Partitioning can reorder equal metrics; stable ties are
not guaranteed across the whole sort.

Update visits the sorted sequence. The first candidate passes. A later candidate
is rejected if helper `186a71f10` finds **any earlier sorted candidate** whose
metric is strictly smaller and bearing differs by **less than 10 degrees**.
Angle helper `184acfe70` computes signed acos of clamped dot product, with the
sign from a planar cross product; the caller uses the absolute angle.

The earlier-candidate loop includes rejected candidates, not only admitted
owners (instructions 186a7a022..04B; base reload186a7a09E). Example: bearings 0°, 9°,
18° at increasing distances admit only the first; the third is blocked by the
already-rejected second. Consequently the policy can underfill its allowance.
This is an angular redundancy heuristic, not proof that the farther car's
shadow is invisible, occluded or duplicated. Copying it can fail the tester's parked
car / passing traffic visible-shadow requirement.

Accepted owners are retained as native reference-counted entity references
(vehicle+30), then enabled in selected order. The temporary 24-byte candidate
vector is disposed on exit; it does not survive as a prediction or ready queue.

# Shadow-only lamp publication

`186b655f2(vehicle,enable,index)` maps indices 0..3 to masks 2/4/8/10 hexadecimal
(2/4/8/16 decimal); all other indices map to 0. Through vehicle interface+48
virtual+1C8/+1D0 it updates the owner mask as
`(oldMask | 0x1E) & ~selectedMask`. It walks vehicle light records at 170/178,
stride 0x130, and operates only on records whose byte12D is set (`186b50fae`).
These one-hot bits are shadow-group assignments, not physical resource pools.
Their complete self/cross-shadow exclusion semantics are not recovered.

For each tagged light, `186b498d5` invokes:

1. `186673203(component,enable)` to set full light descriptor **L+11**.
2. `18665b02d(component)` to read the current group, then
  `1866756a0(component,(oldGroup & ~0x1E)|mask)` to set **L+74**.

Registration `186bf3270` identifies these as `bCastShadow` and `uiShadowGroup`.
Its property base **P=L+10**, so registered offsets areP+1 andP+64, not another
layout. This path changes shadow eligibility/grouping, not physical light
on/off or brightness; it does not write a temporal fade factor.

Setters resolve writable state through `186bf22b0(component+28)`: first
`186c21ba0` on one handle, then `186c21b50` on the second handle at+38. Lower
`186c191f0` / `186c190f0` compare descriptor pointers in the selected banks,
copying when those pointers alias, enqueue dirtiness
atomically where necessary, reuse or allocate 0x60/0x1A0-byte copies and publish the
writable descriptor. Globals 184020fa0/183e32f00 own bank selection. The read
accessor resolves the component+38 handle through `184a636fd`, which copies
the handle through `186bd1f30` and calls registry resolver `186c54860` on
183E33EF0. Its exact bank-selection rule is not yet established.
Exact per-frame scheduling/locking ownership
is not fully established, but raw writes that bypass this mechanism are not an
equivalent operation. This is CPU descriptor publication, **not cached shadow maps**.

# Managed lamp tag and siren boundary

Vehicle-light setup `186b6b22c` calls `186b80280`, which compares lightdefinition
associated IDs to vehicle attachment/part records (vehicle1E0/1E8, stride0xD0).
For a matching part not rejected by `186b50f82`, `186b4d16a` reads its definition
flags at+90. If lightdefinition byte 51 is zero and part flags contain 2 or 4,
setter `186b58b4b(light,true)` marks light record12D. Getter `1881bafb0` returns
the light definition at record+8; `186b4b590` exposes its association vector+28.

This is a native authoring/attachment-based lamp classifier. Semantic names of
byte 51 and flags 2/4 remain unknown: it is not proof that every siren is excluded.
VehicleLampPreset, VehicleDynamicLightPreset and VehicleParts names in database
unregistration `186ba8de3` do not map those fields. General-light metadata's
"Is an emergency light" describes bHasElectricBackup atE1, not this vehicle
lamp byte 51. Do not reinterpret it as a siren tag.

Other functions containing offset12D (`186b2e992`, `186b3a3c0`, `186b3c3a0`)
operate on different, larger objects, not this 0x130-byte light record.

# Port and performance limits

No N+2, hold timer, approaching-car trend, police priority, incoming-map readiness
or explicit temporal replacement fade appears in this recovered selector and
enable chain. Its per-Update disable/re-enable cycle is not proof of visible
flicker: publication/render timing is a separate boundary. It does perform
reference work, native candidate scans, vector allocation, sorting and angular
comparisons; there is no measured cost or reason to promise sub-microsecond work.

Use its separation of owner policy and shadow-only publication as an architectural
reference. Do not port its numeric offsets, four-bit assignments, rejection rule
or raw descriptor setters into WD1. Current WD1 fail-open full-handle ownership,
world preservation and native light updates remain mandatory. General renderer
admission and the proven distance-fade consumer are in
[WD2 local-shadow pipeline](wd2-local-shadow-pipeline.md).
