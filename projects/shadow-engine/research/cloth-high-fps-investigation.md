---
type: Reverse Engineering Status
title: Watch Dogs 1 High-FPS Coat Physics Investigation
description: Current evidence, rejected owner cadence, and the recovered Global SecondaryMotion
  solver timestep experiment for Aiden's coat.
tags:
- shadow-engine
- cloth
- smu
- geom
- xbg
- diagnostics
status: draft
sources:
- id: coat-model-evidence
  resource: ../../../evidence/catalog.json#E-1dc5767449e1
  title: Aiden coat GEOM/XBG SMU model evidence
- id: cloth-research
  resource: ../../../evidence/catalog.json#E-84ea28e92dbc
  title: Watch Dogs 1 cloth high-FPS research
- id: ssm-result
  resource: ../../../evidence/catalog.json#E-6aea597a3f47
  title: Three-reader SSM dispatch result
- id: archived-probe
  resource: ../../../evidence/catalog.json#E-f2fd7a05edd3
  title: Historical unvalidated GEOM loader probe
- id: corpus-manifest
  resource: ../../../evidence/catalog.json#E-cb00e25d0849
  title: Five-profile runtime corpus manifest
- id: torso-provenance
  resource: ../../../evidence/catalog.json#E-02e6a77e7d52
  title: Promoted Scratch evidence manifest
- id: candidate-report
  resource: ../../../evidence/catalog.json#E-fe73a453ad7c
  title: v2.0.1 offline diagnostic report
- id: global-runtime-result
  resource: ../../../evidence/catalog.json#E-008bf3d261ad
  title: v2.0.1 Global GEOM runtime result
- id: geom-caller-export
  resource: ../../../evidence/catalog.json#E-12804f64dcaa
  title: Runtime-proven GEOM wrapper decompile
- id: geom-upstream-exports
  resource: ../../../evidence/catalog.json#E-5e0294fdd917
  title: GEOM wrapper upstream resource-load path
- id: lifecycle-candidate
  resource: ../../../evidence/catalog.json#E-7deb2d44a199
  title: v2.0.2 Global resource-lifecycle diagnostic
- id: lifecycle-result
  resource: ../../../evidence/catalog.json#E-0dd8538add4e
  title: v2.0.2 Global resource-lifecycle runtime result
- id: geometry-child-constructor
  resource: ../../../evidence/catalog.json#E-f443858722ca
  title: CGeometryResource secondary-motion child constructor
- id: geometry-child-schema
  resource: ../../../evidence/catalog.json#E-bb845ed5c55f
  title: Secondary-motion child schema registration
- id: secondary-motion-candidate
  resource: ../../../evidence/catalog.json#E-97a4cf286b42
  title: v2.0.3 secondary-motion definition diagnostic
- id: secondary-motion-result
  resource: ../../../evidence/catalog.json#E-525b8d424b3a
  title: v2.0.3 Global secondary-motion definition result
- id: resource-consumer-candidate
  resource: ../../../evidence/catalog.json#E-d2ed6c2bc5e9
  title: v2.0.4 Global resource-consumer diagnostic
- id: resource-consumer-result
  resource: ../../../evidence/catalog.json#E-755901cb032b
  title: v2.0.4 Global resource-consumer result
- id: instance-owner-candidate
  resource: ../../../evidence/catalog.json#E-4b00d1eaf694
  title: v2.0.5 Global geometry-instance owner diagnostic
- id: instance-owner-result
  resource: ../../../evidence/catalog.json#E-fe955c56c57d
  title: v2.0.5 Global geometry-instance owner result
- id: model-part-owner-candidate
  resource: ../../../evidence/catalog.json#E-ce094fa013d3
  title: v2.0.6 Global model-part owner diagnostic
- id: model-part-owner-result
  resource: ../../../evidence/catalog.json#E-fcde051dba4e
  title: v2.0.6 Global model-part owner result
- id: owner-rebuild-candidate
  resource: ../../../evidence/catalog.json#E-1d206d309505
  title: v2.0.7 Global owner-rebuild diagnostic
- id: owner-rebuild-result
  resource: ../../../evidence/catalog.json#E-c14f5d4ec1ed
  title: v2.0.7 Global owner-rebuild result
