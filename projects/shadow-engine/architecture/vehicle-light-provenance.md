---
type: Diagnostic Contract
title: Vehicle Light Component to Renderer Provenance
description: Bounded F10 component and native transform tracing before any persistent ownership
  or quality policy.
tags:
- headlights
- ownership
- diagnostics
- native-abi
status: draft
sources:
- id: handle-proof
  resource: ../../../evidence/catalog.json#E-68e17e5f27d9
  title: Independent stationary descriptor-handle copy proof
- id: implementation
  resource: ../../../evidence/catalog.json#E-ad4735a0faf6
  title: Bounded observer implementation
- id: profiles
  resource: ../../../evidence/catalog.json#E-4d85852a0d8b
  title: Immutable regional update boundaries
- id: proof
  resource: ../../../evidence/catalog.json#E-376b4e3a3991
  title: Independent native byte contract
- id: harness
  resource: ../../../evidence/catalog.json#E-f4a82f305d4e
  title: Actual-source synthetic safety harness
- id: caller-test
  resource: ../../../evidence/catalog.json#E-f841f9dbcdda
  title: Copied caller and skeleton-header safety contract
- id: runtime-228
  resource: ../../../evidence/catalog.json#E-9599855e269d
  title: Global caller, class-table and multi-vehicle grouping result
- id: build-228
  resource: ../../../evidence/catalog.json#E-c54cee03f224
  title: v2.0.28 caller and skeleton-header diagnostic result
- id: native-228
  resource: ../../../evidence/catalog.json#E-0f3ac5db7917
  title: Read-only Global dynamic-light callback decompilation
- id: runtime-227
  resource: ../../../evidence/catalog.json#E-3680dbce43c6
  title: Global multi-vehicle continuity and observational disappearance result
- id: build-227
  resource: ../../../evidence/catalog.json#E-8ccfb1e32173
  title: v2.0.27 copied-token capture-lineage candidate and validation
- id: runtime-219
  resource: ../../../evidence/catalog.json#E-252f363b9811
  title: Global focused-window headlight, siren and shared world-control result
- id: build-219
  resource: ../../../evidence/catalog.json#E-16e86035dd88
  title: v2.0.19 focused sampling candidate and validation
- id: runtime-218-six
  resource: ../../../evidence/catalog.json#E-0c462a017fa3
  title: Six-state Global capture, shared world descriptor and sampler saturation
- id: runtime-218
  resource: ../../../evidence/catalog.json#E-8efa60da1446
  title: Global stationary headlight and siren descriptor matches
- id: link-build
  resource: ../../../evidence/catalog.json#E-950b5a825236
  title: v2.0.18 stationary handle-link candidate and validation
- id: link-callers
  resource: ../../../evidence/catalog.json#E-9bcee2b273c8
  title: Native component array, spotlight predicate and handle consumers
- id: link-fields
  resource: ../../../evidence/catalog.json#E-11607dba1c85
  title: Native spatial descriptor consumer, constructor and copy semantics
- id: runtime-217
  resource: ../../../evidence/catalog.json#E-91c813e0450c
  title: First Global observer activation and missing renderer link
- id: preflight
  resource: ../../../evidence/catalog.json#E-32bc1b6e617a
  title: Knowledge lookup and rejected assumptions
- id: boundaries
  resource: ../../../evidence/catalog.json#E-3792a0e63251
  title: Global update and transform native consumers
- id: construction
  resource: ../../../evidence/catalog.json#E-e51229fc7eb5
  title: Native light construction and transform wrapper
- id: creation
  resource: ../../../evidence/catalog.json#E-f94e6a665100
  title: Light handle allocation and initialization
- id: resolution
  resource: ../../../evidence/catalog.json#E-2ad94f5f962a
  title: Mutating handle lookup and handle teardown
- id: build
  resource: ../../../evidence/catalog.json#E-2d337a97d37a
  title: Candidate build and validation evidence
---

# Role and evidence boundary

This concept owns the copied component/renderer provenance diagnostic and its
native mappings. Later [vehicle-owner correlation](vehicle-owner-lifetime.md)
and [generation-aware selection](vehicle-shadow-selection.md) build on it.
The historical v 2.0.17–.28 experiments below are evidence, not current build
instructions. Renderer type, descriptor pointer or skeleton equality alone is
not vehicle identity; no retained native pointer is dereferenced by the worker.

