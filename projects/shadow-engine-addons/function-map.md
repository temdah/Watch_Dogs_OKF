---
type: Function Map
title: Shadow Engine Addons Function Map
description: Navigation to focused confirmed engine-function and serialized-data mappings relevant
  to Addons.
tags:
- shadow-engine-addons
- functions
- reverse-engineering
status: stable
sources:
- resource: custom-lightning-asset.md
  title: 'Authoring XBG lightning assets: formats, resource joins and spawn failures'
- resource: manual-lightning-bolt.md
  title: Internal Recorded Lightning Bolt
- id: local-pcss-implementation
  resource: local-light-pcss.md
  title: Perspective Local-Light PCSS
- id: public-storm-promotion
  resource: public-storm-runtime.md
  title: Separating a storm hook host from optional observers
- id: v227-first-entry-rear
  resource: ../../evidence/catalog.json#E-607303853326
  title: First-entry native storm loading and repaired rear specular references
- id: collector-live
  resource: ../../evidence/catalog.json#E-917b18ede199
  title: Audible thunder after same-process resource collection
- id: v226-runtime
  resource: ../../evidence/catalog.json#E-db426a3dbb71
  title: Seven resource failures with installed but unobserved collection hook
- id: retail-loading
  resource: storm-audio-loading.md
  title: Retail Storm Audio Dependency Loading
- id: live-missing-resource
  resource: ../../evidence/catalog.json#E-7934fc497f4f
  title: Live absent thunder event and related resources with positive controls
- id: v225-runtime
  resource: ../../evidence/catalog.json#E-73749200be0f
  title: Fifteen matched resource-resolution failures and inaudible thunder
- id: v225-candidate
  resource: ../../evidence/catalog.json#E-7eb2f33e9233
  title: Native command-result observer and retained package audit
- id: v224-candidate
  resource: ../../evidence/catalog.json#E-2cb595ca312e
  title: Scoped native thunder trace and retained profile validation
- id: v223-stage
  resource: ../../evidence/catalog.json#E-1a8bb05ece30
  title: Native-update thunder candidate and retained payload verification
- id: storm-audio
  resource: storm-thunder-audio.md
  title: Storm Thunder Audio Submission
- id: frame-attribution
  resource: lua-frame-attribution.md
  title: Addons Lua Frame Defect Attribution
- id: world-loader-probe
  resource: world-loader-probe.md
  title: World Batch Loader Timing Probe
- id: entity-script-lights
  resource: world-entity-script-lights.md
  title: World Entity Lights and Mission Activation
- id: additional-lights
  resource: additional-light-sources.md
  title: Additional Non-Batched Game Light Sources
- id: atmosphere-probe
  resource: atmosphere-probe.md
  title: Bounded Atmosphere Snapshot Probe
- id: world-light-batches
  resource: world-light-shadow-batches.md
  title: Compiled World-Light Shadows and Decoded Locations
- id: muzzle-lights
  resource: muzzle-flash-shadows.md
  title: Muzzle-Flash Dynamic Shadows
- id: basic-lightning
  resource: basic-lightning.md
  title: Basic Storm Lightning and Moon-Shadow Separation
- id: sun-alignment
  resource: sun-flare-alignment.md
  title: 'HDRI sun and native flare: selection mappings and unresolved projection'
- id: limiter-control
  resource: headlight-limiter-control.md
  title: Vehicle Headlight Shadow Limiter NexusTools Control
- id: diagnostic-tools
  resource: diagnostic-tools.md
  title: NexusTools menu coexistence and diagnostic attribution experiments
---

# Scope

This map links native Watch Dogs 1 functions, serialized fields and mod-owned
observers to their evidence and limits. RVAs are specific to the build identified
by each concept. Mod hooks and exported controls are not native engine APIs.

The [storm host case study](public-storm-runtime.md) separates the runtime-tested
mechanism from later offline-tested packaging. [Graphics activation and streaming](graphics-activation-and-streaming.md)
distinguishes entity placement, completed component identity, render groups and
loading demand; [spawn-registry failure](custom-lightning-asset.md) is an earlier
boundary that can prevent graphics creation entirely.

