---
type: Reverse Engineering Reference
title: WD2 Shadow Reference and WD1 Port Boundaries
description: Evidence scope and navigation for the recovered WD2 headlight selector and local-shadow
  renderer.
tags:
- shadow-engine
- wd2
- vehicle-limiter
- admission
- fade
status: draft
sources:
- resource: wd2-headlight-selection.md
  title: WD2 Headlight Owner Selection and Publication
- resource: wd2-local-shadow-pipeline.md
  title: WD2 Local Shadow Admission and Fade Consumption
- resource: ../../../evidence/catalog.json#E-6d160f060501
  title: Knowledge preflight and read-only investigation scope
- resource: ../../../evidence/catalog.json#E-18d2062daaab
  title: Fresh manager Update with stored program identity and instructions
- resource: ../../../evidence/catalog.json#E-ed8bc0525f86
  title: Extracted shipped rendering profiles
- resource: ../../../evidence/catalog.json#E-721a678b08dc
  title: Archived August13 report, provenance rather than current instructions
- resource: ../../../evidence/catalog.json#E-aa3069320e32
  title: Preserved historical technical evidence
---

# Scope and identity

The imported program is Disrupt_64.dll, x 86-64, analysis base `0x180000000`.
Ghidra records SHA256
`1bc77b469a3591bec36b3af41d513f45ba2887bc338276b1388b5dd932ccd865`
and MD5 `95450f97291ddb4e8654f3f584513562` for the imported file. This is stored
analysis-project identity, not a new hash of a running WD2 installation or
proof of a named retail revision. Addresses in these concepts are **WD2
analysis VAs**, never WD1 RVAs or independently validated WD1 hook sites.

Evidence tier is static code/instruction and extracted-config inspection.
It does not establish live WD2 timing, GPU completion, visual smoothness or
performance equivalence in WD1. Draft status preserves those limits.

# Recovered responsibilities

* [Headlight selection](wd2-headlight-selection.md) owns actual Update
 `186a79adb`, lifecycle, local-player/view inputs, distance sorting, angular
 rejection, setting 1 special case and native shadow-only publication.
* [Local-shadow pipeline](wd2-local-shadow-pipeline.md) owns general admission,
 static-map refresh, post-admission ordering, distance fade and the concrete
 LightData shading-parameter consumer. Distance fade is no longer metadata
 only; temporal budget-replacement fading and dithering remain unproved.

Extracted pc0..2 set HeadlightShadowsLevel0, pc3 sets 1 and pc4 sets 2. General
MaxDynamicShadowMaps varies 8/10/12; PC profiles retain 4 static maps at sizes
256/512/1024. These settings are not one-for-one equivalents of WD1 faces,
passes or expanded 30-slot resource capacity. Four one-hot vehicle shadow
group bits are not proof of four separate physical map pools.

# Corrected interpretations

* `186a68c40` constructs the CHeadlightShadowsManager:: Update profiler label;
 it is not Update. Its initializer/getter/table chain now leads to the actual
 dispatcher and Update body, rather than a nearby-function assumption.
* `186df5af0` is vegetation/wind related, not a four-car limiter.
* `186df59a0` configures static shadow-map storage, not nearest vehicle ranking.
* `186da3a60` sorts already admitted renderer records into special-light classes;
 it neither chooses nearest vehicles nor supplies a temporal handover.
* The manager's sixteen initialized sentinel DWORDs do not prove sixteen
 vehicle slots. Recovered Update uses its reference vector at 50/58.
* Selected-for-update cache flags are written before submission, so they are
 not GPU-ready flags. Existing cache IDs are not proved generation-safe.
* A camera-side angular gate is not an occlusion or visible-shadow-receiver test.
* Disable/re-enable writes within one Update do not prove visible flicker.
* CPU light-descriptor copy-on-write is not rendered-shadow caching.
* General-light bHasElectricBackup's emergency-light description does not
 identify a vehicle siren tag.

# What WD1 can take from this

The useful foundation is **owner-aware selection before shadow admission,
shadow-only eligibility, and a separate native shadow-strength path**. A direct
copy of WD2 policy is not justified: it rebuilds the selected list, rejects
near-collinear candidates (including behind previously rejected candidates),
can underfill its allowance, and contains no N+2 or motion-based transition
policy. Those choices can conflict with the reported visible parked-car-shadow case.

WD2 still scans, allocates, sorts and publishes descriptors. No sub-microsecond
manager cost or guaranteed WD1 FPS gain follows from the recovered algorithm.
Its general static cache is a separate fact, not permission to implement the
rendered-shadow caching or atlas changes the design excludes.

WD1 must independently establish its shadow-only eligibility writer, dirty/
publication ownership, current candidate classification, and usable-map fade
consumer before porting that mechanism. Current type 1 logical-budget exclusion
does not prove all siren roles, nor physical headlight/siren pool separation.
See the linked concepts for exact confirmed roles and remaining safety gates.

# Extracted WD2 profile values

The August 2026 extracted configuration distinguishes headlight policy from dynamic and static-map budgets:

| Profile | Headlight level | Dynamic maps | Static maps | Static size | Minimum spot coverage |
| --- | ---: | ---: | ---: | ---: | ---: |
| pc_0 | 0 | 8 | 4 | 256 | 0.001 |
| pc_1 | 0 | 8 | 4 | 256 | 0.005 |
| pc_2 | 0 | 8 | 4 | 256 | 0.0001 |
| pc_3 | 1 | 10 | 4 | 512 | 0.00005 |
| pc_4 | 2 | 12 | 4 | 1024 | 0.00001 |
| pc_5, pc_6 | Not specified in the cited headlight table | 12 | 4 | 1024 | 0.00001 |

The registered headlight description was `0 = OFF / 1 = Only your car / 2..4 = 2..4 cars`; the inspected shipped headlight profiles stopped at level 2. The separate static-map manager accepted count 0–8 and size 32–4096, rebuilding approximately `0x230`-byte records named `StaticShadowMap`. Settings included `AlwaysUpdateNewStaticShadowMaps`, `ShadowOmniSpotMinCoverage` and `SpotsCastShadows`. These are extracted configuration/static-code facts, not live WD2 performance measurements or equivalent WD1 capacities. The old report lacked the selector mapping; the linked newer selector concept supersedes that uncertainty.
