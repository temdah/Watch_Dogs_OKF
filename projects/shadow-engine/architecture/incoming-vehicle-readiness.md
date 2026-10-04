---
type: Runtime Policy Contract
title: Incoming Vehicle Shadow Readiness
description: Incoming selection policy and synchronous preparation-cost reductions.
tags:
- shadow-engine
- vehicles
- performance
- admission
status: draft
sources:
- id: retired-policy-migration
  resource: ../../../evidence/catalog.json#E-shadow-baseline-20261004
  title: Retired experiment removal and settings migration fixtures
- resource: https://www.adriancourreges.com/blog/2015/11/02/gta-v-graphics-study/
  title: Firsthand GTA V DX11 frame analysis, 2015
- resource: https://www.nvidia.com/en-us/geforce/news/grand-theft-auto-v-pc-graphics-and-performance-guide/
  title: NVIDIA GTA V PC graphics guide, 2015
- resource: https://www.adriancourreges.com/blog/2016/09/09/doom-2016-graphics-study/
  title: Firsthand DOOM Vulkan frame analysis, 2016
- resource: https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine
  title: Epic Virtual Shadow Maps documentation, consulted 2026-10-04
- resource: https://www.unrealengine.com/tech-blog/virtual-shadow-maps-in-fortnite-battle-royale-chapter-4
  title: Epic Fortnite Chapter 4 shadow production tradeoffs
- id: onset-experiment
  resource: ../../../evidence/catalog.json#E-shadow90-onset-20261004
  title: Global lighting-side onset experiment, native proof and actual-source fixtures
- resource: ../../../evidence/catalog.json#E-ad4735a0faf6
  title: Current69 position-only player anchor and uniform owner selection/quality
- resource: mod-performance-audit.md
  title: Measuring native patch overhead without confusing it with frame cost
- resource: ../../../evidence/catalog.json#E-e19e149211e9
  title: Stationary owner loses policy eligibility as traffic passes in67
- resource: ../../../evidence/catalog.json#E-8829e8a21f3f
  title: Actual-near extra protection and preparation optimisation preflight
- resource: ../../../evidence/catalog.json#E-d6e4c3cebc48
  title: Scoped region validation and adjacent preparation audit
- resource: ../../../evidence/catalog.json#E-e7f9af05aec8
  title: Saved Global disassembly and named binding provenance
- resource: ../../../evidence/catalog.json#E-e8a5bb74e5fe
  title: Knowledge lookup and constraints
- resource: ../../../evidence/catalog.json#E-e995befb5a2c
  title: Sanitized implementation and safety contract
- resource: ../../../evidence/catalog.json#E-4d85852a0d8b
  title: Explicit optional player-position proof coverage
- resource: ../../../evidence/catalog.json#E-f4a82f305d4e
  title: Frozen62 equivalence and incoming policy fixtures
---

Experimental .80 adds the separate [exact driver identity contract](driver-vehicle-identity.md).
It supersedes the older driven-owner gap below only for the validated Global
path. Incoming extra-slot ordering remains; native population timing is a separate unresolved boundary.


# Candidate contract

The retained .66 policy changes extra-slot ordering: actual nearby candidates within eight
world units rank by current distance; outgoing retention fills next; forecast
arrivals only use remaining space. Main N and its incumbent margin, immediate
actual-near admission and totalN+2 are unchanged. Prediction cannot displace a
closer near-field extra or consume a slot needed for retained departures.
This does not protect every visible receiver or guarantee native admission.

Preparation now uses 128 sorted, binary-searched protection regions per synchronous
copy pass, with direct-query fallback when full, rather than 32 linearly searched
replacement entries. This is a metadata cache, not cached shadow rendering.
Owner grouping uses bounded full-owner hash indexes in classification/selection;
all registry epochs/conflict evidence remain. No update cadence/lifetime change.
Existing workload timing separates performance effects from selection changes.
The historical below-50 us target was not a measured .66 result.