- id: owner-update-candidate
  resource: ../../../evidence/catalog.json#E-0bff55f18ab7
  title: v2.0.8 Global owner-update cadence diagnostic
- id: owner-update-result
  resource: ../../../evidence/catalog.json#E-fa6a02e242b3
  title: v2.0.8 Global owner-update cadence result
- id: owner-cadence-experiment
  resource: ../../../evidence/catalog.json#E-19019a019e0d
  title: v2.0.9 Global owner 60 Hz cadence experiment
- id: owner-cadence-result
  resource: ../../../evidence/catalog.json#E-b68cc28e1cd2
  title: v2.0.9 rejected Global owner cadence result
- id: secondary-motion-update-chain
  resource: ../../../evidence/catalog.json#E-fc66e12bc789
  title: SecondaryMotion update dispatch chain
- id: secondary-motion-solver
  resource: ../../../evidence/catalog.json#E-23a2e09f3bc0
  title: SecondaryMotion per-instance solver
- id: secondary-motion-timestep
  resource: ../../../evidence/catalog.json#E-e354f47c04a3
  title: SecondaryMotion timestep consumer and builders
- id: solver-wall-delta-experiment
  resource: ../../../evidence/catalog.json#E-feb12628d46e
  title: v2.0.10 solver wall-delta experiment
- id: solver-wall-delta-result
  resource: ../../../evidence/catalog.json#E-c2914a3203fb
  title: v2.0.10 Global solver wall-delta result
- id: solver-state-wall-delta-experiment
  resource: ../../../evidence/catalog.json#E-8568dc1e950f
  title: v2.0.11 solver-state wall-delta experiment
- id: solver-state-wall-delta-result
  resource: ../../../evidence/catalog.json#E-7b21e926cd81
  title: v2.0.11 Global crash result
- id: solver-crash-function
  resource: ../../../evidence/catalog.json#E-fd2e65f7d3c3
  title: v2.0.11 faulting solver helper
- id: solver-crash-instructions
  resource: ../../../evidence/catalog.json#E-d0cb96933027
  title: v2.0.11 exact fault instruction window
- id: adapter-source-wall-delta-experiment
  resource: ../../../evidence/catalog.json#E-abb897f14ccf
  title: v2.0.12 adapter-source wall-delta experiment
- id: adapter-instructions
  resource: ../../../evidence/catalog.json#E-7681556ebb7e
  title: SecondaryMotion adapter exact instruction window
- id: adapter-source-wall-delta-result
  resource: ../../../evidence/catalog.json#E-8aeadcdc1262
  title: v2.0.12 Global adapter-source wall-delta result
- id: adapter-instance-wall-delta-experiment
  resource: ../../../evidence/catalog.json#E-e6d9b6e8c455
  title: v2.0.13 adapter-instance wall-delta experiment
- id: adapter-instance-wall-delta-result
  resource: ../../../evidence/catalog.json#E-e67848ff6720
  title: v2.0.13 Global adapter-instance wall-delta result
- id: smoothed-timing-force-experiment
  resource: ../../../evidence/catalog.json#E-e359d7b2838c
  title: v2.0.14 smoothed timing and force experiment
- id: smoothed-timing-force-result
  resource: ../../../evidence/catalog.json#E-6ac03dd3313d
  title: v2.0.14 Global smoothed timing and force result
- id: adapter-fixed-rate-experiment
  resource: ../../../evidence/catalog.json#E-d843630d169d
  title: v2.0.15 adapter fixed-60-Hz experiment
- id: adapter-fixed-rate-result
  resource: ../../../evidence/catalog.json#E-bc3926c97048
  title: v2.0.15 Global fixed-rate adapter result
- id: budgeted-presentation-experiment
  resource: ../../../evidence/catalog.json#E-4bc8e3153a8c
  title: v2.0.16 60 Hz budgeted-presentation experiment
- id: budgeted-presentation-result
  resource: ../../../evidence/catalog.json#E-8d42eaea36a8
  title: v2.0.16 Global budgeted-presentation result
- id: output-finalizers
  resource: ../../../evidence/catalog.json#E-f8dd43c25b75
  title: Global SecondaryMotion output finalizers
- id: source-clock-replay-experiment
  resource: ../../../evidence/catalog.json#E-627844dfc56c
  title: v2.0.17 source-clock output-replay experiment
