---
type: Architecture Reference
title: Shadow Pressure Boundaries
description: Evidence separating manager admission, cached-owner retention, and renderer face
  capacity.
tags:
- shadow-engine
- shadows
- admission
- cache
- capacity
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-shadow-budget-20261004
  title: Retained Global .89 admission, face occupancy and nominal single-face area reanalysis
- resource: https://docs.unity3d.com/Packages/com.unity.render-pipelines.high-definition@17.0/manual/Shadows-in-HDRP.html
  title: Unity HDRP 17 adaptive shadow resolution, atlases and mixed caching
- resource: https://docs.unity3d.com/Packages/com.unity.render-pipelines.high-definition@17.0/manual/shadow-update-mode.html
  title: Unity HDRP 17 independent cached-shadow update modes
- resource: https://dev.epicgames.com/documentation/en-us/unreal-engine/movable-light-mobility-in-unreal-engine
  title: Epic movable-light shadow cache benefits and invalidation limits
- resource: https://dev.epicgames.com/documentation/en-us/unreal-engine/megalights-in-unreal-engine
  title: Epic stochastic many-light rendering and its quality and integration tradeoffs
- resource: ../../../evidence/catalog.json#E-077cac7a56c4
  title: Global87 whole-pass population binary
- resource: ../../../evidence/catalog.json#E-3724261dfc5f
  title: Global85 unmarked population tail, native boundaries and coverage/cost limits
- id: intermediate-policy
  resource: ../../../evidence/catalog.json#E-176d7aee808c
  title: Current fixed-admission comparison constants
- id: manager-source
  resource: ../../../evidence/catalog.json#E-6658abb69696
  title: Shadow manager and owner-profile module
- id: renderer-source
  resource: ../../../evidence/catalog.json#E-9a4ab6c06cd6
  title: Renderer queue diagnostics module
- id: matrix
  resource: ../validation/regional-runtime-matrix.md
  title: Regional Runtime Matrix
- id: historical-capability
  resource: ../../../evidence/catalog.json#E-3692bba09cf6
  title: Proven Shadow Engine capabilities and historical pressure findings
- id: engine-policy
  resource: ../../../evidence/catalog.json#E-f45567a3ad24
  title: Engine expansion and B4 policy module
- id: knowledge-log
  resource: ../../../evidence/catalog.json#E-b679c9f441cb
  title: Public Shadow Engine engineering log
- id: intermediate-runtime
  resource: ../../../evidence/catalog.json#E-1903832ba6a6
  title: Stable Global intermediate-admission intersection and bridge result
- id: intermediate-admission
  resource: ../../../evidence/catalog.json#E-bb8bd404d1f4
  title: Fixed-capacity intermediate B4 comparison and validation
- id: admission-capture
  resource: ../../../evidence/catalog.json#E-d90ce37dc0dd
  title: Shadow admission and cache reconciliation decompilation
- id: cache-manager
  resource: ../../../evidence/catalog.json#E-bc0e0b354e98
  title: Global cache reconciliation and age/new-owner refresh selection
- id: cache-allocator
  resource: ../../../evidence/catalog.json#E-454dae1239f0
  title: Global cache-owner allocation, reuse and identity initialization
- id: cache-texture
  resource: ../../../evidence/catalog.json#E-aa165849571a
  title: Global StaticShadowMap constructor and dimension fields
- id: cache-profile
  resource: ../../../evidence/catalog.json#E-eb759699435d
  title: Global cache configuration callback and count/size rebuild boundary
- id: cache-builder
  resource: ../../../evidence/catalog.json#E-1001d162f65a
  title: Global cached-backing attachment and selected-update queue construction
- id: b4-scheduler
  resource: ../../../evidence/catalog.json#E-97835655b2f3
  title: Native B4 scheduler decompilation and patch-site map
- id: matrix-evidence
  resource: ../../../evidence/catalog.json#E-9c66531d0987
  title: Five-profile runtime evidence
- id: calibration-evidence
  resource: ../../../evidence/catalog.json#E-0af74b2e7e72
  title: v1.2.3 five-profile calibration and Complete Edition pressure capture
- id: archived-capability
  resource: ../../../evidence/catalog.json#E-6de2a2c4f130
  title: Archived proven-capabilities report