Detailed vehicle samples include policyRole:0 unselected,1 main,2 nearby,
3 outgoing,4 forecast, alongside policyProtected and native admitted state.
The .66 tools changed only the extra-slot explanation. Tests
cover 64 shuffled fragmented regions, full-field classification equivalence,
the historical finite 1..10 budgets, nearby/outgoing over speculation and spare-slot forecasts.
Native renderer optimisation and temporal fading remain separate investigations.

Historical 64/63 implementation follows; ordering/cache sizes below describe
those builds, not 66.

v2.0.64 retains 63 selection and reduces copying/transaction overhead. A bounded
32-region stack cache reuses successful committed/protection/range checks only
inside one synchronous candidate-copy pass. It is discarded before native
execution, not carried to another call or used as identity/lifetime evidence.
Failed, guard, noaccess, overflow and crossing-region reads remain rejected.
Neither this nor the former per-pointer query pins memory against concurrent
unmapping; the existing synchronous native borrowing contract remains required.
No process-wide readability helper or lifetime policy changes.

Policy copying skips spatial-handle reads for non-Spotlight3 types, which cannot
be suppressed. Requested diagnostics still retain those identities. Native next
links are read after validation, and unchanged links are no longer rewritten in
filtering/restoration. Complete full-handle owner selection and cadence remain.
The existing workload action adds sampled snapshot/copy/classification/selection
times, copy query/hit counts and changed-link counts; ordinary calls do not add
QPC timings. The .64 change retained .63 tools compatibility.

Synthetic shared-region 137-candidate copying reduces 411 queries to 1 and measured
about 118 us versus1.7 us. This is an idealized layout, not game preparation or FPS.
The .63 report accepted incoming responsiveness/4-slot visuals but rejected its performance. Later .64 measurements were 73..92 us mean positive-limit preparation; limit 4 was reported faster while 10 remained slower than 0.

Earlier 63 implementation details follow.

v2.0.63 changes preparation for every positive limit, not only 10. Full-handle
candidate duplicates use a bounded hash index instead of repeated full scans.
Detailed registry statistics and type 1 diagnostic classification are excluded
from ordinary preparation, but retained in requested reports. Scratch headers
and used records are cleared; unused maximum-capacity arrays are not cleared.
The frozen 62 classifier remains test-only. Synthetic classification timing is
not total preparation time, frame time or GPU performance.

The Global optional proof now follows the local-player entity reference and
copies its XYZ once per classification. Vehicle XYZ is copied during its native
batch and published with the existing full-handle/renderer-epoch record. Native
batch arguments, cadence and rendering resources are unchanged. Other profiles
retain the native reference until independently mapped. Missing live positions
on the verified path cannot authorize suppression. Readability and repeated
identity checks reject invalid copies; they do not constitute a native lifetime
pin. Save loading/reloading and player movement therefore remain runtime gates.

# Incoming slots

The N primary slots retain the small incumbent distance margin. With a valid
player anchor, the extra two slots prefer candidates within eight world units
or approaching across the primary frontier within a 200 ms prediction. Prediction
is capped at eight units, uses 32..250 ms observations and full owner/handle
identity. A 256-entry direct-mapped scalar table belongs to the residency lock;
collisions or long gaps reset prediction. No native pointer is retained there.
Remaining extra slots retain outgoing owners for at most one second.

Total selected owners never exceeds N+2. Uncertain world/vehicle classification
remains passthrough; degraded evidence still freezes resident identities.
The policy cannot create candidates the engine has not supplied, guarantee
immediate rendering after admission, or override native shadow resource pressure.
0 remains unlimited. Quality controls, world-light admission, lifecycle and all
internal actions remain. No distance-quality feature or temporal fade is added.

# Fade boundary and validation

