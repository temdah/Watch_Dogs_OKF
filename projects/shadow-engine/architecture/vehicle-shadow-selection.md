---
type: Runtime Diagnostic Contract
title: Vehicle Shadow Selection Diagnostic
description: Generation-aware vehicle publication, coherent grouping, and hybrid vehicle-headlight
  admission boundary.
tags:
- shadow-engine
- vehicles
- headlights
- spotlight3
- selection
- diagnostics
status: draft
sources:
- resource: incoming-vehicle-readiness.md
  title: Incoming Vehicle Shadow Readiness
- id: implementation
  resource: ../../../evidence/catalog.json#E-ad4735a0faf6
  title: Vehicle selection diagnostic implementation
- id: tests
  resource: ../../../evidence/catalog.json#E-3260c48f5228
  title: Selection source-contract tests
- id: native-harness
  resource: ../../../evidence/catalog.json#E-f4a82f305d4e
  title: Actual-source synthetic selection harness
- resource: ../../../evidence/catalog.json#E-06078fbd86b8
  title: 69 three-window measurements, lifecycle and duplicate notification finding
- resource: ../../../evidence/catalog.json#E-ddb6d6bf0c6b
  title: 68 normal-cost measurements and downstream protected-admission losses
- resource: ../../../evidence/catalog.json#E-9a3c014e4dc8
  title: v2.0.68 maintained owner-index preparation preflight
- id: limiter-footprint
  resource: ../../../evidence/catalog.json#E-46ac97e89236
  title: v2.0.60 runtime evidence and limiter footprint audit
- id: coherent-batch
  resource: ../../../evidence/catalog.json#E-500352591906
  title: v2.0.59 evidence and coherent batch publication preflight
- id: nearest-transition
  resource: ../../../evidence/catalog.json#E-a57e00eecbdd
  title: Nearest-primary outgoing retention candidate and validation
- id: preflight
  resource: ../../../evidence/catalog.json#E-4c95d9762dff
  title: Knowledge and source preflight
- id: first-runtime
  resource: ../../../evidence/catalog.json#E-21831fa43ac6
  title: First Global nearest-selection runtime result
- id: corrected-runtime
  resource: ../../../evidence/catalog.json#E-81df7c009858
  title: Corrected manager-delta Global runtime result
- id: renderer-epoch-candidate
  resource: ../../../evidence/catalog.json#E-88f9b7340713
  title: Renderer-epoch selection diagnostic result
- id: renderer-epoch-runtime
  resource: ../../../evidence/catalog.json#E-7738200c6420
  title: Renderer-epoch Global runtime result
- id: limiter-preflight
  resource: ../../../evidence/catalog.json#E-5e461d8102ee
  title: Generation and active-limiter preflight
- id: limiter-global-runtime
  resource: ../../../evidence/catalog.json#E-3dce9733c398
  title: First active-limiter Global traffic-jam result
- id: epoch-scoped-candidate
  resource: ../../../evidence/catalog.json#E-c29884fe5376
  title: Epoch-scoped limiter and runtime-control candidate result
- id: epoch-scoped-runtime
  resource: ../../../evidence/catalog.json#E-9d72c337c598
  title: Epoch-scoped limiter Global runtime result
- id: admission-preflight
  resource: ../../../evidence/catalog.json#E-8c7e1151236e
  title: Protected admission and vehicle type-1 diagnostic preflight
- id: admission-runtime
  resource: ../../../evidence/catalog.json#E-115403120956
  title: Protected admission and rank-boundary Global runtime result
- id: residency-preflight
  resource: ../../../evidence/catalog.json#E-53fcbfed7fa7
  title: Owner residency and degraded-evidence preflight
- id: residency-candidate
  resource: ../../../evidence/catalog.json#E-ede26ed45366
  title: Owner-resident limiter candidate result
- id: residency-runtime
  resource: ../../../evidence/catalog.json#E-6d33cf4d9589
  title: Owner-resident limiter Global runtime result