- id: source-clock-replay-result
  resource: ../../../evidence/catalog.json#E-0e0f0790cb9d
  title: v2.0.17 Global output-replay crash result
- id: nested-solver-replay-experiment
  resource: ../../../evidence/catalog.json#E-aecae02f4d6a
  title: v2.0.18 nested-solver output-replay experiment
- id: nested-solver-replay-result
  resource: ../../../evidence/catalog.json#E-741fa09d51e7
  title: v2.0.18 Global nested-solver replay result
- id: nested-solver-replay-video
  resource: https://www.youtube.com/watch?v=SxiunEFl7HI
  title: Public v2.0.18 fixed-rate cloth simulation with pose replay
- id: solved-output-cache-replay
  resource: ../../../evidence/catalog.json#E-5950598649d6
  title: v2.0.20 solved-output cache replay
- id: solved-output-cache-runtime-rejection
  resource: ../../../evidence/catalog.json#E-29704cec2cf3
  title: v2.0.22 solved-output cache visual rejection
- id: v2023-runtime-baseline
  resource: ../../../evidence/catalog.json#E-fc1ab9f7bc57
  title: v2.0.23 accepted continuation baseline
- id: output-tail-recovery
  resource: ../../../evidence/catalog.json#E-968d1376e40a
  title: Global cloth output tail and lower movement boundary
- id: v2024-runtime-rejection
  resource: ../../../evidence/catalog.json#E-496e8abdc27f
  title: v2.0.24 Global complete output-tail replay rejection
- id: v2025-solved-tuple-replay
  resource: ../../../evidence/catalog.json#E-24ff1e81b475
  title: v2.0.25 Global solved-tuple replay candidate
- id: v2025-runtime-rejection
  resource: ../../../evidence/catalog.json#E-80b27cfea130
  title: v2.0.25 Global solved-tuple replay rejection
- id: v2026-output-owner-tracer
  resource: ../../../evidence/catalog.json#E-b48cbd67a094
  title: v2.0.26 Global publisher output-owner tracer
- id: diagnostic-source
  resource: ../../../evidence/catalog.json#E-a3a09f241a70
  title: Diagnostic-only GEOM probe
- id: profile-source
  resource: ../../../evidence/catalog.json#E-1f29073db08d
  title: Immutable runtime profiles
---

# Scope and retained experimental mechanism

This is the separate Global cloth investigation, not a feature included in the
current production shadow pipeline. The accepted experimental continuation is
v 2.0.23, whose cloth module matches v 2.0.18. v 2.0.26 adds a read-only output-owner
tracer; its runtime owner classification remains pending. Full-rate animation
and controller behavior remain native. Front-coat flicker and hand penetration
during hands-in-pockets remain reproducible; general improvement is not a claim
that the coat is universally fixed.

Every matching submission enters native adapter `0x00C16ED0`. A source-record
QPC phase clock permits at most one major physical solve per 60 Hz period at
16.666668 ms; missed whole periods are discarded while fractional phase is
retained, so there is no catch-up burst or manufactured step below 60 Hz input.
Force filtering advances only on majors (alpha 0.125) through a private aligned
source-value copy. Shared context timestep writes are serialized and restored
bit-for-bit after the synchronous call. Serialization can reduce parallelism;
no throughput or frame-time saving is established.

A gate accepts the nested solver only on the current thread and exact expected
arguments 2-5. Major mode invokes original solver `0x00C16BD0`; replay mode calls
publisher `0x00C168E0` with the **actual solver arguments 1 and 3**, without physical
integration. Wrong thread, mismatched tuple, invalid memory or unavailable proof
runs the complete native solver. Parser, wrapper, adapter and solver hooks share
one optional rollback transaction; the publisher is validated but not detoured.
The solver argument 1 is a fresh adapter-local 0x90-byte object, not adapter
argument 1. No native pointer substitution or direct replay from the adapter hook
is equivalent to this call contract.

The classifier requires a live three-name coat resource and a type 0/CLOTH,
130-node source. This is bounded experimental classification: an exclusive
resource-pointer-to-solver-source association remains unproved. CHAIN=1 and
JIGGLE=2 are different object types. Replayed transforms come from fresh,
non-integrated solver input, so “output replay” does **not** certify a coherent
hold of the last completed physical pose.

# Model identity and independent parser profiles