The [WD1 eligibility and lighting mapping](wd1-shadow-eligibility.md#lighting-consumption-of-the-distance-factor)
now follows the native distance factor into `LightShadowFactor`: the CPU block
receives `C+68` and its complement. This supersedes the metadata-only consumer
gap. The bounded experiment below intercepts population before the caller
publishes the completed block, without revisiting cached blocks asynchronously.
It does not prove dithering. Do not alternate admission, write an unowned
property, or delay arrivals to simulate a fade.

Tests cover the historical finite 1..10 budgets, nearby-before-outgoing, player-relative distance,
missing position group exclusion, proof corruption, generation/gap reset and
100 dense classifier equivalence cases. Global byte proof is not live visual
acceptance. Capture logs expose playerAnchor and selectionDistance; native
type 1 diagnostic distance remains separate from headlight admission.

# Lighting-side onset experiment

This is preserved experiment documentation. The .91 cleanup removes the hook,
profile data and onset-history owner from the active unity build. The experiment
has no reported visual acceptance; CPU observation gaps remain distinct from a
verified new shadow-admission generation. The native mapping and negative limits
below remain research evidence.[^retired-policy-migration]

The .90 experiment detours Global `0031A8C0` with the native six-pointer x64
call contract and invokes the original exactly once before postprocessing.
Ten sparse, independent instruction/data spans and the 15-byte relocatable
stack-store prefix gate activation. Other profiles have no mapping for this
feature. Installation uses the existing deferred transaction; behavior activates
only after commit, and an unsupported proof preserves existing rendering.
[^onset-experiment]

The owning onset subsystem borrows the original call's candidate, spatial,
descriptor and LightData block only during that call. It requires enabled
type3, matching passed candidate pointers, non-null native backing and texture,
and the expected finite factor/complement pair. Exact recent vehicle ownership
and full entity generation come from the existing nonwaiting registry copy,
including its freshness, publication-gap and ambiguity guards. Type1, world,
unknown and unsupported cases retain native strength. The driven car remains
eligible for this shadow-only ramp; no player lookup or brightness write is added.
[^onset-experiment]

A separate nonwaiting token owns 256 scalar history slots with at most eight
probes. Each full light-handle/owner/entity identity ramps from zero to native
strength over 180 ms using `t*t*(3-2*t)`. More than 250 ms without an eligible
observation starts another ramp; slots expire after 1,000 ms. Same-tick or
out-of-order concurrent observations cannot reverse progress. Unsigned tick
differences handle wrap, and completed clocks saturate. Collision/full-table,
identity or lock failure preserves native output. No borrowed pointer is kept
for later dereference, and no token spans native execution.
[^onset-experiment]

Only LightData `+160 = native_factor * ramp` and `+164 = 1 - result` change;
the original already marks that field dirty. Candidate `+68`, admission,
resolution, light color/brightness, distance and resource ownership are untouched.
Cached uses of that populated block consume the stored pair; this experiment
does not force native refreshes or asynchronously animate a cached block.
Its clock starts on observed native-backed lighting population, **not a GPU
completion event**. It cannot guarantee fading of new casters appearing inside
an already-active shadow map, very brief absences, or a block that the engine
does not repopulate. Faster preparation and extended range remain separate.
[^onset-experiment]

Offline fixtures cover exact factor-only writes, identity/publisher failures,
clock/gap/collision behavior, every proof-byte rejection, other-profile fallback,
a six-argument executable trampoline over synthetic code and allocation/write
rollback. Internal/Release builds are reproducible. These results establish the
bounded CPU contract, not visible fade quality, regression acceptance or FPS.
The existing recording worker logs cumulative inspected/modified/skipped counts;
render callbacks do not perform file I/O.[^onset-experiment]

[^onset-experiment]: Actual-source fixtures, Global image hash/signature verification and build/package records; first in-game visual validation remains outstanding.

# External renderer comparisons and transfer limits

These are published reference techniques and WD1 design hypotheses, not new
WD1 binary findings or a controlled comparison of visual quality. GTA observations
below concern the 2015 PC DX11 renderer, not GTA V Enhanced or ray-traced shadows.

- [GTA V frame analysis](https://www.adriancourreges.com/blog/2015/11/02/gta-v-graphics-study/)
  observes four sun-shadow cascades allocating more detail near the camera, and
  mesh LOD transitions using stippling. Neither observation establishes temporal
  headlight-shadow admission blending. [NVIDIA's guide](https://www.nvidia.com/en-us/geforce/news/grand-theft-auto-v-pc-graphics-and-performance-guide/)
  documents extended shadow distance and PCSS contact softening; softening an edge
  is different from hiding the first appearance of a shadow. GTA is a useful
  visual comparison, but these sources do not establish that its local-light
  scheduler solves WD1's dense-traffic case.
- [DOOM's Vulkan frame analysis](https://www.adriancourreges.com/blog/2016/09/09/doom-2016-graphics-study/)
  describes atlas reuse, distance-dependent map size, and separating cached static
  shadow content from dynamic casters. The transferable question is which work
  remains valid and can be reused. Stationary scenery does not by itself make a
  cached projection valid when a vehicle's headlight moves. No DOOM atlas layout,
  size or performance result is a WD1 capacity recommendation.
- [Epic's Virtual Shadow Maps documentation](https://dev.epicgames.com/documentation/en-us/unreal-engine/virtual-shadow-maps-in-unreal-engine)
  describes distinct resolution biases for moving lights and a gradual return
  when motion stops. It also states that light movement invalidates that light's
  cached pages. This motivates motion-aware quality and transition research,
  without proving that WD1 can animate resolution or preserve map history.
- [Epic's Fortnite Chapter 4 account](https://www.unrealengine.com/tech-blog/virtual-shadow-maps-in-fortnite-battle-royale-chapter-4)
  reports abandoning directional shadow caching for its moving-sun workload and
  reducing effective resolution to meet its performance target. More caching is
  therefore not universally cheaper. This is a directional-light production
  example, not a measured vehicle-headlight solution.

## Distinguish the visible failure before choosing a technique

Human observation, reported directly on 2026-10-04: the visible pop-in is an
entire light's shadow becoming active. The observer explicitly selected this
case over an individual caster appearing inside an already-active shadow.
No new build identity or synchronized capture accompanied this clarification;
it is symptom classification, not onset-experiment acceptance or proof that
distance, admission pressure or resource readiness is the responsible gate.
It focuses the investigation on the per-light onset path. The other failure
classes below remain a general diagnostic reference.

The observer further attributes the delayed onset to shadow-slot competition
in dense scenes: the whole shadow appears when space becomes available as the
view approaches. This is consistent with the recorded
[Global .87 admission transitions](wd1-shadow-eligibility.md#global-87-whole-pass-admission),
including an eligible light moving from ordinary rank26 to24 and acquiring a
binding. Those captures establish admission pressure, not a synchronized match
to the reported visual event or physical texture-pool exhaustion. Ordinary
admission count and the configured resource capacity are distinct quantities.

For this failure mode, a candidate design should tie onset state to a verified
unbound-to-bound transition for the full light identity. The existing experiment
instead infers onset from eligible lighting-population observations and gaps;
it does not explicitly track admission loss/reacquisition. Such a transition is
still not itself proof of GPU completion. Reducing requested resolution does not
increase the native count allowance, and extending range can add competing
candidates. Earlier admission within a fixed budget reallocates opportunity
from other lights; it is not free preparation capacity.

| Visible event | Relevant mechanism | WD1 evidence boundary |
| --- | --- | --- |
| Entire local-light shadow appears | Admission, backing availability, shadow-strength transition | The onset experiment observes CPU population; it does not prove visible readiness. |
| A building or vehicle suddenly gains a shadow inside an active light | Caster streaming, caster culling/LOD, map refresh | A per-light clock can already be complete; caster identity and submission need mapping. |
| Shadow detail changes abruptly | Resolution or representation transition | Changing a texture request does not prove a blended transition. |
| Shadow arrives late during fast travel | Candidate production, visibility feedback, admission pressure, update scheduling | Existing eligible/unbound samples do not identify the visible event's cause. |

The strongest portable design hypothesis is to prepare eligible lower-resolution
work before it becomes conspicuous, preserve near-field priority, and introduce
valid results gradually. This is not evidence that any cited game implements that
exact combination. WD1 already has bounded forecast selection; selecting a future
owner does not force earlier native candidate creation or rendering. Earlier work
also consumes the same finite budget and may displace useful work.

A genuine low-to-high map crossfade requires simultaneous valid representations,
their lifetimes and a shading consumer; it cannot be assumed possible within the
existing map budget. A shadow-strength ramp needs less state but may visibly
lighten the scene and cannot blend individual new casters. Extending distance must
still preserve the independent category/coverage gates documented in
[WD1 eligibility](wd1-shadow-eligibility.md). Lower resolution reduces texel work,
but does not automatically remove geometry submission or admission costs.

Cross-engine image compositing is not a shadow-renderer interface. A renderer
transplant would need the host's light transforms, caster geometry and animation,
material cutouts, resource lifetimes and lighting integration. Reimplementing a
specific technique against verified WD1 boundaries is a separate, narrower route.
The existing [WD2 comparison](wd2-shadow-reference.md) remains the closest mapped
engine reference, with its own static-evidence and portability limits.

# Native Global identity and camera mapping

The old native batch float is camera-derived, not demonstrated player distance.
Parent0099E5D0 reads vehicle+10 reference, reference+8 entity and 0082E610 XYZ.
It calls006A5480 on the first controller at global 03B78508 and subtracts the
returned transform translation.006A5480 resolves a component through 0069C950;
006EC660 names its class CCameraComponent. It calls0078A7C0 and 003F8400 to refresh
the cache at controller-data+20. This is NOT a safe read-only getter to invoke.

GetLocalPlayerEntityId registration at 02EF3620 pairs named string02EF3370 with
006F1D80. Its006F1D95 instruction reads global 03B78508: root->array->first
controller, controller+8->data, data+10->entity reference, reference+0->fullID.
GetEntityPosition registration at 03002CD0 pairs02FFDA18 with01422D60. The wrapper
targets011EB1B0, which resolves a reference, reads reference+8 and calls0082E610.
The latter copies entity+50/+54/+58 to the output XYZ. Its caller increments a
reference counter; the patch does not reproduce that ownership protocol or call
these native functions. Static layout proof is not cross-thread lifetime proof.

63 byte-checks the Global binding instruction spans and position-reader prefix,
then stores only the immutable image-root address. Copies use readability,
finite-coordinate and repeated identity checks; vehicle coordinates are copied
inside the existing vehicle batch. No new hooks or native writes. Non-Global
profile fields are zero: no guessed translation. VMPless/Complete binding scan
hits alone do not authorize enabling their position path. These static checks alone do not establish live loading, reload, camera or movement correctness.

# Fade mapping limit

String032027F0 fCastShadowFadeDistance is registered at 0259A0D2 with offset 48
through 02594320. This is a metadata registration context, not an owned runtime
light/shader fade address. It proves neither temporal fading nor dithering.
No fade write is included in 63.


# Recorded limits

Version .67 detailed samples fully admitted protected headlights in all eight samples, yet a complete/recent stationary owner at about 18.45 world units was unprotected in three samples and primary again in the fourth. Five residents were present in seven of eight samples. Extras are conditional - near within eight units, outgoing under one second, then approaching forecast - not an unconditional nearest six. This supports policy eligibility loss, without timestamping the exact visible disappearance or expiry.

The .63 dense 100-round classifier comparison measured about 108..112 us for frozen .62 versus 23 us, excluding snapshot/preparation, native work and live player reads. Historical .62 positive-limit preparation was about 0.7 ms; 10 and 0 both averaged 26 faces. ETW access error 5 supplied no presentation/FPS result. Native cadence/resource admission can still delay first visibility.

The former driven-owner gap is addressed only by the experimental .80 Global proof. A CVehicle token alone or nearest distance never proves the driven car. Exact bypass preserves native requested quality, not forced 4096 or immediate resizing; shared maps, siren work and native admission remain limits. Current control semantics are finite 1..9, 0 off and 10 Unlimited; older finite-10 test references describe historical policy fixtures.

[^retired-policy-migration]: Preserved pre-cleanup source and actual-source baseline fixtures; both native builds reproduce offline, with no game acceptance inferred.