- id: archived-atomic-boundary
  resource: ../../../evidence/catalog.json#E-6fae80de83a9
  title: Archived v0.8.5 TinyCC atomic return observation
- resource: ../../../evidence/catalog.json#E-7672703021a6
  title: Global82 driver quality separation and sampled limiter admission
---

# Selection bookkeeping experiment (.79)

The .79 experiment changed only module 18's
CPU bookkeeping. `classify_vehicle_selection_projected_fields` reuses its existing
full-owner hash and a call-local rank-by-group array after the unchanged sort.
Group creation, saturation, exact ties, complete/partial classification, full
sample fields and lock-miss keep decisions remain. No persistent state is added.

`prepare_vehicle_limiter_chain` owns header reset, original head/count, counters
and the disabled check. Only enabled calls enter
`prepare_enabled_vehicle_limiter_chain`, which owns the existing temporary
snapshot/projection/copy frame and unchanged validation/filter path. On the
TinyCC77 binary the old prologue probed 33 pages even at 0. The new small wrapper
avoids that work; emitted-code checks verify the large frame is behind the
branch. This is compiler/source evidence, not measured runtime speedup.

The quality publisher's per-record tag accesses now use the already-required
selection token, as documented by the [quality boundary](vehicle-shadow-quality.md).
All consumer code, ranking/residency, list order/restoration, capacity, profiles,
settings and UI remain. Frozen 77 comparisons and existing safety fixtures gate
the candidate. the tester's verified 79 Global run accepts A1-A3 with stable gameplay
and working limit 4. No causal FPS or pop-in improvement is established.

# .82 scoped runtime evidence

Finite1 with diagnostic extras0 means one ordinary traffic owner plus a proven
driven owner excluded before ranking. It does not mean only the driven car.
Unknown/ambiguous/type1/world passthrough boundaries still limit suppression scope.

Four Global captured calls at1/512/4096 confirm driver role5 and native4096 quality
preservation. The limiter suppresses24/26/30/30 known headlight candidates with no
whole-call fallback. The same rank1 traffic owner is protected but omitted by
native admission in the first three samples; a different rank1 owner is protected
and admitted in the fourth. No complete known headlight marked for suppression is
admitted in those samples. Thus both selection replacement and downstream omission
are observed; a selected car is not guaranteed native admission.

The visual report describes rapid other-car flicker while driving. Four samples
at500ms spacing cannot identify each visible transition or establish its cause.
Two fixed-policy workload windows have100 sampled managers with zero whole-call
fallback or degradation; this does not exclude unsampled per-light uncertainty,
cached-shadow behavior or selected-owner changes. Driver correctness in these
samples does not close the separate limiter continuity issue. No quota, resource
capacity, ranking or safety change follows from this review alone.

# Player-position dependency

The [incoming-readiness contract](incoming-vehicle-readiness.md) supersedes
earlier unresolved-anchor and outgoing-only descriptions below. Global now has
an explicit local-player position proof; other profiles retain the native
reference. Its originating candidate status is historical; .79 is accepted in the reported
Global scope.

# Address-ordered candidate copying (.69)

Module 18 copies the validated native list in original order, then validates
and copies descriptors and type 3 full handles in ascending address order.
Records, node order, checks and classification inputs remain unchanged for
coherent input. The bounded 256-entry sort array and region facts live only for
this synchronous preparation call. No AllocationBase protection assumption,
retained native pointers, allocation, extra lock or new runtime write is added.
The shared node/descriptor/handle readers also serve the original detailed path.

Synthetic descending-page input produces identical records with 16 versus 2
validation queries; guard/noaccess/missing fields and full selection/restoration
fixtures pass. This is not live performance evidence.68 publication indexing,
N+2 selection, type 1 exclusion, world/unknown passthrough, quality, lifecycle and
capacity remain.0 remains unlimited. Native admission omissions and continuity
are separate unresolved work; 69 adds no fade or renderer-capacity experiment.
# Retained: v 2.0.68 publication-owned lookup