# Native boundaries

Old Global decompiler image base is `0x7FFC39BF0000`. Addresses below are RVAs.

| Profile | Shared vehicle-light update | Transform wrapper | Light/spatial transform writer |
| --- | --- | --- | --- |
| Global / supported-04DF | 0x00BA7570 | 0x007AA0A0 | 0x0079E0B0 |
| VMPless | 0x0078E1A0 | 0x002C0790 | 0x002B47A0 |
| Complete | 0x01BB5420 | 0x01725800 | 0x01719810 |
| Asia | 0x0077E560 | 0x001FA1B0 | 0x001F6FB0 |

These four chains were independently recovered and checked on actual preserved
images. They are not cluster-delta guesses. A4EE has no proven update RVA;
its optional observer is disabled, not mapped by similarity.[^corpus]

The update ABI is `void(component, skeleton, worldTransform, float delta,
unsigned char forceUpdate)`. The fourth argument is **XMM3**, not integer R9;
the native `movaps xmm1,xmm3` feeds virtual +0x40. The fifth is a stack byte.
The shared function is the +0x30 virtual update used by vehicle dynamic lights
and headlights. Static Global class-table leads are CVehicleDynamicLight
vtable `0x02F46E40` and CVehicleHeadLights `0x02F8A070`; no vtable classifier is
installed. Component +0 is vtable, +8 is a settings/config pointer, +0x10 is
the native light pointer, +0x11C is the skeleton bone index (`-1` bypasses bone
transform). Native +0x30/+0x31/+0x32 gates can suppress updates. Skeleton is a graphics-interface grouping token, **not a CVehicle base or
generation**; the later native batch bridge is documented separately.
[^boundaries][^construction]

At update +0x12A native code loads component +0x10; its +0x133 call enters the
wrapper. That wrapper resolves light +0x20 through Global `0x02593920`, then
tail-calls the transform writer with `(light, spatialRecord, matrix)`. The
observer records the already-resolved argument of this existing native call;
it never invokes the resolver itself. The writer updates light transform and
spatial position/direction. Spatial +8/+0xC/+0x10 is position, including the
type-3 origin adjustment; +0x14/+0x18/+0x1C is normalized direction. The older
F10 `observedTuple` therefore must not be interpreted as world position.
Spatial +0 is the renderer's indexed-buffer indirection root, not a vehicle.
[^boundaries][^construction]

Native light +0x20/+0x28 are spatial/descriptor handle words; +0x38 is the
native enable byte. +0x39 stays an opaque secondary byte. Handle upper bits
are logged raw, not declared a reuse generation. Global `0x025BB1E0`, reached
by native handle resolution, can clear a dirty bit, increment/allocate/copy
buffer state and update slots: it is **not a read-only lookup**. Global
`0x02595720` tears down the two handle paths and writes invalid `-1` handles.
Native code retains allocation, release and light lifetime ownership.
[^resolution][^creation]

The previous Addons copy-constructor experiment at Global `0x009D64D0` with
destructor `0x00BCC390` produced zero live matches. Do not restore it or infer
constructor timing from zero matches. Its old +8/+0xC hidName/hidKey reading
conflicts with the pointer layout above. The preserved experiment is evidence of a failed observation route,
not proof that the constructor never runs.[^preflight]

# Observer mechanism and lifetime

Module 18 owns state in `ShadowEngineContext.vehicle_diagnostics`. Before any
deferred transaction writes, read-only preflight verifies six complete native
instruction spans, both rel 32 destinations and image bounds. Profile data owns
only the independently recovered update RVA. Missing proof disables just this
extension, preserving older F10. A valid installation journals the transform's
15-byte and update's 18-byte detours, with complete non-RIP-relative prologues.
Original trampolines publish before executable writes; observer enables only
after both installs. Full rollback restores bytes, frees allocations, clears
bindings and frees TLS. A failed byte restoration retains reachable resources;
the existing transaction does not promise stop-the-world atomicity.