# Mapped boundaries

* [Environment collection registration](storm-audio-loading.md): constructor
  A5EFD0, base registration15D7A0, thunk148FA0 and native callback registry3B593A8.
  Live26 confirms correct registered owner, owned slot and enabled hook. A
  same-process save reload changes counter0->1, loads all four storm roots and
  makes thunder audible according to runtime feedback. First-entry initialization was the remaining fix at v2.1.26;
  exact initial chronology is not measured. See focused ownership/inspection gates.

* [Legacy sound-loading comparison](storm-audio-loading.md):1.0.7 initialization
  VA10001CD7 and settings scan10001B15 supply scheduler state/settings, without
  established audio loading. Supplied1.0.34 is a byte-matched later bolt build.
  See the focused concept for legacy identity, consumers and evidence limits.

* [Retail storm resource loading](storm-audio-loading.md): environment callback9FC8E0,
  slot2F5FA90, helper275DC0 and native collector ownership. Moon selection skips
  storm dependencies;26 contributes the private Storm A IDs through the same helper.
  Typed CSoundResource acquisition294D00, manager3B593C0 and load/unload boundaries
  are mapped with Global identity, evidence and safety limits in that concept.

* [Live sound-resource identity](storm-sound-execution.md): manager global3C0D030,
  256 low-ID-byte buckets with16-byte entries; read-only live snapshots identify
  thunder1B2CA and related1B2C8 as absent, with resident controls. Native lookup
  allocates/acquires references; no native calls used. Type2 executor236F700 can
  also propagate a missing-child error. No inspected TFoWC2 FAT overrides these
  files; retail collection ownership is mapped in the loading concept.

* Runtime25 now confirms15 matching thunder command results8000E002. See
  [execution/resource resolution](storm-sound-execution.md): resource rejection
  is established; live root absence and the missing collection phase are now mapped above.

* [Sound execution/resource resolution](storm-sound-execution.md): Global command
  slot31D7B18 ->232A010 returns the status from23CA920;236E4A0 can reject
  missing resources or incorrect resource types after early handle allocation.
  Lookup23D1C90 allocates nodes and its caller acquires references, so neither
  is a read-only probe. .25 captures64 copied native results across asynchronous
  execution and joins event/handle; no audio policy or resource ownership change.

* [Storm thunder audio](storm-thunder-audio.md): Global2B7DC0 borrows the native
  sound singleton; vtable+100 ->2BBFE0/2BB480 returns an event handle after native
  readiness checks and23BE190 SND_SendSoundEvent dispatch. Pulse helper9F5D80
  ignores that handle, so handled is not successful audio proof. Fresh installed
  TFoWC2 Storm A/B match retail completely; .22 and .23 thunder remain inaudible.
  Readiness2BC560 requires both native-owned self+14/+17 bytes nonzero; flag
  meanings remain unknown; .24 samples both as1. No forced readiness writes.
  Internal .24 guards slot2E70940 and forwards the verified six-argument ABI
  exactly once. TLS limits observations to private scheduler calls; copied pulse
  deadlines, readiness and returned handles distinguish acceptance from audibility.
  Foreign sounds remain unobserved; callback lifetime is process-resident.
  .24 runtime observes13 accepted1B2CA requests with readiness1/1 and on-time
  pulse progression; Runtime feedback reports no audible thunder. Investigation moves
  downstream; execution/resource checks are now mapped in the concept above,
  while live voice/mixer outcomes remain unresolved.

* [Lua frame attribution](lua-frame-attribution.md): Global1C7CC2 is a downstream
  table lookup, not an Addons owner marker. Historical Addons events match the
  reference runtime timestamp but lack frame/GC/victim memory. Source screening
  and retained public-reporter prototypes identify no Addons frame mismatch;
  Trainer's reference mismatch is confirmed. Shared mechanism remains plausible,
  not established for historical Addons sessions. Earlier callback/category
  attribution statements are hypotheses, not proven causes or removal guidance.

