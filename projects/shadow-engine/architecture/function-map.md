---
type: Reverse Engineering Map
title: Shadow Engine Function Map
description: Community-facing navigation for verified engine-function and subsystem roles.
tags:
- shadow-engine
- reverse-engineering
- functions
- rva
- navigation
status: draft
sources:
- resource: ../validation/regional-runtime-matrix.md
  title: Regional feature coverage and automatic compatibility validation
- resource: driver-vehicle-identity.md
  title: Current Driver Vehicle Identity
- resource: population-observation.md
  title: Shadow Population Boundary Observation
- resource: startup-supervision.md
  title: Delayed Shadow Initialization
- resource: menu-host-compatibility.md
  title: Shadow Engine Menu Host Compatibility
- resource: world-quality-validation.md
  title: World Quality Validation Overhead
- resource: detail-window-observation.md
  title: Explicit Detailed Observation Windows
- resource: periodic-summary-transport.md
  title: Worker-Owned Periodic Summary Output
- resource: overhead-measurement.md
  title: Whole-Mod Overhead Measurement
- resource: completion-diagnostic-overhead.md
  title: Completion Diagnostic History Lookup
- resource: renderer-queue-validation.md
  title: Renderer Queue Validation and Overhead
- resource: mod-performance-audit.md
  title: Measuring native patch overhead without confusing it with frame cost
- resource: wd1-shadow-eligibility.md
  title: WD1 Shadow Eligibility and Work Boundary
- resource: wd2-headlight-selection.md
  title: WD2 Headlight Owner Selection and Publication
- resource: wd2-local-shadow-pipeline.md
  title: WD2 Local Shadow Admission and Fade Consumption
- resource: wd2-shadow-reference.md
  title: WD2 Shadow Reference and WD1 Port Boundaries
- resource: incoming-vehicle-readiness.md
  title: Incoming Vehicle Shadow Readiness
- id: private-lua-frame-design
  resource: lua-frame-fix-design.md
  title: Lua Frame Compatibility Fix Design
- id: private-lua-stack
  resource: lua-stack-compatibility.md
  title: WD1 Lua Packed Frame Size and Garbage Collection
- id: private-distance-quality
  resource: distance-shadow-quality.md
  title: Distance Shadow Quality Controls
- id: private-internal-tools
  resource: internal-tools.md
  title: Lua-to-native bridges and shared-control ownership experiments
- id: private-vehicle-selection
  resource: vehicle-shadow-selection.md
  title: Vehicle Shadow Selection Diagnostic
- id: private-vehicle-retirement
  resource: vehicle-retirement-diagnostics.md
  title: Tracked Vehicle Retirement Diagnostics
- id: private-vehicle-provenance
  resource: vehicle-light-provenance.md
  title: Vehicle Light Component to Renderer Provenance
- id: private-headlight-resource
  resource: headlight-resource-diagnostics.md
  title: Headlight Shadow Resource Diagnostics
- id: private-vehicle-quality
  resource: vehicle-shadow-quality.md
  title: Vehicle Shadow Quality Boundary
- id: private-black-flicker-method
  resource: black-flicker-diagnostics.md
  title: Black Shadow Flicker Attribution
- id: private-runtime-profiles
  resource: runtime-profiles.md
  title: Runtime Profile Architecture
- id: private-shadow-pipeline
  resource: shadow-pipeline.md
  title: Shadow Engine Pipeline
- id: private-capacity-layout
  resource: engine-capacity-layout.md
  title: Shadow Capacity Layout
- id: private-shadow-pressure
  resource: shadow-pressure.md
  title: Shadow Pressure Boundaries
- id: private-vehicle-classification
  resource: vehicle-light-classification.md
  title: Vehicle-Light Classification Boundary
- id: private-result-lifecycle
  resource: external-slice-results.md
  title: External Slice Results
- id: private-cloth-investigation
  resource: ../research/cloth-high-fps-investigation.md
  title: Watch Dogs 1 High-FPS Coat Physics Investigation