The vanilla torso and the inspected 60-FPS torso mod have identical mesh payload,
topology and identifier inventories: 130 `PL_Coat_SMUNode_*` and 16 `*_SMUJiggle`
names. Differences are compiled GEOM/XBG metadata. Classification requires all
three names inside a validated input: `PL_Coat_SMUNode_130`,
`Ph_Jig_Zipper_Base_SMUJiggle`, and `Ph_JiggleStiff_Right_Poket_Out_SMUJiggle`.
The authoritative vanilla input is 1,229,516 bytes, SHA256
`EA3EF04124984D78CB0AECC315948F03150D5CB3BEC398848C7B29F9CFE8CF0A`, resource
ID`0x372232BF`; identifier offsets are`0x6804/0x59C4/0x6CC4`, parsed counts 4/4.

The parser proof requires the 22-byte whole-instruction prologue and `MOEG`/
numeric`GEOM` comparison at+0x4C, uniquely present in each usable image.

| Profile | Parser RVA | Evidence boundary |
| --- | --- | --- |
| Global/04DF | `0x0036F880` | Preserved mapped-image uniqueness and live torso-load proof |
| VMPless | `0x00927340` | Independent unpacked signed-image proof |
| Complete Edition | `0x01D6E800` | Independent unpacked signed-image proof |
| Asia/Miru | `0x00942210` | Independent mapped-image proof |
| Shev/A4EE | Inactive | Packed input has no proven parser; no equivalent mapped image |

These addresses are profile data, not one relocation formula. Intermediate
wrapper/adapter/solver research is Global-only. `SHADOW_ENGINE_CLOTH_DIAGNOSTIC`
separates the experimental module from production. Missing, ambiguous or failed
cloth proof leaves ordinary shadow behavior unchanged. Bounded copied diagnostics
flush only on F9/shutdown; they never establish live ownership by themselves.

# Recovered Global resource and solver roles

All addresses in this section are Global RVAs. Static roles are distinct from
the runtime observations below.

| Boundary | Recovered role and ownership limit |
| --- | --- |
| `0x00145DE0`, return`0x00145DF6` | Resource wrapper dispatches virtual parse+0x100, then+0x40 and conditional+0xF0. Upstream`0x0015DF70/0x00162720` perform resource lookup/allocation, references, publication/queueing and finalization. |
| `0x02E797D0` | Live `CGeometryResource` vtable; wrapper caller`0x001627B4`. Finalization flags change 0x08→0x0C without changed sampled reference fields. |
| resource+0x78, vtable`0x03209048` | Allocated0xB0-byte authored secondary-motion definition: measurements, connectors, poses, ball/double-ball joints, IDs/names and joint-to-bone mappings. Reflection/init/cleanup references do not identify the 130-node live solver. |
| `0x00440CB0` | Generic tagged-handle unwrap returns referenced pointer with low tag bit cleared; coat matches proved construction-only. |
| `0x00439F40`, `0x00436580` | Geometry-instance initialization and creator readiness/dependency check. Genuine component caller`0x007CA83D`, primary ID6269, runtime record ID3207. |
| `0x007CA330` | Groups model-part descriptors, allocates 0x40-byte geometry instance, attaches it through a group to a higher owner. Descriptor+0x188→handle owner+0x10→non-null coat resource. Fifth argument is only a byte: captured0x77BBEA01 means mode 1, not a 32-bit mode; only 0/1 observed. Descriptor first word0x3F800000 is a float, not a vtable. |
| `0x007CACA0` | One-argument owner rebuild; owner vtable`0x02F17D30`, caller`0x007CC79B`. Bounded scan of 256 descriptors and eight snapshots. |
| `0x007CC010`, `0x007D0070`, `0x00794EF0` | Transform/group-state path, registered recurrent owner callback, and existing-group synchronization. No explicit delta argument; broad owner callback is not a suppressible cloth-solver boundary. |
| `0x00C171F0`→`0x00C16ED0`→`0x00C16BD0` | `CSecondaryMotionComponent` / `SecondaryMotionUpdate` / `CSecondaryMotionUpdateJob` dispatch, per-instance adapter and exclusive synchronous solver. Adapter argument 4 advances through persistent 0x170-byte source records; argument 2 is a worker-stack local. |
| `0x00B6E1F0` | Complete 0x170-byte parameter value-copy path. Adapter copies source before solving; private source acceleration copy is distinct from replacing solver context. |
| solver state+0x38/+0x98 | Object type and simulated-node count. Context+0x130 is physical dt. |
| `0x00C13F10` | Integration uses acceleration×dt² + previous position + velocity×dt×damping; later solver velocity recovery uses 1/dt. Source first float 4 supplies acceleration. |
| `0x00B69FA0`→`0x00C15EA0`→`0x00C168E0` | Type 0 pose finalization, animation/physics blending and output publication. Publisher copies 0x20-byte transform pairs, updates dependent indexed slots and dirty state, and does not integrate or consume dt. |
| Publisher argument 2 |0x38-byte output-owner wrapper: descriptor+0x00, transform-output base+0x20, dirty-state base+0x30; seven pointer fields. Wrapper equality is not yet proof of stable backing ownership. |