* [Public problematic-light reporter](diagnostic-tools.md): Global projectile
  tracer entry at RVA `0x00B59760`, guarded by its exact 19-byte entry signature.
  The production detour forwards every call and copies one start/end pair only
  after the user arms it. The endpoint is a projectile trace coordinate carrier,
  not proof of a native light-object hit; the placement map performs later
  offline identification. Module state lives for the process and the public Lua
  owns only one menu action, with no Script or lifecycle callback.

* [Basic storm restoration](basic-lightning.md): v2.1.23 private scheduler/output,
  vector retirement, native curve-coordinate dataflow, clean resolved rain-slot
  reads and frame-scoped RGB contribution. Global native audio helper9F5D80
  consumes private pulse/clock and copied strike/thunder IDs, submits through
  the native audio interface and marks private handled state. Scheduler audio
  inherits environment+4A8. No Moon writes or spatial transform; Global identity
  plus12 exact byte gates. Offline isolation/audio arguments pass; live acceptance was pending at this stage. v2.1.23 later remained inaudible;
  v2.1.27 became audible after the loading repair. A2F7E0 now forwards the original update then
  schedules privately; A15180 only consumes copied results. A6080B/A6081D prove
  native lightning-before-sky order and matching delta. No shared Moon scalar writes.

* [World loader probe](world-loader-probe.md): exact Global load-vtable slot,
  processor/stream boundary and cursor observation; aligned pointer publication,
  bounded copied samples and process-lifetime forwarding. Experimental native
  diagnostic integrated in the v2.1.2 Addons ASI/menu; no caster/fade mutation
  or complete load coverage. Global runtime confirms1,696 completed loads,
  including341 after checkpoints; renderer publication remains unverified.
  v2.1.3 corrects ordinals and adds bounded post-call consumed-interval copies
  for offline exact content matching. Matches remain content identity, not live
  ownership/publication or underground clearance. Host owns worker/stop state;
  Lua owns checkpoint
  request count. The former standalone companion is superseded.

* [World entity and mission lights](world-entity-script-lights.md): shared FCB
  component ownership, 78 explicit shadow-off entity IDs, Bean sculpture/Owl
  Motel/stadium examples, and exact mission-target joins. Maps Domino activation
  contracts, not native caster setters; inheritance and runtime admission remain
  unresolved.

* [Additional game light sources](additional-light-sources.md): actual
  common/patch prefab shadow controls, current Addons differences and
  absent-field capsule exceptions. Static data only; entity callers,
  attachments, scripting API and final shadow admission remain unresolved.

* [Atmosphere snapshot](atmosphere-probe.md): exact loaded-library/key table,
  native 32-byte curve knots, selected cloud triples and observer ownership.
  Captured-image static evidence only; bounded tests are not runtime proof.

* [Compiled world-light batches](world-light-shadow-batches.md): includes a
  community later-setter lead (`RCX+0x20` resolver, Boolean store at result+0xD).
  It is not mapped to the saved Global image/type/callers and cannot be used as
  a blanket detour. The confirmed mapping remains the dynamic-light batch type identity, processor loader, shared-definition deserializer, and
  reflection-confirmed `bCastShadow` byte; named Omni/Spot/Capsule enums,
  variable-key instance serializer, position/orientation updater and WLU
  `ExportPath` ownership. All 49,592 stored instances have positions and owning
  resource links; base-corpus type-count validation also identifies 496
  additional disabled instances in 29 omitted files. Includes exact captured-image identity, inputs/outputs,
  ownership, evidence level, consumers, incomplete fixture identity and limits.
  The unified v2.1.4 build applies the mapped field to the 12,788 audited
  definitions only after verifying all retail hashes and exact mutation bytes.
  Its anomaly marker uses the existing Global `AddTrace` endpoint carrier under
  separate arm state; returned endpoints are resolved offline to this placement
  inventory. This maps a diagnostic coordinate carrier, not a native light-
  object setter. Database exclusions remain definition-wide.

