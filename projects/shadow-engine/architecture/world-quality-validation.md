---
type: Runtime Safety Contract
title: World Quality Validation Overhead
description: H5 same-pass readable-region reuse and identical-hash hoisting with unchanged world-quality
  decisions.
tags:
- shadow-engine
- overhead
- quality
- validation
- ownership
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-8b97f6755321
  title: World-quality pass and stack validation owner
- resource: ../../../evidence/catalog.json#E-ad4735a0faf6
  title: Shared readable-region helper and exact vehicle identity lookup
- resource: ../../../evidence/catalog.json#E-db266d7d5858
  title: Actual-source and frozen-reference equivalence fixture
- resource: ../../../evidence/catalog.json#E-ced926ccad73
  title: Frozen original world and identity functions
- resource: mod-performance-audit.md
  title: Measuring native patch overhead without confusing it with frame cost
- resource: ../../../evidence/catalog.json#E-c681b34977c2
  title: Corrected active-world run, H3/H4 safety and finite-section acceptance
- resource: ../../../evidence/catalog.json#E-7e911445fe1d
  title: Current-working lineage, approval and knowledge lookup
- resource: ../../../evidence/catalog.json#E-8d9b4b980f5d
  title: H5 implementation, equivalence, artifacts and acceptance limits
- resource: ../../../evidence/catalog.json#E-e4a6c568c145
  title: Full sanitized validation and quality ownership contract
---

# Dimension checks and validation history

The .75 world-validation experiment retained quality decisions while reducing
repeated region queries. The later [quality experiment](vehicle-shadow-quality.md) adds a separate optional dimension
proof ahead of payload inspection. Under-cap bypass changes diagnostic coverage,
explicitly labelled as inspectedEntries, while preserving queue mutations.
Failed proof and above-cap requests retain this H5 payload validation contract.
The current Q1 fixture compares frozen 75 output; the historical H5 fixture now
explicitly compares frozen 74 with frozen 75, not the modified current counters.
Q1/Q2 were accepted with engine .77/tools .78. No new native mapping or hook
was required. The detailed preserved-decision section below describes the
frozen .74/.75 equivalence boundary; under-cap entries now skip that inspection.

# Accepted .75 scope and ownership

Version 2.0.75 combined scoped world validation with the .74 diagnostic
producer-closure correction;
no separate .74 game result is claimed. H5 changes neither quality policy nor
native hooks, ABI, profiles, capacity, resource ownership or defaults. The shared
patch source uses the existing renderer layout and exact runtime-profile gates.

`apply_world_shadow_quality` owns one stack `VehicleCopyRegionCache` per call.
Initialization occurs only after the existing enabled/readiness checks and the
existing nonwaiting vehicle-selection token succeed. The scope expires before
unlock/return; it is never reused by the earlier vehicle pass, later capture,
native renderer or next invocation. Module 18's readable-region helper now has
this additional consumer alongside synchronous candidate copies. No mutable
shared cache or second resource owner is added.

The helper stores only successful committed, non-guard/non-noaccess region
bounds returned by VirtualQuery. Every exact requested span must fit within one
such region; adjacent regions are never merged. Failed checks are not cached.
A full cache falls back to fresh validation. Its 128 slots exceed the maximum
60 descriptor/handle checks in this 30-entry pass. Readability does not pin an
allocation: the synchronous queue/payload lifetime remains a prerequisite.
Neither the old nor new check makes arbitrary concurrent unmapping safe.

# Preserved decisions

The pass still reads descriptor 0x44 bytes and the eight-byte spatial handle,
in the same short-circuit order, before type, identity and dimensions. Null
candidates remain uncounted. Missing/unreadable descriptor or spatial payloads
increment skipped_unreadable once. Only types 1 through 4 proceed. Exact vehicle
identities increment skipped_vehicle; ambiguous identities increment
skipped_ambiguous. Missing identities and UINT64_MAX still receive the world
cap. This differs intentionally from the exact-identity vehicle-quality path.

Each dimension remains min(native, cap), with no upscale. In the historical H5 comparison, under-cap records still performed
classification and affected the same skip counters. Mutated entries
and calls retain the same accounting. Entry clamp, lock attempt, separate
vehicle/world publication boundary and policy snapshots remain unchanged.
H5 itself introduced neither a dimensions-first shortcut nor a combined pass.
Q1/Q2 later added the separate optional shortcut above.

`lookup_vehicle_quality_identity` now computes its identical handle hash once
per lookup. Four-bank traversal, age order, tag checks under the selection token, collision probes,
owner conflict/ambiguity rejection and newest accepted distance remain intact.
Missing and ambiguous results still leave output parameters untouched. This is
shared arithmetic cleanup for existing consumers, not a new identity cache.

# Validation and interpretation

The frozen .74 reference contains both original function bodies, with symbol
renames only and the old world pass calling the old identity lookup. The actual
source fixture compares all queue bytes, counters, lock state and identity
outputs, and counts VirtualQuery externally. Protection changes between calls
must be observed by a new scope. Dense and fragmented layouts bound the benefit:
reuse can remove repeated queries only when requested spans share readable
regions. Synthetic timing includes cache initialization; it is not game FPS.

The final fixture passes 1,290 world cases, 16 identity cases and 6,719 checks.
Synthetic shared-region layouts reduce 60 queries to 1 or 2; 60-region fragmented
layouts retain all 60 queries. One host timing run including cache initialization
measures 54.913 to 1.133 microseconds for dense input and 17.384 to 17.849 for
fragmented input. This is a layout-dependent saving, with a small cost in the
fragmented case, not a uniform speedup or game FPS result. Existing quality,
H3/H1/ownership and refactor gates pass; the Internal build reproduces and both
packages match frozen inputs.

The corrected .75 Global capture confirms active 0/4096/4096 and completes
50 manager plus 50 queue samples. The world pass has 320 valid samples, mean
29.796250 microseconds, median 28.8 and p 95 41.9. Its active classification and
exact-vehicle exclusions are recorded with no unreadable/ambiguous skips. Zero
mutations at 4096 is consistent with already-under-cap native requests and does
not indicate a disabled loop. The earlier .75 capture at 4/2048/Original is
excluded from active-world comparison.

This mean is below the two .73 observations (59.481/34.022) but similar to the
.72 baseline (29.119/30.266). Workloads differ; a causal H5 game-performance gain
is not isolated. Frozen-reference equivalence, bounded query savings, the active
runtime and the tester's positive .75 gameplay report support this scoped implementation.
Continuous ownership balances 214151 results with zero inspected failures. The
retained H3 correction and H4 transport pass their tested-scope checks.

These results are limited to the recorded Global control. They do not
establish an all-profile speedup or alter the separate [settings contract](saved-settings.md).