Module 18 maintains a derived full-handle index over the existing four 512-slot
selection banks. The publication lock owns records, counts and sorted numeric
slot links. Zero initialization is empty; bank rotation clears heads; existing
slot updates do not reinsert links. No independent eviction, engine pointer,
new hook, allocation, native eligibility write or rendered-shadow cache.

Ordinary preparation copies validated native candidates first, then acquires
the registry once and copies their matching ownership records. Classification
uses stack-owned matches instead of materializing/indexing every bank. All active
banks participate, including old conflicting owners. Full 64-bit comparison,
bank/slot encounter order, newest same-owner selection and ties remain. Health
and population metadata describes the full registry, not projection size.
After 2048 chain visits, collision-heavy input falls back to full snapshot copying
under the same lock and the original matcher after unlock. Partial matches are
discarded; health is not double-counted. Detailed captures retain full records.

The coherent registry observation now follows candidate copying. Equivalent
inputs must produce equivalent decisions; identical concurrent interleavings
are not promised. No native reads, rendering or logging occur under this lock.
Publication insertion adds bounded work; lower hook time alone is not proof of
lower total mod cost. Pointer validation and selection remain per-call.

Retained: N+2, actual-near/outgoing/spare-forecast ordering, expiry, world/unknown
passthrough, type 1 exclusion from headlight slots, quality, capacity, lifecycle
and diagnostics.0 remains unlimited. The current native manager filter already
prevents downstream shadow work; earlier descriptor writes need independent
ownership/consumer proof.68 does not implement continuity/fade changes. Synthetic equivalence and the tester's high-load test are separate gates; no
game FPS improvement or visual acceptance is inferred from offline timings.

# Predecessor: v 2.0.61 limiter lookup footprint

Module 18 builds a 512-bucket index over the already copied, bounded selection
snapshot once per classification. The automatic index owns only numeric array
indices (10KiB); no engine pointer, persistent cache, allocation or lock is
added. Reverse insertion preserves original snapshot traversal order, including
owner conflicts and equal epoch/tick ties. Each candidate probes its hash bucket
and still compares the full 64-bit handle. Both headlight and capture-only type 1
matching use this same helper. Worst-case collisions remain bounded by snapshot
capacity; a hash collision is never treated as a match.

Normal limiter candidate copying skips diagnostic descriptor-flag extraction
and spatial-XYZ reading/validation. Existing node, descriptor and full-handle
readability checks remain. Captures retain all detailed fields through the
original wrapper. Admission/ranking uses no omitted field. Native next-link
restoration, publication, expiry, selection policy and all quality settings are
unchanged. This is CPU-work reduction, not a different shadow budget.

The actual-source harness compares 1840 indexed queries against an independent
linear reference over empty/full snapshots, collisions, conflicts and ties.
One dense fixture visits 2725 bucket records versus 471040 linear records, plus
the 2048-record index build. This is an operation-count comparison, not measured
CPU speedup or game FPS. Existing registry copying, per-candidate duplicate
scans, grouping/ranking and diagnostics bookkeeping remain optimization leads.
The original .61 measurement did not establish a game-speedup claim.

# Retained: v 2.0.60 coherent batch publication

Module 18 stages up to 64 validated scalar component observations in the
stack-owned native vehicle batch scope. The existing component hook reads its
handle after native update, retaining caller, TLS, skeleton, transform and
array-membership validation. No engine pointer survives the synchronous batch.
After native return, one nonwaiting registry acquisition publishes the group
to both selection and quality tables. The commit reads the renderer epoch under
that token, preventing pre-lock epoch capture from rolling a bank backwards.
Readers cannot see intermediate bulbs from a successful group commit.

The staging bound or conservative insufficient-capacity preflight rejects the
whole group before table mutation; contention rejects without waiting. Existing
gap/overflow counts now count rejected batch publications, not individual bulbs.
The registry-count invariant guarantees room in the handle-only quality table
whenever the selection reservation fits. No lock spans native execution, engine
reads, logging or rendering. The batch stack owns the copies until return.