F10 captures at most 256 component observations total, deduplicated by component
pointer per 500-ms epoch. It shares the existing nonwaiting writer token,
serial, freeze/rearm exclusion and worker. A stack-local TLS scope exists only
during the original synchronous update; nested updates mask the outer scope
even when deduplicated. The transform observer requires the same light pointer,
serial and bounded index. All original arguments pass unchanged, exactly once.
TLS publication/restoration failure disables observation. No lock waits,
continuous per-job logging, extra native resolver calls or GPU reads occur.

The worker reads copied data only; native pointers are opaque identities after
the synchronous call. Normal F10 stream completion/2.5-second partial timeout
is unchanged. Epoch 3 may be short; four owner observations per light are not
guaranteed. Contention, conditional updates, the cap and within-epoch pointer
reuse can omit evidence. No observation is a lifetime-safe admission decision.
Idle hooks still add pass-through detour overhead, but no TLS/memory queries.
[^implementation]


# Additional mapped callbacks and descriptor domain

Global native metadata associates update`0x00BA7570` with both
`CVehicleDynamicLight` and `CVehicleHeadLights`. Adjacent callbacks are headlight
destructor`0x00BFEEF0`, setup`0x00BDA380`, generic intensity`0x00B9FE20`, and
headlight-specific enable/intensity/cookie control`0x00BA0020`. Virtual+0x38 is
setup/resource-reference bookkeeping, not a per-frame position update. The
headlight destructor releases its extra resource before common teardown.

First-spotlight consumer`0x0104D9C0` walks array+0x148/count+0x150/stride 0x130,
uses type 3 predicate`0x00B9FFB0`, and reads a light's spatial handle through
`0x00B9FFF0`. Caller`0x00D27440` uses spatial position and descriptor cone data;
`0x0093C830` uses the same getter for attachment links. Generic dynamic-light
components therefore participate; absence of the dedicated headlight table
cannot exclude a rendered headlight.

The native spatial record is 0x58 bytes. Constructor`0x025989E0` initializes
+0x50 toUINT64_MAX; copy`0x025BB050` preserves that full 64-bit field; consumer
`0x025938D0` passes it to the descriptor lookup. Instance construction writes
the embedded light's descriptor handle there. This is the same domain as light
+0x28, and is read only from the already-borrowed renderer spatial record. The
bad-data thunk`0x025A0210` is not a callable proof.

| Profile | Spatial-copy proof RVA |
| --- | --- |
| Global | `0x025BB050` |
| VMPless | `0x00819E00` |
| Complete Edition | `0x01C631F0` |
| Asia/Miru | `0x007F12E0` |

Each proof independently checks a 24-byte register prefix and 56-byte no-call
tail at+0x9E, with complete image/readability bounds. Failure or A4EE disables
only the optional read. No new detour or native resolver invocation is needed.
Renderer samples copy `descriptorHandle/descriptorHandleValid` before native
rendering; `handleLinkEnabled` reports proof availability. Shared spatial
instances can use one handle; invalid/unreadable/UINT64_MAX is never a match.
Later allocation/reuse work proves the full generation domain, but cannot turn
a shared handle into a uniquely owned bulb without conflict checks.

Global capture of 113 update records found caller return`0x0093D8EA`, skeleton
table`0x02F13700` and dynamic-light table`0x02F46E40`. Callsite`0x0093D8E7` in
batch`0x0093D730` invokes component virtual+0x30 over array+0x148/count+0x150,
stride 0x130. The return address is copied before any helper; the skeleton first
word only after readability proof. The table is a common type interface; native
class/construction/update traversal, not subtraction from skeleton, proves the
CVehicle batch role. Its separate ABI is owned by the owner-lifetime concept.

# Focused windows, retries and copied lineage

The original 256-record total is divided into 64 slots for each of four renderer
samples. A completed sample opens 100 ms of matching-handle collection, capped
at 4096 native update opportunities. If optional handle proof is absent, broad
sampling retains separate quotas. Records are append-only until freeze; no
index eviction can redirect live TLS. The final sample receives its full window
before normal completion; 2.5 s partial timeout remains explicit.