# Loader and ownership observations

| Experiment | Recorded observation and resulting limit |
| --- | --- |
| Dormant SSM readers | All three generated `SSMSimulationParametersDesc` readers had zero calls during the v 1.1.4 coat session; dormant serialization is not live solver evidence. |
| Initial parser probe | At most 32 post-return snapshots; 5,384 validated GEOM calls and two three-name matches, no drops, same thread 22180/caller0x00145DF6. Proves live torso loading. |
| Resource lifecycle (.2) |33 vtable slots and fields+08/+28/+34/+40 before/after parse and wrapper return; 5,211 parses, 64,297 wrappers, two coats/two returns, no drops. Proves concrete resource ownership, not physical cadence. |
| Definition (.3) | Both coat variants have two ball joints, five bone IDs/names and two mappings; six other collections empty. Small authored layer, not full 130-node ownership. |
| Unwrap (.4) | Three exact vanilla unwraps on loading thread: two initializer and one creator readiness call; none recurrent during movement. |
| Instance/group probes (.5–.7) | One genuine component and exact descriptor→resource→group→component chain; later call reused group. Null tracked-slot comparison was a diagnostic false positive, so non-null resource is mandatory. Class/rebuild caller recovered; no solver cadence established. |
| Owner cadence (.8) |21,273 callbacks over 93.8632167 s =226.6276Hz on one thread. Early cumulative F9 did not reset the final capture. Recurrent owner callback, not a dt-bearing solver proof. |

# Rejected physical and presentation experiments

The version numbers below belong to the cloth research line and must not be
confused with the active shadow-engine versions.