This closes a source-level partial-publication window, not every cause of lost
classification. Four-epoch expiry, snapshot-lock fallback, native admission and
cached-resource behavior remain. Missing publications can still expire;
unknown/ambiguous lights pass through. Actual-source tests cover invisible
staging, common epoch, generation mismatch and rejected-group nonpublication.


Zero bypasses limiter preparation, not native admission or quality controls.
Positive limits can change the native mix of vehicle/world/type 1 work and add
CPU preparation overhead. Selected counts do not guarantee monotonic GPU/FPS.


# Selection and publication guarantees

Finite selection uses current renderer type 3 candidates with one complete 64-bit
handle instance, one unique recent owner association and a complete group of at
least two lights. Global allocator`0x025B0530` creates 32-bit slot+32-bit generation
handles; teardown`0x025B84D0` increments the generation before reuse. Full equality
protects ordinary slot reuse; renderer epochs are patch observation identities,
not native allocation generations. Four 512-slot banks retain deltas 0–3.

A failed publication tags its bank epoch+1 (zero means never invalidated).
Cumulative gaps/overflow are telemetry, not a permanent filter-disable latch.
Publisher in-flight counting starts before lock attempt and ends after commit
or failure tagging; snapshot copies then checks that count, closing the delayed
failure-tag race. Snapshot-lock failure, unavailable proof or malformed lists
fail open for that call; current-window gap/overflow/overlap marks degradation.
Missing, conflicting, duplicate, shared, incomplete and world lights remain
native individually. Degraded evidence cannot manufacture ownership.

The manager owns one synchronous list transaction: validate the complete bounded
chain, save original next pointers, preserve original order when filtering,
invoke the original once, and restore links immediately on return. Borrowed
candidate pointers never survive this call. Selection does not promote retained
owners in native order or guarantee native admission, update, GPU completion or
visible output. Type 1 vehicle lights stay outside the type 3 traffic quota;
that is not a universal siren tag or a separate physical resource pool.

Current primaries use squared distance with 0.9 incumbent weighting (about 5.1%
linear margin), numeric owner tie-break, and immediate entry for a clearly nearer
owner. The two extras prefer actual-near demand, outgoing grace and spare forecast,
as detailed in [incoming readiness](incoming-vehicle-readiness.md). Outgoing
retention lasts≤1000 ms from departure, never extended by observation; pressure
prefers newer departure, then nearer distance/owner. Promotion removes duplicates;
missing complete groups cannot be retained. No one-second primary hold or 300 ms
challenge remains. Predictions use 200 ms bounded approach and≤8 world units,
not camera visibility or incoming GPU readiness.

Module 18 owns 12 numeric residency slots. Primary admitted_tick is selection time;
outgoing admitted_tick is fixed departure time. Unsigned subtraction handles wrap.
Count/reset changes clear under the residency token; quality-only edits do not.
Degradation freezes ordinary resident identities until complete evidence resumes;
nonwaiting residency contention uses stateless main+2 choices for that call, not
a guarantee of the same owners. `primaryHandoffs` counts entrant calls;
`residencyPendingHolds` counts outgoing retention, not delayed incoming admission.

Build .80 C1/C2 has offline validation but no accepted runtime result yet. It retains 0 and gives explicit 10
Unlimited bypass; finite 1–9 remain. A fresh Global driver proof joins full owner
and entity ID, excludes that driver from traffic rank/residency (including an old
matching slot under degraded evidence), keeps even a partial driver lamp group,
and preserves its native type 1/type 3 quality request. Unknown identity retains
.79 policy. See [driver identity](driver-vehicle-identity.md) and
[saved settings](saved-settings.md). Neither control alters physical capacity.

# Diagnostic progression and rejected policies