- id: private-movement-investigation
  resource: ../research/player-movement-high-fps-investigation.md
  title: Watch Dogs 1 High-FPS Player Movement Investigation
- resource: saved-settings.md
  title: Persisting mod policy without blocking native callbacks
- resource: ../compatibility/wd2-reference.md
  title: Watch Dogs 2 Shadow Architecture Reference
---

# Scope

The [engine fundamentals primer](../research/engine-fundamentals.md) introduces
rendering, resource ownership and evidence interpretation before the detailed mappings.

This map navigates semantic roles, owners, evidence and limits. RVAs identify locations in a particular build; they are not portable function identities. Detailed proofs belong to the linked concepts. Native engine mappings and mod-owned policies are distinguished below. Dense-driving shadow continuity remains an unresolved observation, not a proved cache-capacity defect.

# Engine boundaries and mod implementation consumers

The [control API reference](control-api.md) owns exported signatures, saved-word
layouts, versioned request/status fields and their acceptance semantics.

| Concept | Role, consumers and evidence boundary |
| --- | --- |
| [Runtime profiles](runtime-profiles.md) | Select one coherent supported executable before common policy uses immutable mappings; unknown/ambiguous images remain read-only. Static corpus coverage and live profile acceptance are distinct. |
| [Runtime architecture](runtime-architecture.md) | Unity composition and subsystem state ownership; regional data is separate from common mechanism and policy. |
| [Patch transactions](patch-transactions.md) | Complete preflight, journaled writes and bounded rollback. Trampolines publish before reachable detours; failed executable restoration preserves reachable allocations/bindings. No concurrent atomic-replacement claim. |
| [Startup supervision](startup-supervision.md) | Module 80 pinned worker owns safe-early discovery and responsibility after hooks commit; module 70 owns deferred validation/one-shot mutation/rollback; module 60 owns constructors; module 75 reports terminal reason without owning installer state. |
| [Shadow pipeline](shadow-pipeline.md) | Manager admission -> queue production -> renderer consumption; locate the first broken boundary rather than inferring cause from visuals. |
| [Capacity layout](engine-capacity-layout.md) | Coupled construction, map loops, three queue regions, 46 embedded references, pass envelope and result capacity. Bounded native count/mask/name-array audit does not prove all GPU consumers or five/six-face layouts. |
| [Shadow pressure](shadow-pressure.md) | Global002E9B60 owns ordinary admission and cached-owner age/update selection;002E2470 allocates/rebinds cache owners;002C0500 constructs static backing.00308A90 supplies profile count/size/B0 and invokes native rebuild on count/size changes.30 physical maps, B4, A8 and reserve8 are distinct. Age/new-owner policy is static proof, not a diagnosed game delay; initialization flags are not GPU readiness. [Cost/capacity assessment](shadow-pressure.md#more-shadow-casting-lights-at-lower-frame-cost) separates sampled admission pressure, nominal resolution savings and unmeasured GPU cost. |
| [WD1 eligibility](wd1-shadow-eligibility.md) | Global002E9B60 admits the first24 ordinary-eligible records in the sampled normal21/4 profile. Corrected producer:003CA2E0 allocates the holder;002DFF40 schedules0048D7E0 priority/distance sorting and0048CE20 candidate construction/distance fade.002D66D0 schedules002CC700 conditional query-result writes to C+78 before003C6CE0 consumption. The old003DC780 virtual-slot+20 attribution confused depth textures with the candidate holder. Factory001EFE10 creates the occlusion query;001EA240/001E2550 read nonblocking DONOTFLUSH data through0034D3C0. 0031A8C0 maps C+68 and its complement into registered LightShadowFactor;0031B3B0 caches blocks, while00490AD0/00490A00 build and publish fresh command data. The retired lighting-side onset experiment is documented under incoming readiness; descriptor mutation ownership, initial coverage and query issuance remain incomplete;472 sampled eligible pairs split at rank24. |
| [Vehicle classification](vehicle-light-classification.md) | Type 3 alone cannot distinguish vehicle and world spotlights. Retrospective F10 joins, update skipping and fixed TTL do not prove same-frame classification/lifetime safety. |
| [Vehicle provenance](vehicle-light-provenance.md) | Shared update ABI and native handle/transform chain. Global 0x00BA7570 appears in CVehicleDynamicLight/CVehicleHeadLights metadata; 0x0093D730 encloses component traversal and 0x0093D8E7 is its virtual+0x30 callsite. Spatial+0x50 is a descriptor handle; first-Spotlight3 and conditional updates limit completeness. Copied callers/skeleton words are evidence, not lifetime pins. |
| [Owner and skeleton lifetime](vehicle-owner-lifetime.md) | CVehicle class/update/light-array chain and graphics-owned skeleton creation/cleanup. Four-image batch proof and 172 initial Global copied-owner correlations do not establish native generation/retirement coverage. |
| [Tracked retirement](vehicle-retirement-diagnostics.md) | Common CVehicle teardown and cleanup/base callees across Global/VMPless/Complete/Asia; void-owner ABI, numeric copied identity and nonwaiting gaps. Initial Global installation/93 F10 links had no gaps but no observed tracked teardown. |
| [Selection](vehicle-shadow-selection.md) | Module 18 whole-batch post-update publication, four renderer-epoch full-handle banks, candidate projection/index fallback, grouping/ranking/residency and synchronous changed-link restoration. .60 staged whole-batch publication, .61/.63 bounded indexes, .64/.66 scoped validation, .68 maintained indices and .69 address ordering are retained source-cost steps. |
| [Selection implementation cost](vehicle-shadow-selection.md) | .79 classifier owns temporary group/rank indices; thin disabled wrapper initializes headers while enabled helper owns large scratch storage. Publication and readers share the existing lock. These are source/compiler roles, not new native RVAs or FPS proof. |
| [Population boundary](population-observation.md) | Distinct native boundaries separate eligibility, selection, admission, cache refresh, CPU resource wrappers, physical capacity and visibility. .87 P-A review establishes sampled native-order admission competition with consistent cache/resource behavior; a safe replacement policy is not selected. FPS measurement is independent. No capacity/fade mechanism follows from static mappings alone. |
| [Population observation](population-observation.md) | Module19 owns1200 sampled50ms buckets perstream, automatic60-second stop, ticket-drained binary export and CRC; modules20/30 supply candidate, binding/cache and renderer boundaries. Module75 routes independent onset controls and SE9 countdown/status; the offline decoder validates complete numeric payloads. Each queue phase uses fresh region checks. Optional Global proofs cover context lookup and integer-area normalization; reconstructed gates remain distinct from native output and GPU readiness. |
| [Incoming readiness](incoming-vehicle-readiness.md) | Global local-player XYZ proof corrects the old camera-derived batch distance. Other profiles retain their native reference. Conditional near/outgoing/forecast extras do not guarantee native admission or first visibility. The retired .90 Global experiment borrowed0031A8C0 population before publication and ramped only the native shadow-factor pair over180ms, with scalar full-identity history and no admission/distance change. Offline ABI/rollback/clock tests are not visual acceptance. |
| [Driver identity](driver-vehicle-identity.md) | .82 C1-D2 uses Global CPawn+90 direct vehicle reference, fresh pawn/player full-ID agreement, native flags, component-cache and first driver-role seat. Predicate00948370 and CPawn caller00AE6530 have exact startup guards. Scoped copies/rechecks never call creating resolvers or retain driver pointers. Selection joins copied CVehicle/full-ID publication; .83 removes the temporary quality consumer. The .81 failed keyed route is removed. Offline proof and four Global selection/quality samples pass; traffic continuity and FPS acceptance remain open. Other profiles retain ordinary policy. |
| [Vehicle quality](vehicle-shadow-quality.md) | Exact vehicle-handle type-1/type-3 caps preserve lower native requests and uncertain/world/shared identities. Emergency data tags lack a proven runtime priority field. .80–.82 temporary driver exemption was validated; .83 removes it and its quality-only lookup/payload, restoring one vehicle cap while keeping limiter protection. Optional .89 background policy uses fresh full-ID/position copies and a bounded hysteresis history at the existing request boundary; Off preserves the prior path, resource/visual acceptance remains separate. |
| [World validation](world-quality-validation.md) | Fresh stack readability scope within the separate world token plus one shared identity hash. World missing-identity behavior differs from vehicle passthrough; no cross-call memory or resource cache. |
| [Quality validation](vehicle-shadow-quality.md) | Q1 verifies a fresh bounded dimension span inside each pass token and skips requests with both axes within cap; failed proof uses the complete legacy path. Q2 exposes inspected-entry coverage separately from complete captures. Frozen-.75 comparison and later scoped runtime acceptance differ from GPU proof. |
| [Saved settings](saved-settings.md) | Module 17 owns durable settings; module 16 routes changes, module 80 initializes before consumers, module 75 transports and Lua presents scalar intent. Validate/save/replace precedes publication. Experimental .80 uses SES2/SE6; no engine pointer enters persistence. |
| [Host callbacks](menu-host-compatibility.md) | Exact inspected NexusTools slider setter echoes, queued edits, Script properties and NextTick drain/lifetime. Desktop behavior tests require a separate all-prototype 31-register gate: oversized module roots can pass desktop tests while the target menu fails. Host scheduling and Global repair do not replace that check. |
| [Internal tools](internal-tools.md) | Pinned-worker mailbox, native settings and singular ambient-traffic owner. Module76 sequences independent collectors from one request, tracks exact serials/epochs, preserves held tickets and exports a bounded ZIP with coverage gaps. SEB1 reports progress separately from SE10; UI completion is not visual/GPU acceptance. |


[NexusTools initialization](../compatibility/nexustools-init.md) maps separate 1.1.12/1.1.13
CustomLuaManager guards and the optional-repair isolation boundary. Host layout
proof is distinct from shadow activation and Lua lifecycle acceptance.

# Resource and diagnostic owners

| Concept | Role and limits |
| --- | --- |
| [External results](external-slice-results.md) | Native 17-entry record+0x70 array; higher indices use producer-cycle storage with exact per-acquisition retirement. Global frame graph 0x003E0F80, loop 0x003E1727, wrapper batch 0x003E17A6 and pre-finalizer 0x003E19E3 -> 0x003E0E70 (epilogue 0x003E19F4) are distinct. Asia tail/finalizer 0x00A584E3/0x00A57940. RBX/RDI are renderer/record. Release 0x003C1350 is too early; post-return cleanup too late; finalizer owns acquisition/retention, not release. |
| [External completion evidence](external-slice-results.md) | Scheduler Global 0x002D6070 / Asia 0x008F0E90 receives entry/result index as argument 3 and face index as 4; final face publishes. Producer Global 0x00306E60 / Asia 0x00940510 encloses the full loop, argument 7 = record+0x70. Producer return is not completion. .10 zero builder markers/complete pre-finalizer masks led to .11 producer-owned opening and observation-only builder; no missing join or safe blocking dependency was proved. |
| [Black-flicker method](black-flicker-diagnostics.md) | First-invalid-boundary lookup/builder/task/use tracing isolated indexed stores; later intersection symptom remains distinct. Similar appearance, balanced ownership or clamps alone do not identify a writer or receiver. |
| [Intersection recorder](intersection-diagnostics.md) | Three shared-lookup returns feed +0x100/+0xF8/+0x110. Fresh caller/store/callee proof, nested TLS, bounded copied events and worker output. Four-profile static evidence; no ground draw/GPU/cache binding attribution. |
| [Resource diagnostics](headlight-resource-diagnostics.md) | Four regional candidate/request/resource CPU consumers; split pre-policy, post-policy and native-return copies. Global00306E60 creates missing backing;00430A80 reuses resource-keyed CPU request wrappers and00426AF0 constructs/pools them. Persistent backing can bypass resize. No later dereference of retained pointers, GPU generation, readiness or safe invalidation API is proved. |
| [Known-serial lookup](completion-diagnostic-overhead.md) | Sole publisher uses masked ring position; .71 validates exact slot atomically. Unknown-ID completions still search oldest pending and count ambiguity. Resource ownership is independent. |
| [Detailed windows](detail-window-observation.md) | Module 19 owns epochs/history/report copies. .74 numeric TLS and scalar tickets close producer scope independently of optional seals; module 20/30 tickets retain observation identity. Asynchronous completion correlation is heuristic, never a native fence. |
| [Periodic transport](periodic-summary-transport.md) | Module 14 copied-scalar mailbox carries module 30 residency data to module 75 worker, releasing the slot before I/O. Nonwaiting publication; urgent/manual lines remain synchronous; no later native dereference. |
| [Overhead measurement](overhead-measurement.md) | Module 12 worker-owned windows, token/inflight lifetime and sampled nonadditive intervals. H2 mandatory lifecycle lookup remains outside diagnostic compilation. |
| [Workload capture](workload-capture.md) | Sampled manager/preparation/restore and renderer intervals; .84 own-process private sequential DXGI ETW, post-stop file consumption and owned cleanup. No Present hook or elevation request. Actual ordinary-token DXGI delivery is tested; incomplete/occluded data keeps FPS unknown. Provider/file overhead and visible game acceptance remain separate gates. |
| [Performance diagnostic](vehicle-performance-diagnostics.md) | Existing .59 manager/renderer timing and copied movement/admission analysis; no new native hook. |
| [Queue validation](renderer-queue-validation.md) | Module 30 whole-record prefix, count restoration and face-cost consumer. Successful queue-region proof lasts one synchronous callback; pointed resources retain individual checks. |
| [Whole-mod audit](mod-performance-audit.md) | Complete source-confirmed frequency/ownership inventory and finite dispositions, not FPS attribution. |

# Resolution and Lua mappings

[Distance research](distance-shadow-quality.md) owns Global builder 0x0030A570, existing-texture dimension getter 0x0025DBF0, renderer 0x00306E60 backing reuse and profile callback 0x00308A90. Builder argument 4 +0x1E0/+0x1E4/+0x1E8 supplies view XYZ as manager 0x002E9B60 argument 6; spatial+0x08/+0x0C/+0x10 is local-light position and +0x14/+0x18/+0x1C direction. Type 0 is separate. Historical .47 distance consumers were removed; byte checks do not prove world units, safe resource transitions or a distance-only LOD table.

[Lua frame compatibility](lua-stack-compatibility.md) maps captured Global compiler 0x1DA670/0x1DA6D0, loader 0x1D9F65, frame setup 0x1C296D and GC traversal 0x1C35E0. A constructor needing 51 registers declared 19 because of five-bit truncation. The independent four-bit upvalue limit maps A4EE compiler increment004E7031, binding emission004E75C8 and VM construction004D863A; register compliance alone misses16 captures wrapping to0. Prototype allocation/free, initializer, verifier, load/dump and host-init guard roles remain separately documented. The experimental 17-site frame repair is integrated from .57, with Global first-run success and five-region offline mapping in .95; storage/activation/lifecycle and new regional runtime acceptance remain incomplete; [repair design](lua-frame-fix-design.md) retains those gates.

The related stale item-24 trace maps Global concatenation 0x1C5800, buffer helper 0x1C8CA0 and global buffer+0x58/capacity+0x68. The child aliased non-GC scratch storage while absent from rootgc. Captured heap/code establish roles and a rooting defect, not a recorded historical sweep or mod-specific trigger.

# Successor-engine research

[WD2 shadow reference](wd2-shadow-reference.md), [headlight selection](wd2-headlight-selection.md) and [local-shadow pipeline](wd2-local-shadow-pipeline.md) own successor-only analysis VAs: manager Update 0x186A79ADB, shadow-only publication 0x186B655F2, general admission 0x186E24E40, post-admission special-class ordering 0x186DA3A60, distance factor 0x186E2A620 and LightData shading consumer 0x186D526A0. Dispatch/lifetime and player/view/distance/angular inputs are separate from static-cache scheduling. These do not prove temporal replacement, dithering, GPU readiness or a siren pool. [WD1 adaptation limits](wd2-shadow-reference.md) records independent ownership/early-gate/transition/lamp-role prerequisites; none of these VAs is a WD1 hook.

# Historical cloth and movement research map

These experiments belong to the focused [cloth investigation](../research/cloth-high-fps-investigation.md) and [movement investigation](../research/player-movement-high-fps-investigation.md). They are Global/04DF evidence and are excluded from current shadow policy. The [WD_DTCLAMP review](../research/wd-dtclamp-comparison.md) distinguishes its claimed Havok accumulator from the mapped SecondaryMotion solver; its external RVA fails the required instruction in the captured Global image, and static trampoline defects do not establish runtime coat connection or a 30 Hz scheduler.

| Boundary | Confirmed role and experimental limit |
| --- | --- |
| GEOM/XBG torso path | Aiden-torso parser/generic wrapper runtime-proven. An exact direct pointer from coat resource to selected 130-node CLOTH solver remained unproved. |
| 0x00C171F0 -> 0x00C16ED0 -> 0x00C16BD0 | Named SecondaryMotion callback -> adapter -> per-instance solver. Solver state owns object type/node count; context+0x130 supplies a fixed 1/30 s input shared across states/threads. Context cannot be the instance clock. |
| Adapter 0x00C16ED0 | Complete 0x170-byte value copy. Its argument 4 is persistent source identity; argument 2 is worker-stack-local. Solver argument 1 is the adapter's temporary copy; adapter argument 1 becomes solver argument 2. Native pointers and actual ABI matter. |
| Source/instance timing | Stable source classifier can span multiple instances. The apparent instance argument was narrower but later found stack-local; direct timing ownership cannot be inferred from temporary addresses alone. |
| Source first float4 | Acceleration consumed with dt^2. A private aligned value copy can isolate source mutation; per-call substitution still inherits submission frequency. |
| 0x00C168E0 | Publisher copies completed solver transforms into shared output and marks dirty entries without integration. It requires actual solver arguments 1 and 3; calling it from adapter arguments violates its boundary. |
| Type-0 native tail | Pose finalizer 0x00B69FA0 -> animation/physics blend 0x00C15EA0 -> publisher 0x00C168E0. Fresh non-integrated tuples can overwrite solved transforms despite executing publisher side effects. |
| Publisher argument 2 | Static 0x38-byte output-owner wrapper: descriptor+0x00, transform-output+0x20, dirty-state+0x30. .26 traced wrapper/all seven pointer fields and source/solver provenance; live exact owner identification was still pending. |
| 0x0272EAC0 | CCharacterControllerJob: job+0x130 controller and +0x138 float delta. It forwards to primary movement/timers 0x027292F0, collision/contact 0x02729490, final state/output 0x026CC230. One submission owns one completion; coherent carrier does not mean safe suppression. |
| 0x02727FF0 | Receives primary native timestep. A 499-instruction reachable CFG preserves it to 0x027287D7 storing controller+0x188, then 0x027287EE storing reciprocal at +0x18C. Earlier same-update readers see the preceding pair. |
| 0x027277A0 and lower callees | Neighbor consumes +0x188. Resolved callees are Havok support/collision/contact/stale-contact work, not proved yaw/turn arithmetic; apparent table is .pdata unwind metadata, not a vtable. Desired-motion/orientation ownership remains unresolved. |

The linked investigations own experiment counts and detailed failure controls.
The main lessons are:

- Solver-context substitution, adapter suppression and repeated refresh integration
  altered timing or presentation and failed in different ways.
- Correct native arguments are mandatory for publisher replay; adapter-level
  guesses crashed. Later replay improved one control but did not eliminate
  hands-in-pockets clipping/flicker.
- Output caching and source substitution did not establish a safe fixed-rate
  solver. Fresh unsolved tuples and native fallback cadence remained important.
- Whole movement-job suppression, shared delta mutation and primary-only delta
  substitution each broke world/collision behavior or crashed. Mapped timestep
  consumers do not authorize suppressing the owning job.
