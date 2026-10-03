---
type: Engine Layout Contract
title: Shadow Capacity Layout
description: Coupled formulas and invariants for local maps, queue records, embedded mapping
  arrays, passes, and allocation size.
tags:
- shadow-engine
- capacity
- queue
- maps
- passes
- layout
status: stable
sources:
- id: private-low-admission-runtime
  resource: ../../../evidence/catalog.json#E-80ca190daaa8
  title: Low-admission 30-map Global visual and automatic-log result
- id: private-capacity-isolation-candidate
  resource: ../../../evidence/catalog.json#E-81823303ce73
  title: 30-map capacity with B4 held at 16
- id: private-clean-configuration-runtime
  resource: ../../../evidence/catalog.json#E-e2766fed405b
  title: Clean current-code original-configuration intersection control
- id: private-original-configuration-comparison
  resource: ../../../evidence/catalog.json#E-1fc0008298b1
  title: Current implementation with original-v1.2.0 configuration
- id: private-native-consumer-audit
  resource: ../../../evidence/catalog.json#E-e803a31b3859
  title: Bounded Global native consumer audit
- id: private-parity-audit
  resource: ../../../evidence/catalog.json#E-1260c58419aa
  title: Original-v1.2.0 to v2.0.11 known patch-surface audit
- id: private-constants
  resource: ../../../evidence/catalog.json#E-176d7aee808c
  title: Capacity constants and relocation table
- id: private-expansion
  resource: ../../../evidence/catalog.json#E-f45567a3ad24
  title: Engine expansion implementation
- id: private-validator
  resource: ../../../evidence/catalog.json#E-e36d4c66ae9b
  title: Independent capacity validator
- id: private-archived-audit
  resource: ../../../evidence/catalog.json#E-ce0dceb9a20f
  title: Historical 16-to-24 capacity audit
- id: public-historical-capacity-audit
  resource: https://github.com/temdah/Shadow-Engine/blob/2082a3bec1bfc4213ae4572b0e14b4f20c17906b/docs/okf/engine-patch-validation-audit.md
  title: Historical public 16-to-24 capacity audit
- id: cloth-constants
  resource: ../../../evidence/catalog.json#E-6d95aa568f93
  title: Capacity constants and relocation table
- id: cloth-expansion
  resource: ../../../evidence/catalog.json#E-d9694ed25b9c
  title: Engine expansion implementation
- id: cloth-validator
  resource: ../../../evidence/catalog.json#E-9848c23a92f8
  title: Independent capacity validator
- resource: ../../../evidence/catalog.json#E-c38ab69eeed1
  title: Preserved historical technical evidence
---

# Native layout and coupled counts

The native engine owns 16 local maps and 17 physical queue entries. The extra
entry preserves the special long-range job. For a target of `M` local maps:

* physical queue entries = `M + 1`;
* queue index-array clear bytes = `4 + 4M`;
* external map count = `M - 16`;
* external slice-result count = `M - 17`.

Pass 16 is `LongRangeShadow`. Maps below 16 retain their native pass index;
local map `m >= 16` uses pass `m + 1`. A capacity change must update map-loop
construction, handle routing, pass routing, result routing, queue immediates,
allocation size, and all 46 recovered embedded references as one contract.
[^public-constants][^public-expansion]

# Three independently growing queue regions

One local-map record occupies `0x24C0` bytes, but the fields following the
record array do not all move by that same amount. Starting from the native
16-map offsets and adding `E = M - 16` maps:

| Region | Native offset | Formula |
|---|---:|---:|
| First mapping array | `0x270D0` | `0x270D0 + E * 0x24C0` |
| Second mapping array | `0x27114` | `0x27114 + E * 0x24C4` |
| Count and later tail fields | `0x27158` | `0x27158 + E * 0x24C8` |

The first mapping contributes four bytes per added map before the second
boundary; both mappings contribute eight bytes before count/tail/result fields.
For 30 maps (`E=14`), the authoritative offsets are first mapping `0x47350`,
second mapping `0x473CC`, count `0x47448`, tail `0x47450`, result `0x47460`, and
allocation end `0x47470`.[^public-constants]

v1.2.2 incorrectly applied `0x24C8` to all 46 relocations. Its queue populated,
but both native and external `SliceExecute` counters stayed at zero and all
shadows were absent. v1.2.3 assigns each old embedded value to its owning
region and the validator rejects a uniform-stride derivation.[^public-validator]

# Pass-table envelope

The verified shadow category is `0x0C`. Its native registry provides 64 slots
and a stored maximum key of at least `0x3F00`. Added maps require paired
`Shadow` and `ShadowAlpha` objects and therefore two physical slots per map.
The 30-map target uses passes 17-30, slots 34-61, and maximum key `0x3D0C`, all
inside that proven envelope. Do not exceed it without independently recovering
the allocator, lookup, finalization, and every consumer.[^public-expansion]

# Derivation rule

Never infer a capacity formula from only one old/new total. Partition the
object by every intervening variable-length region, classify each relocation
by its original field, and make the offline validator derive expected values
independently of the candidate table.


# Controlled capacity and admission evidence

These isolation results constrain capacity hypotheses; they do not
establish all-scene runtime safety.