| Boundary | Evidence and retained conclusion |
| --- | --- |
| .31 manager-call identity |Two-car control joins four lights; bridge 44–48/58–62 type 3 candidates.256-record table reaches 39,782 evictions without lock gaps. Stored manager counter 7,700–13,000 but local increment result always 1: strict-current ranking is invalid. CAS increment plus explicit global read is required on this TinyCC path; historical v 0.8.5 agrees. |
| .32 strict previous call |Two enabled pairs present, switched-off cars absent; distant special-event pair 112–129 units. Bridge 22–25 exact groups/15–20 delta 1; stopped 19–26/17–26. Four/eight always simulated. Fresh≤16 ms records also delta 2–4, none≥5/future/zero; 406,134 evictions. Manager call is not shared lifetime epoch; continuous oldest replacement is too expensive. Age bands 0–16/17–50/51–250/>250 ms are telemetry, not TTL. |
| .33 four-bank shape |Zero overflow/contention replaces eviction storm.30–32 exact bridge pairs; same/previous covers 36–56/60–64 lights, 6–24 are 2–3 epochs old; none older/future. Four banks cover observed evidence; generation safety required independent native allocation proof. |
| .34 global-gap latch |290,490 candidates suppressed/7,851 active calls, 1,867 fail-open, eight historical gaps, no overflow; F10 still 25–35 complete groups/eight would-keep. A nonzero lifetime gap total incorrectly disables all later filtering. Simulation is not mutation proof. |
| .35 epoch failure |8,233/8,941 calls filter 235,532 candidates; exactly three calls bypass for three gap epochs.19–20 complete groups/eight selected, balanced lifecycle, peak 29/30. Proves recovery, not downstream selected-headlight admission. |
| .36 admission correlation |Exact stack sample marks protected groups; copied 0x18 native bindings classify full/partial/absent after return. Ten evaluated samples admit all four owners/eight faces concurrently with 2–4 vehicle-owned type 1 lights. Rank 4/5 swaps identify sampled whole-owner popping, not siren displacement.544 bank overflows produce 72 epoch failures, one captured recovery. |
| .37 distance residents |One-second minimum plus 300 ms same challenger and≤0.75 squared distance (~13.4% closer) before replacement. F10 retains four/eight, suppresses 96–98; 27,361 evaluated/14,182 active/40 degraded/no whole-call failure.23–26 faces, peak 29/30; world/unknown lights refill capacity.13/70,629 completions 8–16 ms, none≥16 ms; ownership clean. No measured FPS gain; logger truncates at residencyLockBypa. |
| Distance-only counterexample |A passing nearer vehicle removes an already visible parked-car shadow. Longer timer/margin merely delays the same decision; distance is not visible receiver contribution. Separately enabling additional world shadows can refill freed capacity. |
| .38/.40 stable-plus-overrides |Four stable exact scene residents, native-order vacancy fill; two additive nearest overrides alone use 1 s/300 ms/0.75 replacement. Twelve slots support 1–10 plus 2, 0 bypass. Degradation freezes, resets are owned. This was superseded by .58 nearest primaries and later actual-near/outgoing/forecast policy. Police priority remained unmapped. |
| .58/.59/.60 coverage |.58 report: 4+ improved but nearby sprinting losses at 1; 11,094/40,086 degraded calls, often 26 faces. .59 had 0.7–1.4 ms sampled preparation, peak degraded 1,563 ms/141 calls (not a game freeze). Two handles0x2000009CC/9CB lose joins in one sample and remain native at 4096/512; recurring eight headlights stay 512; no proof the same light flips quality. .60 corrects per-bulb/pre-update/pre-lock publication, not every expiry or flicker cause. |
| .61–.69 costs |.60 four preparation calls 853.4/912.7/832.3/799.4 us with 144–147 candidates and 1,232–1,559 registry records. .61 indexed proof and .68/.69 mechanisms above reduce repeated work. Runtime samples and uncontrolled overlay FPS are recorded in [workload evidence](workload-capture.md); evolving scenes prevent causal FPS claims. |

Detailed type 1/protected-owner scans run only in armed F10. A representative light
is not complete vehicle visibility; concurrent type 1 and protected loss would
still not establish causation. Exact recent joins, safe fallbacks and restored
links remain mandatory even when those choices reduce the effective limiter.