- id: archived-b4-results
  resource: ../../../evidence/catalog.json#E-0042fc735065
  title: Archived B4 experiment findings and evidence
- id: v078-runtime
  resource: ../../../evidence/catalog.json#E-06dbc9170dfd
  title: Preserved v0.7.8 runtime log
- id: v124-evidence
  resource: ../../../evidence/catalog.json#E-6ac2c20cc1ab
  title: Accepted v1.2.4 Global extreme-load evidence
- resource: ../../../evidence/catalog.json#E-77e04602a192
  title: Shadow manager and owner-profile module
- resource: ../../../evidence/catalog.json#E-8ba8bf022b48
  title: Renderer queue diagnostics module
- resource: ../../../evidence/catalog.json#E-f34fbdbbfd2a
  title: Proven Shadow Engine capabilities and historical pressure findings
- resource: ../../../evidence/catalog.json#E-c38ab69eeed1
  title: Preserved historical technical evidence
- resource: ../../../evidence/catalog.json#E-e6584912520b
  title: Preserved historical technical evidence
---

# Distinct pressure boundaries

Current fixed shadow policy retains 30 physical maps, 31 queue entries, B4=21,
A8=4 and a pre-reserved eight-owner vector. Selection, manager admission/cache
residency and cumulative renderer faces are different limits. More cars than
maps, a near-full queue, or fewer selected owners do not identify which boundary
caused a visible shadow to disappear.

The manager first selects a bounded priority set and associates overflowed
eligible records with cached owners. The renderer later consumes the resulting
queue and counts physical shadow-map faces. A light can therefore lose a
high-resolution dynamic position or its cached representation before the
renderer queue reaches 24 faces.[^admission-capture]

The v 1.2.3 release policy fixes `B4` at 21, yielding approximately 20 ordinary
dynamic positions when caching is enabled, and fixes `A8` at four cached
owners. Cached owners retain native textures while sharing limited update work;
they are not additional ordinary dynamic positions. The usual oldest-owner
refresh has a new-owner exception described below.[^manager-source][^cache-manager]


Historical cached-owner observations use 512×512. Native configuration determines
the cache texture size; 512 is not a universal constant. More A8 owners can extend
the refresh rotation without adding ordinary dynamic positions. Capture candidates,
admissions, dynamic/special records, cached bindings, update flags, live owners,
entries, faces and actual
clamp/drop counters around loss/recovery. Derived prefix-map ranges are CPU
observations, not GPU binding or receiver proof. Physical expansion beyond pass 30
requires a separate pass-registry redesign; guards cannot be removed by inference.

# More shadow-casting lights at lower frame cost

This is a feasibility assessment, combining published techniques with existing
WD1 mappings. It establishes no new GPU timing or safe capacity setting.

Increasing admission with unchanged work per light normally adds cost. The
engineering opportunity is to lower average per-light work enough to outweigh
the additional lights. Storage, refresh work and lighting evaluation must be
budgeted separately. For illustration, 50% more refreshed lights requires more
than a one-third reduction in average refresh cost to reduce that component's
total time; CPU and final shading costs still need accounting. A lower shadow
pass time does not guarantee higher game FPS if another stage limits the frame.

## What the retained capture actually permits us to say

Reanalysis with the existing strict decoder of the Global .89 60-second capture yields:

- 87,160 ordinary-eligible sampled occurrences, of which 58,926 are unbound.
- Renderer admitted faces equal 26 in 1,111 of 1,200 samples, with a maximum 28
  and no sampled requested/admitted face clamp. This supports an earlier
  admission restriction in that run, not exhaustion of the configured 30 faces.
- Of 26,118 submitted single-face occurrences, 2,294 change from 4096 to 1024:
  8.78%. 21,480 remain 4096; 2,344 remain 512.
- Summing width times height over those same single-face samples gives 9.03%
  less nominal area than their native requests. Multi-face records are excluded
  because their resource packing is not inferred. This is arithmetic on one
  sampled run, not an Off-versus-On benchmark, memory occupancy or GPU speedup.