| Control | Physical maps / queue entries | B4 / A8 | Extra handles / added pass slots / external results | Result and limits |
| --- | --- | --- | --- | --- |
| .12 comparison | 30 / 31 | 25 / 4 | 14 / 28 / 13 | Intersection capture requested up to 33 faces with 19 clamped submissions. |
| .13 original-configuration control | 24 / 25 | 16 / 4 | 8 / 16 / 7 | Global intersection clean; peak requests 24, detailed window 22, peak candidates 217, zero observed clamps/drops and balanced lifecycle. |
| .14 capacity isolation | 30 / 31 | 16 / 4 | 14 / 28 / 13 | No reported black flicker, slightly more pop-in. 9,998 current-generation external results balanced with zero rejection/stale/late/release failures; residency reached 22 faces and 220 candidates. High maps 24-29 and full-run clamps were not established. |
| .15 intermediate admission | 30 / 31 | 21 / 4 | 14 / 28 / 13 | Stable Global intersection/bridge report; peak requests 29, detailed window 27, zero clamps/drops. CPU occupancy beyond 24 does not prove every high-index GPU consumer or overflow behavior. |

The 24-map target has first/second mappings 0x396D0/0x39734, count 0x39798, tail 0x397A0, resource context 0x397A8, result 0x397B0 and allocation end 0x397C0. It requires 50 pass slots and maximum key 0x310C. The 30-map resource context is 0x47458; it requires 62 pass slots with maximum key 0x3D0C. Owner reserve remains 8, native result storage 17, LongRange pass 16 and registry capacity 64 in both.

All 46 .13 targets match the original v1.2.0 source. The .14 target matches all .12 capacity targets and differs only in module-00 version/B4/comments; .15 likewise isolates B4=21 from .14. Explicit independent validation targets are --policy-target-v120, --policy-target-30-b4-16 and --policy-target-30-b4-21, alongside the retained original 30-map target. The .14 native checks, 43 Python tests, reproducibility and four-profile 71-check corpus gate passed; A4EE runtime remained unverified.

The controls implicate admission or enabled work rather than expanded allocation alone, but do not prove B4 itself, physical clamping or any particular GPU consumer caused the flicker. High admission must not be paired with undersized storage or partially reverted relocations. Lower admission can restore earlier pop-in limits.

# Known-site parity

Original-v1.2.0 to .11 comparison retained constructor expansion, all 46 queue relocations, three handle consumers, two pass consumers, two indexed-result relays, coherent scheduler bounds, owner reserve, whole-record face protection and null face-cost protection. Normalized function comparison retained manager/guard/lookup/store mechanisms. Historical pre-render repair hooks were already uninstalled in v1.2.0; removing their dead code did not remove an active fix.

Runtime confirmed 14 distinct extra handles and 28 distinct added pass objects. Original retest queues used 21/24 faces without a clamp marker; .11 used 30/30 with 901 cumulative clamps and 1,149 trailing entries dropped by the third capture. Exact captured queues fit, and no event marker identified the flicker instant. No dropped record was linked to the affected world light.

Known-site parity and balanced result ownership do not prove all native count, mask, reader, refresh or sampling assumptions support 30 maps. Re-enabling dead repairs or bypassing guards has no established corrective basis.

# Independent native consumer audit

Static Global-image inspection independently recovers 46 anchored instruction
references to known old queue offsets; every one is already relocated. The
renderer at `0x306E60` follows the relocated queue count and each entry's face
count, rather than a residual fixed 16/24 loop. Its byte-mask shift at
`0x3085C8` uses the within-entry face index, not the global map cursor.
This is bounded static evidence, not a full computed-alias/GPU audit.
[^private-native-consumer-audit]

Global constructor `0x3D5920` initializes 17 eight-byte name objects in each
of the arrays at `+0x1490` and `+0x1518`. Setup `0x3E1A20` uses these for
native ShadowAlpha/Shadow registration, including LongRange. Added names live
in patch-owned resource state and feed added registry slots through module 60;
these native name arrays are not a forgotten physical pass-table expansion.
Do not extend their constructor loops into adjacent fields.
[^private-native-consumer-audit]

Per-entry constructor `0x2D5EA0` constructs four subobjects of stride `0x820`;
this is not a four-map global limit. The existing sanity guard's acceptance of
counts up to six does not establish safe native five/six-face layout. Latest
manual entry observations contain only one/four faces. The supported face-count
domain remains a research question, not an attributed flicker cause.
[^private-native-consumer-audit]

No omitted global capacity patch was identified. Five unanchored raw byte
matches, computed-base readers, unvisited callees and GPU binding/sampling
remain outside the proof. The current build and policy were not changed.
[^private-native-consumer-audit]


[^public-constants]: Capacity constants and relocation table
[^public-expansion]: Engine expansion implementation
[^public-validator]: Independent capacity validator
[^private-native-consumer-audit]: Bounded Global native consumer audit

# Historical owner-vector reallocation failure

The historical cache-owner expansion exposed a storage-lifetime invariant distinct from its logical A8 ceiling. Cache owners occupied contiguous `0x700`-byte records, and manager admission published raw pointers to those records in temporary candidate descriptors. The old configuration reserved physical space for four owners but allowed eight logically. Its fifth owner allocation could move the vector after earlier pointers had already escaped within the same admission pass.

The v0.7.7 repair used the engine's native reserve routine before admission to provide eight records while preserving already-constructed size and contents, then verified size/capacity before allowing the larger workload. Later captures observed no base movement during admission. This historical logical-eight test does not change the current logical-four policy: pre-reserved capacity eight and A8 describe different quantities. A dynamically growable vector is not evidence that mid-pass growth is safe after element pointers are published.