| Experiment | Mechanism and recorded result | Durable conclusion |
| --- | --- | --- |
| .9 broad owner60Hz |17,031 calls/86.9297481 s; 5,208 original and 11,823 suppressed, 195.9053Hz→59.9104Hz, 69.4205% suppressed. Character stutter/ghosting; coat still too fast. | Restore every owner callback; another frequency cannot repair the wrong boundary. |
| .10 shared-context wall dt |19,562 matches/19,558 corrections; incoming 0.033333335 s. Speed improved, but clipping/sticking and little motion. One context shared by≥4 solver-state/instance pairs across workers; applied 1.3–24.4 ms. | Shared-context timing mixes simulations. Retain physical dt finding, reject its clock. |
| .11 private solver context/state clock |256 clocks, copied 0x170-byte context with only+0x130 changed. Two pre-completion crashes:0xC0000005 at0x00C14A3D in0x00C149F0, `MULPS XMM1,[RDX+0x80]`; RDX was substituted solver argument 2. | Reject pointer substitution and worker-stack clock identity. Exact memory/alignment cause is not established by the available crash description; do not claim alignment-only repair. |
| .12 source-only wall clock |Native pointers preserved; serialized context write/restoration, unique 27-byte detour prefix plus 31-byte source-copy suffix.2,040 matches/2,038 corrections, one source,≥3 apparent instances, 1.7–24.9 ms instead of 33.333 ms; floaty/collapsed panels. | Source is stable but shared; raw interleaved elapsed-time stream fails. Later static recovery shows the apparent instances were worker-stack identities. |
| .13 apparent-instance raw dt |19,654 matches, five apparent clocks, 18,146 corrections/1,508 fallback.3.0/3.1 ms then 75.8 ms gap→native 33.333 ms; umbrella lift and less smooth motion. | Raw scheduling gaps plus discontinuous native fallback fail; no player-state multiplier was read. |
| .14 smoothed dt/force |Seed 8.333 ms, clamp 1–16.667 ms, slew≤1 ms/call after lock acquisition; acceleration alpha 0.125 in private source.15,828 corrected calls/five apparent clocks. Better clipping, but too fast/bouncy and120FPS better than240FPS. | Changing dt each submission does not control integration or force-filter frequency. |
| .15 whole-adapter fixed60Hz |25,229 submissions =17,642 fixed 16.666668 ms executions +7,587 skips; zero misses/fallback. Smoother and less clipping, but rapid movement/rest flicker. | Fixed accounting works; skipping adapter or its only solver suppresses required output. |
| .16 microstep physical budget |All 16,616 calls corrected: 12,014 majors/4,602 one-ms presentation integrations, five apparent clocks; no saturation/miss/fallback. Extreme jumping/clipping. | Splitting a physical period among integrations is not solver-equivalent. |
| .17 direct output replay |Stable source clock retained, but publisher received adapter 1/3 instead of solver 1/3. Immediate reported crash; no dump/fault instruction available. | Invalid call contract is confirmed statically, not a fault-stack attribution. Enter native adapter and intercept its actual solver tuple. |
| .18 nested replay |24,650 exact calls =8,398 majors +16,252 output-only replays; one source, zero gate mismatch/miss/fallback. Reported approximately 99% stable, residual pocket clipping/flicker. | Accepted narrow mechanism; replay publishes current non-integrated tuple, not necessarily last solved pose. |
| .20/.22 shared-output cache |Four sources×512 transforms, captures completed shared/dependent ranges; publisher runs then prior transforms restored. First valid cloth-only .22 runtime had erratic pose resets. | Reject post-publication shared-output rewrites. |
| .23 rollback baseline |Cache/state/restore paths removed; cloth source exactly .18; movement excluded.8,748 submissions =4,365 majors+4,383 replays; one source, zero misses/mismatches/publisher failures/fallback. General movement/vaulting substantially better; pocket defect retained. | Accepted experimental Global continuation, not universal visual correctness. |
| .24 complete output tail |28,324 exact matches =8,438 solves+19,886 pose-finalize/blend/publish replays; one source, zero failures. Pocket phasing unchanged. | Missing tail stages were not the cause; full tail still receives fresh non-integrated input. |
| .25 solved tuple substitution |Caches 0x20 bytes from each 130×0x40-byte local node, substitutes before publisher and restores local tuple afterward.10,153 replays: 2,438 successful/7,715 precondition failures→native 33.333 ms; 11,463 fixed majors,≥19,178 solves/21,616 submissions. Pocket defect plus worse jumping. | Mixed fixed/replay/native cadence invalidates the test. Same-shared-state-pointer condition is a leading unproved failure cause; reason-specific failure and ownership proof needed. |
| .26 output-owner tracer |Returns .23 policy, removes all .25 tuple/cache writes. At most 64 exact source/wrapper/seven-pointer identities plus solver provenance/major-replay counters; wrapper-only and backing changes distinguished. No movement hook/telemetry. | Read-only ownership investigation; runtime result pending. |

A public .18 result video records visible fixed-rate simulation/replay, while
preserved native logs establish activation and accounting. No screenshot/GIF or
missing marker overrides the actual tester's report.

# Remaining proof and validation limits

The live timestep consumer is proven; exclusive resource-to-source linkage,
replay-output lifetime, dependent/dirty ownership during animation transitions,
and safe coherent held-pose publication remain incomplete. Do not infer a PhysX
or global-Havok origin from names. Civilian `ClothMaxModulo`,
`WIND_ANIMATION_SCALE`, Havok packfile/world-step paths and WD2 player hooks are
not coat-solver evidence. The v 1.1.5 probe was never runtime validated.

Intermediate research uses Global-only runtime gates with exact preflight,
transaction rollback, bounded state, unchanged unrelated shadow behavior and
manual visual classification. Final integrated release candidates require
independent affected-profile/all-profile mapping and runtime validation; A4EE
cannot be guessed. The movement and external dt-clamp investigations retain
their separate [controller](player-movement-high-fps-investigation.md) and
[comparison](wd-dtclamp-comparison.md) limits.