* [Internal recorded lightning bolt](manual-lightning-bolt.md): existing Global
  B59760 carrier ABI, captured owner/resource reuse, endpoint selection and native
  segment emission. Source-level 8B3CD0 copy/owner+18 retention is recorded with
  unverified release, scene lifetime and execution-thread limits. Current 16-segment
  main chain omits generated branches; appearance and scene-lifetime acceptance remain incomplete.

* [Custom lightning mesh](custom-lightning-asset.md): offline GEOM97.50 geometry
  export; all2,414 non-null authored fileModel IDs resolve by archive path hash.
  Also owns live relocated entity-transform evidence, the nearby/distant preview
  comparison and internal weather-observer activation policy. These add no engine
  RVA and establish neither GPU visibility nor per-strike light/audio synchronization.
  The same concept owns the isolated full-sky-mesh distance/hold control and its
  separation from normal animated event lifetime.
  Its Global static map distinguishes identity-initialized graphics cache
  (`7E13B0`), entity-to-cache update (`7D0070`), renderer publication (`794EF0`)
    and size-cull flag forwarding (`78C450`/`409990`). None is a diagnosed bolt
    rejection condition or an authorized global renderer patch.
    Global header parser `34E7B0`, single-LOD selector `2C9CC0` and rejection
    path `2F0AF5..2F0C70` distinguish authored cutoffs from effective visibility.
    The bounded internal observer uses existing-reference lookup `18B620` and
    copied producer/published registry views; no GPU draw or root cause is proved.
    Factory registration `7E6D2E` → `81F320` replaces construction table `2F13200`
    with completed table `2F17D30`; the original observer rejected all561 samples
    by matching the construction table. The corrected gate follows factory output.
    The matched corrected run finds534 final pre-activation graphics states, ten
    renderer successes and one unavailable entity. Entity activation `856AC0`
    sets bit2 and dispatches component `+30` → `7D0050` → `7CBD80`; resource
    completion `7CBF70` gates activation on bit2 via `8236A0`. Upstream activation
    policy is mapped in the subsequent trace; these samples do not prove GPU draws.
    The subsequent loading trace maps serialization `85EE10`, category getter
    `8237B0`/setter `77B740`, provider selection `69EB40`/`6DB2C0`, World/Near
    construction `6E6AF0`, world-rectangle query `6AF700`/`6F0430`, retained
    loading demand `6DBB50` and readiness dispatch `6DB8C0`. The scoped sky
    prototype correction selects World0 instead of inherited Near2; live
    activation and visual acceptance of that correction remain pending.
    The later Nexus image maps registration `11E920` to spawn `11BB00`, decimal
    parsing `11C3F0` and UID lookup `11C4B0`. Its matched capture enumerates all
    fifteen sky definitions but fails both spawn lookups before engine creation.
    The integer/`%f` error mismatch makes printed zero unreliable; exact registry
    failure and manager-update causality remain unresolved. See the owning concept.
  Dedicated Unlit/white-texture resource chain and appended prototype retain the
  original library bytes. Spawn API1160C0/UID lookup116A70 establish the explicit
  decimal-string argument on the inspected module; no new native hooks. Manual
  show/remove is offline-tested. Corrected repeated spawning is human-confirmed;
  comprehensive occlusion/retirement remain unaccepted. The owning concept records the
  four-byte exporter bounds error,64-unit cutoffs and header-only correction,
  plus Arm-first recording and same-instance replay extension. The brief preview
  uses bounded spawn/remove pulses and geometric cap taper, with explicit
  clock-gap/cleanup ownership. Runtime pulses are visible but transitions quantize
  near0.5 seconds; duration/rhythm are not accepted. See the owning concept for
  the host-cadence gate before animation. The elevated preview now uses the verified
  host NextTick queue, absolute deadlines, three staged variants and independent
  aimed/random ownership; distant rendering and timing await runtime acceptance.