Missing first-transform evidence can retry an existing record at most once per
16 ms within its 500 ms epoch. Each attempt rechecks the live light and both raw
handle words; changed identity skips, success stops retries. Initial tick/thread/
flags/delta describe the first observation, not a later transform. Same-value
reuse remains outside capture-local proof. Native forceUpdate and all arguments
remain unchanged; no forced movement or update is introduced.

The worker owns a bounded 256-record process-lifetime copied tuple registry keyed
by component/light/skeleton/full handle. F10 state excludes rearm during worker
updates; engine threads never wait. Tuples carry diagnostic lineage, capture
serial/sample mask/first-last counts. Changed component tuples, handles on other
tuples, simultaneous sharing and common skeletons are explicit leads. Absence
is only nonobservation, never destruction, despawn or native generation. Storage
overflow remains explicit and never changes rendering.

Markers retain `OWNER_BEGIN/RECORD/END`, `STAGE_VEHICLE_OWNER_WINDOW` coverage,
and `STAGE_VEHICLE_OWNER_LINK` componentMatches/rendererInstances. Valid bits 1/2/4
mean component/light/scoped-spatial copies. `transformSeen=0` is not hook failure;
overflow counts omitted opportunities, not unique lights or rejected shadows.
`ownerProven=0/persistentRegistry=0` are deliberate for the originating capture.
Current production registry semantics live in the selection contract.

# Controlled Global findings

| Capture | Recorded facts | Inference limit |
| --- | --- | --- |
| .17 three states |121 components, 18 transform identities, 45 renderer records, no transform matches; zero overflow/TLS/mismatch. Generic dynamic-light tables only; headlight-like pair and intermittent type 1 remain 4096. | Hooks activate, stationary conditional transforms do not establish ownership. Zero external jobs and no F9 are not stress validation. |
| .18 initial three captures |46 renderer records, 22 type 3/type 1 observations each uniquely matched; four components share skeleton, no transform observation.134 components,≤21 retry attempts, zero gaps; matching CPU4096 metadata. | Direct full-handle read closes stationary link; no independent world Spotlight 3 control, no lifetime proof. |
| .18 six wilderness/streetlight states |316 valid renderer records; target pair only on, siren pair only flashing; target 4096, some other type 3 at 512. World control has two persistent type 1 instances sharing one separate handle.256 owner records fill epoch 0 in 0–16 ms across 28–29 skeleton leads; no later records fit.28,640 resources/34,577 results balance, no failures. | Native quality variation is not distance-only policy; overflow is diagnostic starvation, not corruption. Later matches are not fresh same-epoch ownership. |
| .19 focused three streetlight captures |12/12 manager+renderer samples, 70 valid0xF records, windows 0/500/1000/1500 ms; active owners within 16 ms. Car off has none; headlights two type 3/4096; sirens add two type 1/4096 where flashing. One persistent type 1/4096 world handle has two instances and zero component matches. No quota/probe/unreadable/TLS/transform failure.58,720 native stores, zero external jobs. | Focused quotas solve sampled starvation without larger total; world fixture identity follows controlled observation, not spatial ownership proof. |
| .27 A/B transition |Three complete captures: A siren pair, then A headlights plus separate B four-light group, then B retained and A four tuples absentStreak1. All linked handles have one component/renderer instance; zero move/reuse/sharing/overflow/timeout/flush/probe/TLS failures. | Distinct copied groups and observational disappearance; no destructor or same-address generation proof. |
| .28 one/two police vehicles |Two complete four-window captures, continuing and new disjoint four-light groups plus separate two-light traffic group; 113 common caller/type records; zero overflow/TLS/reuse/sharing. | Supports grouping without traffic contamination; physical labels remain operator correlations. Native batch ownership requires the separate class/update proof. |

Actual-source fixture milestones covered 63/67/71/76/80 Python checks plus four
native harnesses as features progressed; all four mapped images passed their
applicable byte gates (71 per image for later observer builds). Tests covered
both detour write-failure rollbacks, scope nesting, full-versus-low handle
identity, focused quotas, later-window retention, shared instances, final grace,
time/probe bounds and copied-only flush. These are mechanism checks, not broad
visual acceptance or native allocation lifetime proof. A4EE stays unverified.