The reproducible script, input and decoder hashes, dimension groups and complete
face histogram are registered as
[E-shadow-budget-20261004](../../../evidence/catalog.json#E-shadow-budget-20261004).
Streams are not causally paired by bucket; totals are occurrences, not unique
lights. Unused sampled faces do not establish safe admission headroom in other
scenes. The historical B4=25 control requested 33 faces and clamped work.

## Transferable approaches

| Approach | Published mechanism | WD1 applicability and missing contract |
| --- | --- | --- |
| Adaptive resolution | Unity HDRP rescales dynamic maps by projected light coverage and packs multiple resolutions into atlases. | The existing request-size hook is a usable starting point; verified screen impact, near-field protection and stable transitions remain needed. Light-center distance alone does not measure the importance of nearby shadow receivers. |
| Separate residency and refresh | Unity retains cached maps between explicit updates, with movement-triggered refresh options. | WD1 cached bindings can already skip queue creation. More residency needs stable identity/storage, valid retained texture contents and an update policy that handles movement and new arrivals. Merely skipping a dynamic queue entry does not establish persistent contents. |
| Cache static geometry separately | Epic documents avoiding repeated static-caster rendering under unchanged lights. | Most useful for stationary world lights. WD1's named StaticShadowMap is not proof of a static/dynamic caster split. Caster lists, invalidation and composition would need mapping. Moving headlights cannot safely reuse an unchanged projection just because buildings are static. |
| Stochastic many-light rendering | Epic MegaLights uses a fixed per-pixel sampling budget and denoising; increasing overlapping light complexity can reduce quality. | A major lighting-path replacement requiring a scene representation, visibility queries, material integration and temporal reconstruction. Its shadow-map option still pays per-light map preparation. It is not a DLL or setting that removes WD1's admission limit. |

Sources: [HDRP resolution/atlases](https://docs.unity3d.com/Packages/com.unity.render-pipelines.high-definition@17.0/manual/Shadows-in-HDRP.html),
[HDRP update modes](https://docs.unity3d.com/Packages/com.unity.render-pipelines.high-definition@17.0/manual/shadow-update-mode.html),
[Epic caching](https://dev.epicgames.com/documentation/en-us/unreal-engine/movable-light-mobility-in-unreal-engine),
[MegaLights](https://dev.epicgames.com/documentation/en-us/unreal-engine/megalights-in-unreal-engine).

Resolution arithmetic explains the opportunity without predicting performance:
one 4096-square face has the same nominal area as sixteen 1024-square faces.
Twenty 4096 faces total 335,544,320 texels; ten 4096 plus thirty 1024 faces total
199,229,440, or 40.625% less. This hypothetical 40-face arrangement exceeds current
validated capacity and is not a configuration recommendation. Every added light
still has geometry, submission, filtering and lighting-evaluation costs; alpha
tested casters and overdraw can dominate independently of nominal dimensions.

## Feasibility order and acceptance evidence

The existing resolution hook is a narrow implementation route, but savings
depend on which currently rendered work may be reduced. If the full original
nearby range must retain its resolution and low resolution applies only to a
new outer band, that band adds cheaper work; it does not reduce existing work.
Under that constraint, reducing redundant redraws or caster/submission cost is
necessary to fund more lights with lower total cost. Establish actual savings
before spending part on additional admissions. The existing pass registry and face
guards remain binding even if rendering becomes cheaper. Significant expansion
beyond the current envelope requires allocator, pass lookup, result lifetime and
all consumers to be redesigned and independently validated; an atlas changes
sampling and ownership as well as storage.

Selective retained-map updates are a second route with potentially larger
savings for stationary lights, but lower immediate feasibility. Native age/new
owner scheduling below already has burst and starvation possibilities. Neither
a larger A8 nor a blind every-N-frames policy proves validity or smoothness.
Fast-changing headlights and nearby dynamic casters need timely refreshes.

Success requires more simultaneously usable shadowed lights plus lower total
CPU/GPU frame cost on comparable dense scenes, preserving nearby quality and
avoiding stale shadows, black-world regressions and worse frame-time spikes.
Admission/face/resource counts establish functional changes; they cannot replace
shadow-pass and overall frame-time measurements. CPU callback timings are not
GPU timings. This assessment does not select a new B4/A8 value or promise FPS.

# Cache allocation, replacement and update selection

These are static roles from the preserved Global image. Offsets below are
hexadecimal; RVAs are not portable hook identities. The source bodies establish
native CPU decisions, not their live frequency, GPU readiness or a safe mutation
API. The manager owns the 0x700-byte owner records and their textures; the patch's
eight-record reserve prevents vector movement after borrowed owner pointers are
published, while A8 retains its separate logical limit.

| Function | Ownership, inputs, outputs and consumer boundary |
| --- | --- |
| Manager 0x002E9B60 | Reconciles owner+78 identity against the admitted candidate set. Unmatched owners become unused with identity -1. Promotion into the ordinary dynamic allowance also clears the old cached association. Retention therefore depends on native admission and lane, not just continued candidate existence. |
| Cache allocator/rebinder 0x002E2470 | Reuses an owner whose +78 is -1; otherwise appends only below A8 and constructs the new owner and its native texture. Assignment copies native spatial identity, initializes age+7C=10000, clears +80 and resets matrices in backing+90. Reuse skips fresh texture construction; the same slot can represent a different light. |
| Cache texture constructor 0x002C0500 | Creates a native StaticShadowMap texture using manager+AC for both dimensions and initializes the owner's wrapper, dimensions and inverse dimensions. These retained textures are separate from the expanded dynamic map/pass registry. |
| Queue builder 0x0030A570 | Attaches owner+90 at candidate+58 when owner+80 is set. Cached bindings with update byte+10=0 then skip queue construction. The ordinary cache-bound size path reads the existing owner's texture through 0x0025DBF0. |
| Profile callback 0x00308A90 | Copies configuration+A58 into manager+B0. Clamps configuration+A50 to0..8 (reduced mode0) for A8 and +A54 to32..4096 for AC. A count or size change calls owner-range cleanup 0x0031DC00, resets size+A0 and reserves storage. This rebuild boundary is not a per-call resize API; subordinate texture-release semantics remain incompletely mapped. |

Sources: the manager, allocator, texture constructor, queue builder and profile
callback exports respectively.[^cache-manager][^cache-allocator][^cache-texture][^cache-builder][^cache-profile]

For existing cached owners, the manager increments age+7C up to INT_MAX and
ordinarily selects the greatest age for refresh, sets binding+10=1, resets age
to0 and sets owner+80=1. With manager+B0 enabled, however, each newly assigned
owner can receive immediate update selection. Any such new update suppresses
the usual oldest-existing-owner refresh for that call. Thus a guaranteed single
refresh per frame is not the native contract: ages advance per manager call,
new-owner updates can form a burst, and continuing reassignment can defer
existing-owner refresh. This is a static scheduling possibility, not a confirmed
cause of the remaining driving pop-in.[^cache-manager]

Owner+80 is set before queue construction. Neither it, the update byte nor an
attached backing proves completion or incoming shadow visibility. Increasing A8
can preserve more identities while adding texture storage and lengthening update
intervals; changing B0 trades newcomer delay against bursts and older refreshes.
Neither change follows safely from low face occupancy alone. A quality cap of4096
also preserves a native512 request rather than promoting it to4096; see the
[quality contract](vehicle-shadow-quality.md). Resource wrappers and returned
dimension metadata have separate [ownership limits](headlight-resource-diagnostics.md).

[^cache-manager]: Global manager 0x002E9B60, reconciliation and refresh-selection body.
[^cache-allocator]: Global 0x002E2470, unused-slot search and assignment/append paths.
[^cache-texture]: Global 0x002C0500, StaticShadowMap construction and dimensions.
[^cache-builder]: Global 0x0030A570, cached backing, update byte and dimension consumers.
[^cache-profile]: Global 0x00308A90, configuration and owner-range rebuild boundary.

# Native B4 scheduler semantics and safety limit

The Global manager initializes `B4` to four and can change it by one on each
manager call. Native normal-mode bounds are four through eight; reduced-mode
bounds are one through two. The deciding branch is derived from current
candidate/descriptor fields. It does not consume measured frame time, GPU
time, requested faces, outstanding slice work, stale-result counts, or worker
backlog. Native `B4` is therefore scene-adaptive admission state, not a proven
load or backpressure controller.[^b4-scheduler]

Archived v 0.7.8 evidence exposed the consequence of incoherent patching: an
initial/lower value of 17 paired with an unchanged upper bound of eight drove
runtime `B4` back to eight. Later expanded-residency experiments deliberately
patched constructor, normal lower bound, and normal upper bound to the same
value so admission remained deterministic while the reduced-mode branch stayed
native. The preserved run explicitly records `B4=17, A8=8` after the first
manager call, followed by `B4=8, A8=8`; it was not an A8-only test.
[^v078-runtime][^archived-b4-results]

An expanded native range such as 16 through 25 is not a proven stability
mechanism. Because the manager runs repeatedly and changes `B4` per call with
no pressure signal, hysteresis, or rate limit, that policy could rapidly alter
residency according to candidate ordering and cause the same eviction and
reacquisition churn visible as shadow flicker. A bounded load experiment must
either use one coherent fixed value across constructor/lower/upper sites, or
introduce a separately owned controller with measured inputs, hysteresis, and
an explicit update cadence. The latter is new engine policy and requires its
own mapping and validation before mutation.[^b4-scheduler][^archived-b4-results]


# Global .85 retained cache/update evidence

In256 complete unmarked manager observations,26 bindings consistently split into
2 special,20 ordinary dynamic and4 cached. There are1024 cached-binding
observations:258 update requests and766 normal no-update bindings. One cached
update is selected in254 calls and two in2 calls, matching renderer totals of
23/24 entries and26/27 faces. No face truncation occurs in this retained tail.

Twenty-nine native slot-key changes across27 calls all receive immediate update
with post-call age0, consistent with B0=1. Within continuously matched
slot/key/full-handle segments, completed update intervals usually span4 manager
calls and reach a maximum of6 calls/58.1834ms. This does not demonstrate prolonged
refresh starvation. The four initialized slots remain within physical reserve8;
the owner vector does not move. Native32-bit slot keys remain distinct from
full-generation vehicle identity and GPU allocation generations.

The tail lasts approximately2.073 seconds and has no visual event mark. Its
working refresh selection does not exclude an earlier stall or prove GPU
completion. The [eligibility concept](wd1-shadow-eligibility.md) owns the
simultaneous ordinary-admission saturation result.

# Global .87 sampled cache consistency

Across1200 sampled manager calls, all2400 before/after cache headers retain
count4, capacity8, A8=4, B4=21, dimension512, B0=1 and a stable owner-vector base.
There are4461 cached-binding observations:1161 selected for update and3300
legitimately skipped. All4278 retained-key before/after age transitions match
reset-on-update or increment-by-one. All183 observed newly assigned bound keys
receive immediate update, post-call age0 and initialized1.

In149 calls with new-owner updates, retained-owner refresh is suppressed as
mapped. In978 calls without new assignments but with cached bindings, exactly
one greatest-age surviving owner refreshes. No checked scheduling-rule violation
appears. Copied ages range0..7 before and0..8 after; they count manager calls,
not elapsed milliseconds or GPU completion.

The50ms sampling omits intervening calls. Same-slot/key/full-handle endpoints
cannot establish continuous residency or a true refresh interval: assignments
can change and return between observations. Native32-bit keys are also not full
handle identity; one sampled slot/key associates with two different full handles
at different times. New assignment and ordinary refresh obey the mapped policy
within selected calls, but these observations do not exclude all between-sample
churn or prove visible readiness. They do not justify an age/refresh rewrite.

# Experiments and observed limits

| Experiment | Evidence and conclusion |
| --- | --- |
| Original 24-face regional pressure |VMPless23/24 and Complete Edition 21/24 with visible world loss, no clamp. Paired loss/recovery: 147/71 candidates, 17/17 dynamic-or-special, 4/0 cached, 21/20 faces. No queue corruption, owner movement or lifecycle failure. Upstream admission/cache competition relieved before physical truncation. |
| v 1.2.2 layout rejection |30 maps, 31 entries, 14 extra handles, 28 extra pass slots, 13 external results; A8 stays 4. Uniform0x24C8 across 46 relocations shifted mapping arrays by 48/24 bytes: queue populated, zero SliceExecute stores, all shadows missing. |
| v 1.2.3 correction |Regions independently grow0x24C0/0x24C4/0x24C8 per map. Passes 17–30 use slots 34–61, max key0x3D0C within 64 slots/stored0x3F00. Complete Edition 26 admissions/26 of 30 faces still evicted/reacquired spotlight/moon shadows, proving residency pressure can precede a full map budget. |
| v 1.2.4 / v 2.0.0 B4=25 |Only coherent normal B4 changes 21→25; reduced mode, A8, vector reserve, layouts/lifetime retained. Global 154 candidates, 30 admissions, four cached, 30/30 faces; 402 above-budget requests up to 33,≤3 trailing entries omitted. No overflow/tail corruption/owner movement/late/duplicate/release failure or reported visual regression. Accepted tested hypothesis, not universal capacity safety. |
| v 2.0.3 dense bridge |220 candidates, 30 faces; 907 synchronous clamp messages: 775 requests 31 faces, 81 at 32, 51 at 33. Physical pressure confirmed, separate from rejected lifecycle. .4 removed per-clamp file writes but retained aggregate clamp/drop/peak counters. |
| .14/.15 fixed-admission comparison |.14 B4=16 reported no flicker/slightly more pop-in. .15 B4=21 retained 30/A8=4 and all mechanisms; constructor/both normal bounds stay coherent.44 Python/native/corpus/repro gates passed; A4EE and broad tests separate. |
| .15 accepted Global control |Very stable reported intersection/bridge; 67,138 then 120,106 exact current-generation results, balanced resources, zero rejection/stale/late/release/clamp/drop.26/30 sampled, peak 29, 216 peak candidates. Intersection 432 submissions≤27 faces, 1,299 nonnull lookups/5,196 independent comparisons withzero differences. Supports clean CPU use beyond 24, not full 30/overflow/GPU proof. B4=23 proposal was deferred; B4=21 became scoped leak-hotfix release. |

The lower B4 control and higher historical pressure runs are different scenes
and lifecycle revisions. They do not establish one universal flicker threshold.
B4 is candidate-driven scene-adaptive state natively, not measured load control;
wide unowned ranges could change every manager call without hysteresis or rate
limit. Preserve coherent fixed bounds for an isolated experiment; a real pressure
controller requires measured inputs, owned cadence and independently validated
stability rules.

# Historical quality loss below physical face capacity

In the historical v1.2.8 control, native A8=8 and full candidate passthrough produced only 9 of 24 physical faces while three ordinary dynamic lights rendered at 4096x4096 and cached owners rotated through one 512x512 refresh slot. Increasing physical map storage alone would not explain that observed coarse-shadow transition.

The later v1.2.16 tree trace recorded seven vehicle headlights in the fully dynamic lane while world spotlight handles `0x1D25` and `0x1D1B` entered the sole active 512 refresh slot and were displaced there by vehicle lights. Eight cached owners shared that refresh position over time. This capture supports one residency transition causing both reduced resolution and lower apparent shadow-update cadence; it does not establish a drop in game FPS or identify those historical handles in later sessions.

# Historical coherent B4=12 control

The v0.8.0 control set constructor, normal adaptive lower bound and normal adaptive upper bound coherently to B4=12, with logical A8=4 and physical owner reserve eight. The reported session observed 12/4 after profile initialization rather than the earlier 17/8 oscillation. With caching enabled this represented approximately eleven ordinary dynamic positions plus the cached-owner lane, not twelve ordinary lights guaranteed separate high-resolution maps.

The recorded run lasted 258.495 seconds and ended at renderer call 41,901. Of 224 residency samples, 148 held 14 entries / 17 faces. The report observed no physical overflow or clamp, invalid pre/post-render queue tail, owner reserve/vector failure or null-resource guard event, and found no matching crash dump or Windows Application Error event. The tester reported no black-world state or crash in that one session. This absence of observed failures did not establish endurance or identify the older tail overwriter.

A two-car tree test still showed coarse shadow demotion and a brief disappearance at no more than 18 of 24 faces. It therefore supplied another example of visual loss below physical face capacity. The report proposed a coherent B4=17 control while retaining A8=4 and reserve eight; that paragraph was a hypothesis, not a result. No controlled FPS or frame-time comparison accompanied the v0.8.0 evidence. Its historical full-chain passthrough and absent vehicle-owner classifier are not current policy.

# Historical emergency-light pressure observation

A 2026-08-23 report using Addons v1.0.13 described reduced quality of unrelated world shadows after additional police-siren shadows became active, with faster recovery when the engine patch was enabled. This was a comparative visual report without synchronized admission, residency, update or allocation measurements. It motivates separating those boundaries during diagnosis; it identifies neither a saturated capacity nor a safe capacity increase. The report is historical and does not supersede the later measured residency/capacity results above.