This map is incremental and does not claim to enumerate every Addons subsystem.

* [Muzzle-flash lighting](muzzle-flash-shadows.md): weapon front/face/impact
  configuration registration and particle illumination Boolean readers.
  Native muzzle-light creation, shadow admission and lifetime remain unmapped.

* [Basic lightning and moon shadows](basic-lightning.md): single-selector
  ownership, native state/scalar path, typed keyed resolver and its unverified
  fallback/lifetime. Includes the rejected selector swap and crash-unsafe scan.
* [Sun/flare alignment](sun-flare-alignment.md): CPU record/time/weather/recipe
  selection and publication; the cloud-key wrapper is a mutating setter path,
  not a passive getter. Final projection and flare-direction consumer remain open.
* [Vehicle headlight limiter control](headlight-limiter-control.md): stable
  version-1 cross-mod ABI exported by Shadow Engine v2.0.35, with Addons-owned
  lazy module/export discovery and getter/setter confirmation contract. The
  v2.1.5/v2.1.6 Addons carrier is runtime-rejected: three identical Global
  faults at `Disrupt+0x001C7CC2`, now statically mapped to embedded Lua
  hash-table node lookup. Logs prove no setter or world-batch call preceded the
  v2.1.6 failure. Exact Lua object lifetime/corruption remains unknown without
  a dump; do not ship or retest that carrier unchanged. v2.1.7 retains the ABI
  but replaced the Lua lifetime shape with a zero-upvalue NexusTools callback
  and existing-Script-owned lazy discovery/state/cleanup. Runtime produced the
  fourth identical fault, rejecting that correction as sufficient. Active
  source was restored to v2.1.4 at that rejection; no further Addons-side registration variant
  without a new ownership boundary or dump.

* [Vehicle light reference integrity](vehicle-light-reference-integrity.md): entity DynamicLights -> vehicle preset key -> specular dynamic prefab; seven mismatched identities initially repaired in internal staging and incorporated in public v2.2.0. Source510 rear/16 emergency versus saved effective474/14 references.
* [First-entry storm resource ownership](storm-audio-loading.md): Global15D7A0/15BAA0 embed and initialize Environment+8 container;146080/155140 forward/add native dependencies with demand and readiness propagation. v2.1.27 later received runtime confirmation; the separate public host has offline checks.

* [Established feature tests](established-feature-tests.md): numeric FCB entity IDs resolve against little-endian BinHex database keys, then lamp/preset-to-effect/prefab links. The independent baseline protects371 records and8029 resolved references; malformed or changed consumer chains block packaging.

[TFoWC2 shadow filtering](tfowc2-shadow-filtering.md) records the author-described facetted PCSS shader boundary, installed 1.1.0 shader-pack delivery, and unproved local-light coverage. The old zero-binding capture is not algorithm evidence.

[Perspective local-light PCSS](local-light-pcss.md) maps the original homogeneous
projection/visibility adapter, linear blocker-depth conversion, immutable PSO
interfaces, and NexusTools whole-archive redirection at IPE RVAs 1A7E82/1A7E99 and
1A8330–1A8481 for its pinned binary. It records exact ownership, source identities,
the unchanged TFoWC2 corpus and synthetic GPU evidence separately from game tests.

[Secondary streetlamp shadow exclusions](secondary-streetlamp-shadows.md) maps
the marker-to-shared-definition policy, sRGB/linear colour comparison, and exact
C58A3AB9 tag+0x21 caster byte used by the 80-definition Pequino secondary selection.
It records static attribution limits, all-instance ownership and unchanged-light
verification separately from the pending visual test.

Current internal30 policy: [secondary streetlamp shadow exclusions](secondary-streetlamp-shadows.md)
retains lower-lamp illumination while leaving 80 approved caster flags off across
426 matched placements. PCSS29 is retired after reported warnings and no
discernible visual improvement; its implementation remains archived.
