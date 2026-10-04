---
type: Asset Pipeline
title: 'Authoring XBG lightning assets: formats, resource joins and spawn failures'
tags:
- shadow-engine-addons
- lightning
- blender
- xbg
- materials
status: draft
sources:
- resource: ../../evidence/catalog.json#E-addons-native-flash53-offline
  title: Five-image native pulse admission and endpoint-mask validation
- resource: ../../evidence/catalog.json#E-addons-storm-polish52-offline
  title: Staged geometry conversion and decoupled flash/cluster verification
- resource: ../../evidence/catalog.json#E-addons-storm-polish50-observation
  title: Automatic storm visibility and slow synchronized cluster observation
- resource: ../../evidence/catalog.json#E-addons-controller48-offline
  title: State ownership mitigation source controls and offline package gates
- resource: ../../evidence/catalog.json#E-addons-runtime47-controller
  title: Matched controller clock-comparison failures, cancellation loop and accepted weather reply
- resource: ../../evidence/catalog.json#E-addons-service47-offline
  title: Native host queue inspection and service-driver regression source controls
- resource: ../../evidence/catalog.json#E-addons-runtime45-native
  title: Internal .45 native runtime log
- resource: ../../evidence/catalog.json#E-addons-runtime45-host
  title: Matched .45 NexusTools runtime log
- resource: ../../evidence/catalog.json#E-addons-activity46-offline
  title: Bounded activity windows and concurrent flash/audio source and fixture controls
- resource: ../../evidence/catalog.json#E-addons-sky-runtime41-20261003
  title: Loaded bolt definitions followed by spawn UID lookup failure
- resource: ../../evidence/catalog.json#E-addons-sky-world41
  title: Native World/Near loading policy, scoped sky-prototype correction and package gates
- resource: ../../evidence/catalog.json#E-addons-sky-runtime40
  title: Matched runtime graphics activation failures and native lifecycle boundary
- resource: ../../evidence/catalog.json#E-addons-sky-component40
  title: Failed renderer capture and factory-derived component identity correction
- resource: ../../evidence/catalog.json#E-addons-sky-lod-observer39
  title: Native LOD selection, render rejection and automatic observation candidate
- resource: ../../evidence/catalog.json#E-addons-sky-native-20260913
  title: Global native graphics transform and size-cull boundary trace
- resource: https://github.com/Quiet-Joker/Dunia-Engine-XBG-Blender-Importer/tree/d64b396552aa2fe92f877945fab89cb67a3839a7/modules/Watch_Dogs
  title: Pinned upstream WD1 parser and geometry exporter
- resource: ../../evidence/catalog.json#E-addons-bolt-asset-20260908
  title: Actual Blender export and geometry validation
- resource: ../../evidence/catalog.json#E-addons-bolt-resources-20260908
  title: Complete non-null model-ID join against current entity data
- resource: ../../evidence/catalog.json#E-addons-bolt-tools-20260908
  title: Authoring and reproduction source identities
- resource: ../../evidence/catalog.json#E-addons-bolt-candidate31
  title: Internal manual mesh candidate and offline checks
- resource: ../../evidence/catalog.json#E-addons-bolt-payload31
  title: Appended prototype and dedicated resource chain
- resource: ../../evidence/catalog.json#E-addons-bolt-spawn-api
  title: Static spawn API argument and lookup contract
- resource: ../../evidence/catalog.json#E-addons-bolt-runtime31
  title: First manual mesh replay report and matched runtime calls
- resource: ../../evidence/catalog.json#E-addons-bolt-visibility32
  title: Retail-correlated native bounds and header-only correction
- resource: ../../evidence/catalog.json#E-addons-bolt-candidate32
  title: Corrected visibility and replay candidate checks
- resource: ../../evidence/catalog.json#E-addons-bolt-appearance32
  title: Human repeated-spawn confirmation and appearance captures
- resource: ../../evidence/catalog.json#E-addons-bolt-candidate33
  title: Brief pulse lifecycle and softened endpoint export validation
- resource: ../../evidence/catalog.json#E-addons-bolt-pulse-feedback33
  title: Runtime pulse cadence and human appearance feedback
- resource: ../../evidence/catalog.json#E-addons-sky-candidate34
  title: Elevated staged variants, host queue and complete candidate checks
- resource: ../../evidence/catalog.json#E-addons-sky-candidate35
  title: Continuous preview, decay and endpoint mask checks
- resource: ../../evidence/catalog.json#E-addons-sky-candidate36
  title: Placement and actual transform diagnostic checks
- resource: ../../evidence/catalog.json#E-addons-sky-direction36
  title: Runtime all-quadrant entity placement and unresolved visibility
- resource: ../../evidence/catalog.json#E-addons-sky-relocation36
  title: Player-area coverage limit, control distances and offline relocation checks
- resource: ../../evidence/catalog.json#E-addons-sky-candidate37
  title: Live relocation, nearby/distant comparison and internal weather activation checks
- resource: ../../evidence/catalog.json#E-addons-sky-distance37
  title: Automatic nearby visibility report and distance-policy boundary
- resource: ../../evidence/catalog.json#E-addons-sky-comparison37
  title: Matched near/far requests, readbacks and human visibility comparison
- resource: ../../evidence/catalog.json#E-addons-sky-candidate38
  title: Distant-only storm ranges and isolated held sky control checks
---

# Authoring and export boundary

A deterministic authored bolt has one continuous main channel, six branches and
four smaller offshoots. Each descends from an existing channel point and tapers;
closed six-sided tubes provide volume without camera-facing ribbon alignment.
The asset contains 2,370 vertices and 4,696 triangles at 100 units high. The
Blender source contains only authored geometry and preview setup, after removal
of imported objects and orphan data. Its preview emission/glow is an art preview,
not a transferred game shader or an in-game appearance claim.

The pinned exporter parses WD1's sequential GEOM97.50 archive and rebuilds geometry
using an imported template layout. The tested AH_NeonFlicker template has one
mesh, one LOD and one buffer. Its unedited export is byte-identical. The custom
mesh re-parses with all vertices/triangles and the original material identity;
maximum component error is 0.001563 units. Original template bytes stay unchanged.
The exporter reports the expected quantization-range expansion to fit the bolt.

This verifies an offline parser/writer round-trip, not independent native-format
certification. Three additional geometry tests cover deterministic seeds,
parent-channel connections and descending taper across64 seeds, valid indices,
nondegenerate triangles and closed edge incidence. Multiple buffers/streamed
LODs are deliberately rejected by this proof builder. Internal profiles include
the resulting game resources; public profiles reject them. Dependency tools and
the Blender source are never packaged.

The game candidate uses the one-mesh/one-buffer recycling-dumpster blood model
as its geometry layout carrier, matching the node identities of a minimal
graphic-only source prototype. Its geometry is fully replaced; the original
model path is untouched. The unedited carrier exports exactly. A pinned exporter
adapter fixes buffer-tail alignment when the old index count needs two padding
bytes and the new count needs none. Retaining the old padding caused a two-byte
parse desynchronization. The adapter recomputes absolute alignment before the
following GeomMips section; a regression fixture covers this boundary.

# Native visibility correction

The initial exporter round-trip did not detect a second layout error: its sphere
and box offsets are four bytes too late. Four retail models corroborate the actual
GEOM97.50 fields: sphere at0x38, box minimum at0x48 and maximum at0x54. Three
decoded vertex-extrema comparisons agree within3e-8; the multi-LOD strip differs
by0.001435 on one minimum while its header still encloses the decoded vertices.
The following four floats at0x60 encode negative minimumXY and reciprocal XY
spans, agreeing across the same corpus within2.2e-7. This independent comparison
is stronger than the initial same-parser round-trip.

The shipped initial bolt has a zero-radius sphere and inverted X bounds:
minimumX173.205, maximumX-100. Its single geometry LOD, kill distance and material
LOD cutoffs also retain64 units from the small retail carrier. Recorded shots
place it roughly148 units from the firing point. These are concrete export defects
consistent with unreliable visibility; no per-frame renderer trace identifies
which predicate rejected each reported invisible request.

The bolt-specific finalizer writes tight padded bounds and an enclosing sphere
at the corroborated offsets, recomputes the XY span data and sets all three
cutoffs to512 units. It rejects other versions/multiple LODs. The payload validator
requires finite ordered bounds enclosing every generated vertex, an enclosing
sphere, consistent remap data and the expected cutoffs. The regression test
explicitly rejects the preserved shipped header. Only58 model-header bytes change;
geometry, material/texture content and every other archive asset remain identical.
The final export also checks enclosure against decoded, quantized vertices.

# Model and material references

In the inspected modified runtime entity library,2,414 distinct non-null four-byte
`fileModel` IDs all match known XBG archive path hashes. The remaining distinct
value is FFFFFFFF, the unbound sentinel in this dataset. The join uses the existing
archive algorithm: lowercase backslash path, FNV-1 64-bit, explicit packing hash
overrides, then the32-bit archive normalization. It does not use CRC32.

`CGraphicComponent`/`CRigidGraphicComponent` owns the authored `fileModel` input;
the named editor library provides a parallel prototype context. These are
serialized resource references, not live model pointers. Consumers include the
native resource/graphics loading path, whose timing and residency are not proven
by the static join. Prototype UID/name hashing remains a separate unknown. The
manual test uses an explicit, collision-checked UID through the API's verified
numeric-string argument, rather than deriving an ID from a display name.

The proof template refers to `ppavlou-m-20130307111140.material`, backed by a
`graphics/_materials/*.material.bin` file. That file begins with TAM/version7,
contains template `Unlit` and an authored texture path. Matching parameter keys
against the existing CRC32 name dictionary identifies `HDRMul`, `DiffuseColor1`
and `DiffuseTexture1`. This identifies stored parameters, not a complete material
serializer or their final shader dataflow. Gibbed's generic binary-object converter
rejects its header; it must not be treated as an FCB. The export proof preserves
this retail material identity rather than pretending the Blender emission was
exported. The upstream generic material-export advertisement is not WD1-specific
material support.

The test payload now clones that Unlit material to a dedicated path and changes
only its same-length display name, HDRMul to14, DiffuseColor1 to(.68,.78,1), and
DiffuseTexture1 to a dedicated white texture. The bounded28-parameter reader
identifies one-byte type tags, aligned32-bit keys and typed values; it requires
the exact template hash and end boundary. Unidentified flags/headers are retained,
not interpreted as permission to change shader policy. This is a template-specific
patcher, not a general material serializer.

The white texture preserves an existing XBT/BC1 container layout and complete
mip sizes, replacing every BC1 block with opaque white. Original texture and
material paths are unchanged. The model's serialized CPathID and material path
are both updated. Archive hashing requires lowercase backslash paths: forward
slashes produce a different hash. The builder checks the original CPathID before
changing it. Native material/texture loading and final glow still need game proof.

# Runtime gate

The October runtime capture establishes a separate, earlier failure boundary.
All six installed internal41 package members match delivery hashes and the
manager enumerates all fifteen sky prototype UIDs. Nevertheless, both attempted
sky events fail with `Entity not found (hash: 0.000000)` before any entity-position
or graphics sample. The Lua random preview cancels on its first failed spawn;
the independent native storm continues and records two sound submissions.

For Nexus image SHA256
`03875bacfad447397305b9d5f19bcb07dc4473b99f7d1354604b4a2bb1dfe727`,
registration `11E920` points to spawn wrapper `11BB00`. It still reads a string
hash, parses decimal through `11C3F0`, and queries its UID registry through
`11C4B0`. A null result branches to the observed error before engine creation.
At `11BDF8..11BE05` the formatter receives an integer in R8D with a `%f` format:
the printed zero is not evidence that the supplied ID was zero. The earlier
inspected wrapper has the same mismatch. No numeric-argument conversion is
justified by this message.

Enumeration proves definitions were encountered, not that the later spawn
registry remained correct. A manager compatibility/registry problem is the
leading hypothesis; its exact mechanism and update causality are unproved.
This capture cannot accept or reject World loading, distance visibility, or LOD:
the bolts never reached those stages. These RVAs are read-only evidence locations,
not hooks or additional runtime calls.

Static inspection of the supported spawn API establishes mutually exclusive
string arguments `hash` and `name`. The `hash` string is parsed in decimal,
looked up in the loaded runtime-library index, then passed to the engine spawn
path. On the inspected module identity, the wrapper is RVA1160C0 and its UID
lookup is116A70. These are evidence locations, not new hooks or callable RVAs
in Addons. The implementation continues through the exported Lua API.

UID8F31B017 is appended as a separate library/prototype after checking for a
collision. The builder clones the minimal22ACAEC1 graphic prototype, changes its
model resource and bounds, removes editor file provenance and material overrides,
and disables casting/receiving shadows and size culling. It adds no physics,
lights, electricity or reactions. Every original serialized tree byte after the
root child count and every original prototype-table entry remains exact. Only
the root/header counts and an appended library/table entry change. The existing
FCB exporter independently accepts the result. Empty attribute blocks must encode
a zero-count descriptor; a zero-byte section is rejected by that exporter.

The internal Bolt tab uses Play bolt for the authored mesh and retains a separate
Play tracer control action, plus manual removal.
The mesh test accepts a fresh recorded position only after a successful Arm status,
tracks its owning player and keeps the returned64-bit entity ID as decimal text.
Pressing Play again at the same recorded position extends the owned instance by
ten seconds instead of removing/recreating it. A changed position replaces it.
It requests removal after ten watcher-clock seconds, on replacement, Cancel,
player change or script unload. A failed removal retains ownership and prevents
another spawn until cleanup succeeds; failed expiry removal is retried explicitly
rather than logging failures every frame. Removal diagnostics include reason/age.
No raw renderer pointer is retained by this
module. Lua float-number builds lose low bits in large numeric IDs and epoch
timestamps; explicit ID text and the existing relative watcher clock avoid that.
Timer expiry runs on the next script update, not during a suspended game update.

Tests cover rejected/stale aim, exact ID text, repeated show, expiry, cleanup
failure, player change and unload, plus archive isolation and full established
lighting retention. Historical returned effect IDs did not establish visibility.
A successful Lua call still cannot prove resource readiness or actual retirement.

The [recorded tracer control](manual-lightning-bolt.md) remains the independent
working control. The [shared storm path](public-storm-runtime.md), Moon selection,
world/vehicle lighting and internal tools retain their existing ownership. No
automatic placement, flash synchronization, new light or sound is established
by this asset work. The human report explicitly confirms that the authored
mesh rendered once, with
unreliable repeated visibility. Matched runtime evidence contains13 mesh spawn
IDs and13 removal calls at three recorded positions. It establishes API requests,
not frame-to-request association or successful rendering/retirement. Each Show
in the initial candidate removed/recreated the entity. Following the header and replay
corrections, human feedback confirms reliable repeated spawning, with two visible
mesh captures. Endpoint blending and the stationary presentation remain unfinished. The recorded position is still the tracer endpoint,
not a verified surface hit; native captures can extend far below the firing
point. This repeated-spawn report does not establish comprehensive occlusion or retirement.


# Brief strike preview boundary

The manual preview shares the same resource and recorded-position path as the
long-hold inspection. Its fixed on/off intervals are0.18/0.09/0.10/0.12/0.08
seconds. Each on interval spawns the mesh; each off interval removes the owned
exact decimal ID. No unverified visibility or material-animation API is invoked.
Asynchronous resource/render latency can affect short-pulse appearance and needs
visual validation. Repeated requests do not stack. At most one phase advances per
update; a backward clock or phase lateness beyond0.5 seconds aborts instead of
replaying missed flashes. Cleanup failure retains ownership, stops scheduling and
requires explicit retry. Cancel, re-arm, player change and unload stop all pending
phases. Long-hold inspection remains available and can replace the short sequence.

The main-channel radius tapers near its upper16% and lower4% to6% of the previous
tip thickness. Centerline, branching,100-unit height, topology, material, texture,
prototype and corrected visibility bounds/cutoffs are unchanged. This is geometric
cap softening, not terrain attachment, cloud-depth blending or shader alpha fading.
Decoded output retains three pre-existing degenerate triangles in a small branch;
none are added by the main-channel taper. Offline tests cover phase progression,
precise ID ownership, cancellation, cleanup/spawn failure, inspection switching,
clock gaps and player changes. Ground anchoring, storm synchronization, positional
sound and shadow-producing illumination remain unimplemented by this preview.


Runtime feedback confirms every brief-preview pulse appeared. However, three logged
sequences last2.26-2.35 seconds from initial spawn to final removal, with most
transitions approximately0.5 seconds apart. The configured0.57-second sum is not
the actual visual timing. Logged removal ages agree with wall timestamp gaps;
this does not establish a clock-rate fault. The host update cadence must be verified
before short-pulse or progressive geometry animation can rely on this watcher.
Mock-clock lifecycle tests establish ownership/order but missed runtime scheduling
resolution. Reliable pulse appearance is accepted; rhythm, duration and integrated
scene presentation are not. No precise video-to-log event association is claimed.


# Elevated sky preview and queued animation

The sky preview has three deterministic authored variants, each exported as upper
channel, full channel, branched channel, reduced branches and residual trunk.
Each mesh reaches350 units high with2,048-unit geometry/kill/material
cutoffs and independently validated native bounds. Fifteen explicit prototype IDs
8F31B100 through8F31B108 and8F31B120 through8F31B125 are appended; the original inspection
prototype/model and every original library byte remain preserved. Catalog generation
and payload validation share the explicit asset data, with collision rejection.
Decoded exports preserve vertices/triangles and contain no degenerate triangles.
These checks do not establish distant runtime residency or visual acceptance.

Both aimed and random previews use the same sky event implementation. Its base is
20 units above its anchor, so its top is370 above the anchor. The aimed anchor
copies the recorded position without changing it; random anchors use player XY
plus a selected radial range at a random bearing, and player Z. The original
continuous preview uses350-900 units; the visibility comparison adds120-180 as
the nearby default and retains350-900 as a selectable control. Radius is sampled
uniformly within the range, not uniformly by ring area. These are elevated free-space
sky tests, not verified terrain/roof strikes or actual cloud-height queries.
The continuous diagnostic toggle owns a pool of six independent random events,
staggered by90-220ms; it never catches up overdue spawns in a burst. The aimed
event has separate ownership. Cancel stops both modes. Failed removal retains
the affected pool slot; explicit cancellation retries it. Pause, player change,
backward clock and unload stop the continuous controller. No idle queue remains
after its retained callbacks drain. The old inspection, tracer and pulse controls remain.

Sky models use a separate clone of the verified Unlit material and XBT/BC1
texture. Texture luminance fades over the upper/lower22 percent of model height.
UV brightness bands make reduced branches18 percent and the residual trunk2.5
percent of full texture brightness before BC1 quantization. Reduced branches
remove twigs and shorten secondary paths; the residual stage contains only the
trunk. All mip levels retain native container framing. The inspection material,
white texture and model remain unchanged. This is staged geometry/luminance
decay and endpoint masking, not continuous skeletal animation, alpha blending,
cloud glow, depth-aware intersection or terrain attachment. Visual efficacy needs
game testing; a black Unlit surface may not behave as transparency.

The installed host matches the identity in
[menu host compatibility](../shadow-engine/architecture/menu-host-compatibility.md).
Its SH_NextTick function queues a registry-retained callback with minimum delay1
host drain, independently of the later Script game/time gate. A successor callback
is deferred, not recursive in the same drain. The preview uses one active queued
callback per event owner; no worker thread, new host hook or OnRender assumption.
It requires the queue API and fails closed if submission fails. OnPause cancels
active previews; unload closes the owner so retained callbacks cannot reschedule.
Actual outer host-loop scheduling and render residency remain runtime limits.

Per-event shape, rotation and irregular pulse plan remain fixed throughout a
strike. A small private generator does not alter other mods' math.random state.
Upper-channel/full-channel reveals take25-50ms and20-45ms; the initial branched
flash takes65-145ms, followed by45-95ms reduced branches and40-90ms residual trunk.
Zero to two optional restrikes use35-165ms gaps,25-70ms main channel,
30-70ms reduced branches and35-85ms residual trunk. The fully branched model
appears only once per event. Absolute deadlines skip overdue phases; a1.2-second
ceiling requests cleanup on the next host drain. This is not a hard wall-time
renderer guarantee when the host stops or cleanup fails. Removal failure retains
the exact decimal entity ID and stops scheduling until explicit cleanup succeeds.
Runtime diagnostics record actual phase age and total event age.

Direction diagnostics additionally record player XYZ and sampled bearing/range
for each random request. The first owned entity is read back through the existing
GetEntityPosition API on the next host drain, logging requested/actual XYZ and
their difference once per event. Unavailable reads do not alter playback. This
is transform evidence, not render visibility, residency or occlusion proof.
The placement policy does not inspect terrain, water or map regions. Offline
coverage checks exercise all four XY quadrants around a fixed test player.
Runtime readback now confirms1003 random placements across all eight angular
sectors at351.88-899.87 units, plus one aimed placement. All1004 entity positions
match requested XYZ at logged precision. A reported one-region visual restriction
persists: entity placement success does not establish correct rendered geometry,
visibility, residency or occlusion. No water/city-specific cause is established.

That 1,003-request capture samples player X1836.32-1842.74 and
Y1144.79-1152.13, a small area rather than relocation across the map. Each new
random event queries the current player XYZ; it does not use the recorded aim.
A stable-ID teleport/elevation test verifies that new events follow changing
mocked coordinates, including restart in another region. It does not establish
the live position API's output after travel. Existing events retain their
original positions until their bounded lifetime ends.

Later feedback distinguishes working aimed inspection, brief sky and tracer
controls from the failing continuous preview. The corresponding native shot
capture spans about2,844 units between shooter locations, but its four endpoints
are only148.46-149.09 units from the muzzle. This is not a matched control for
the preview's350-900-unit ring. Visibility at those ranges and under overlapping
playback remains unproved; first compare the relocated preview center, then
isolate distance and concurrency. A successful spawn/position call is not a
render-readiness signal.

The subsequently collected host capture resolves the live-origin question:
2,213 random requests follow player X-942.68 to1897.51 and Y199.24 to1417.69.
All2,225 first-entity readbacks (including12 aimed events) match requested XYZ at
logged precision;849 random readbacks have negative requestedX and1,364 positiveX.
The maximum first-readback age is0.024994 seconds.2,209 completed sky events have
maximum logged age1.037018 seconds. No Addons error, unavailable-transform or
false-result marker occurs in that capture. Thus the recorded placement and entity
transform path follows travel; neither that result nor successful removal requests
establish rendering, occlusion, resource residency or a particular culling predicate.
Distance and concurrent playback remain unisolated differences from working controls.

# Internal storm preview policy

Human feedback confirms automatic storm activation and nearby visibility around
the player. The nearby appearance is rejected for regular storms; normal weather
must use distant placement. Nearby strikes are reserved for explicit diagnostics
or a separate rare future event. Subsequent same-build near/far comparison at
different map locations reports sharply fewer observable distant bolts and a
recurrence of the directional restriction. The host capture contains99 nearby
and832 distant placements, all931 first-stage readbacks matching requested XYZ,
and no logged Addons spawn/cleanup failures. This supports distance-dependent
observable visibility, not a particular renderer failure predicate.
All fifteen sky meshes already declare2048-unit geometry/kill/material cutoffs;
the sampled appended prototype disables size culling. Other inherited entity,
loading and renderer behavior remains unverified.

The visibility candidate retains the same assets, six-slot pool,90-220ms diagnostic
cadence and event lifecycle. The initial comparison separates120-180 nearby from
350-900 distant. After nearby appearance rejection, normal storm profiles contain
only350-900 distant and900-1500 far-horizon ranges; distant is the default.
Changing range cancels owned events
before restarting; cleanup failure blocks the transition. The three aimed controls
retain their own recorded anchor and event ownership.

An internal observer records the last accepted native storm scheduling frame;
it forwards the existing audio observer exactly once and clears on storm retirement.
It owns only an atomic timestamp/valid bit, never the native storm state or output.
Lua requests a fresh weather decision through the existing no-result native export
bridge and a fixed adjacent exchange file. A bounded request serial must be echoed
exactly; a missing/partial/stale response is inactive. The native response also
requires an enabled diagnostic session and a scheduling frame within500ms, using
wrap-safe elapsed ticks. File I/O occurs only on an explicit Lua poll, not in the
native frame hook. No unverified Lua C ABI or new engine RVA is introduced.

Automatic preview intent defaults on; the existing Script watcher polls at most
four times per clock second (the observed host cadence is about two). Valid storm
activity starts the pool; weather exit cancels it. Manual preview can run in clear
weather. Stop/Cancel disables both intents until explicitly re-enabled. Pause
cancels events and clears the weather sample; automatic mode can resume after a
fresh poll. Unload closes the controller. A pool interruption or startup failure
disables automatic retry. Offline tests cover these transitions, failed exchange,
cleanup failure, relocation and the range comparison. Automatic activation and
nearby visibility have human confirmation; distant visibility remains unresolved.

This is weather activation only. The accepted native flash/thunder scheduler is
unchanged; its flashes, shadow illumination and delayed sound are not yet scheduled
from the same custom bolt event. Public runtime sources do not include this observer,
exchange or policy.

The held distance control isolates one full branched sky mesh (variant1/stage3)
at350,600,900 or1400 horizontal units along a fresh recorded shot bearing. It
samples current player elevation and uses the same20-unit lift. It stops other
sky previews and automatic intent, requires successful cleanup, then uses the
shared spawn/readback/removal owner with one mesh held eight seconds. Normal
animated events retain their1.2-second ceiling. Fixed control orientation and
geometry avoid changing silhouette while comparing distances. It adds no asset,
native hook or guessed culling-field patch. Pause, Arm, Stop, Cancel, player change,
clock reversal and unload retire the control; removal failure retains ownership.
This duration test can distinguish a steadily visible distant mesh from rapid
stage-swapping behavior. It does not itself prove the renderer's cause.

Host-queue tests complete events without any Script OnUpdate dispatch, checking
short duration, missed-frame skipping, variant/timing changes, precise ownership,
independent aimed/random events, elevated random bounds, queue/removal failure,
clock gaps, player replacement and unload. The scene flash, shadow-producing light
and distance-delayed thunder are not yet consumers of these sky events; the
accepted shared storm continues unchanged. This stage tests elevated placement,
progressive geometry reveal and irregular visual timing together.


# Related native graphics findings

[Entity transforms, graphics activation and loading categories](graphics-activation-and-streaming.md)
owns the native component factory/vtable distinction, LOD/render-group checks,
the failed observer control, and World/Near streaming mappings. A transform
readback does not prove graphics publication, residency, occlusion or visibility.
The .41 spawn-registry failure recorded above occurs before those checks.


# Mod-owned activity windows and concurrent events

A later internal-only implementation (2.1.46 source controls) separates the
activity policy from mesh ownership and the native flash/audio mechanism. This
is mod behavior, not a newly discovered native storm scheduler. Earlier sections
above describe historical experiments; their file-based weather transport and
independent flash scheduling do not describe this implementation.

Lua polls the existing native weather gate through the validated string exchange,
then owns a 60-second calm/strong window or a 30-second peak window. A separate
20-40-second quiet phase follows. Peak selection has probability 1/50 per automatic
window, not a guarantee that every block of fifty contains exactly one peak.
Ordinary windows choose calm/strong with 75/25 weights. Explicit previews use the
same owner and replace an active window instead of starting a competing scheduler.

A volley owns at most three entity IDs, each retained losslessly as a decimal
string. Name-based prototype resolution is retained. Each new volley samples
current player coordinates; members share a narrow bearing sector at horizontal
ranges 900-1500. Reveal/full/decay swaps preserve each member's origin and variant.
Cleanup failure retains the ID and blocks replacement. Weather loss, player
replacement, clock discontinuity, pause and unload cancel owned activity.

The original single-event native owner could not accept simultaneous START
requests while another event or its delayed thunder remained pending. An eight-slot
pool now retains each accepted event's duration, distance, sound variation and
serial under a critical section. A successful mesh spawn precedes its request;
failed group setup cancels all submitted members. Audio delay uses distance/343,
while simultaneous sky envelopes combine by maximum rather than addition. Active
serial duplicates and full capacity are rejected. Native weather freshness and
sound eligibility remain required; previews do not override weather.

The last five seconds of a window admit no new volley, allowing a three-second
mesh and up to 4.374-second thunder delay to complete before the quiet boundary.
Timing uses the existing runtime clocks rather than accelerated world time.
Offline fixtures exercise ten minutes of automatic timing, all three forced
windows, probability boundaries, local cluster limits, animation stages, quiet
periods, failure cleanup, pool saturation and actual Lua/native transport. The
canonical internal-world profile passed with unchanged DAT/FAT/NFO payloads.
These checks do not prove in-game visibility, smooth stage travel, audio balance
or visual acceptance. The referenced archive preserves source/test controls;
no human runtime result for this activity implementation is available.


# Weather readiness is not controller execution

The internal .45 game test reported working manual bolts but no automatic
bolts/flashes. Its matched native log reaches STORM active after initialization;
all six installed files matched the delivery. This proves a passing native gate
at that point, not receipt of STATE in Lua or completion of a START request.
No STORM_FLASH is recorded. The source driver already bypassed native random
strike scheduling; failure cannot be attributed to waiting for a native random
strike merely from the user-visible absence of lightning.

Static inspection of NexusTools PE 6AB6AD4E/ED6000, SHA256
03875bacfad447397305b9d5f19bcb07dc4473b99f7d1354604b4a2bb1dfe727,
identifies SH_NextTick binding B4730 storing a Lua registry reference and enqueueing
an invoker. B5E40 obtains the current VM at execution time, looks the reference up,
and calls it only if helper D2440 identifies Lua type6 (function); the alternative
path pops/unrefs the entry. Successful enqueue is therefore not a delivery
acknowledgement. This static map does not prove reference loss in the .45 run.

The mod pump's ordinary OnUpdate fallback previously refused execution while its
queued flag remained set. A dropped-callback fixture reproduces indefinite idle
with the old code despite subsequent OnUpdate calls. In internal .47 the fallback
always drives the shared service, with same-clock duplicate suppression. A stale
queue ticket expires after half a second; generation checks prevent late replaced
callbacks from starting duplicate chains. Pause invalidates tickets, and a queue
failure leaves ordinary updates operational. Automatic bolt animation also moves
into this shared driver, removing its separate lost-callback lifetime dependency.

The actual bundled Lua/native fixture runs both queue-only delivery and a separate
run discarding every queued callback while registered OnUpdate continues. Both
produce mesh requests, actual native flash envelopes and delayed audio in the
harness; the latter also completes a strong-window preview and quiet break.
Weather-reply and START-result traces are bounded in the existing host log.
These are offline failure-recovery results. The .45 logs do not establish its
exact failed boundary, and a .47 game test remains necessary.

# Controller exceptions can mimic an inactive weather gate

The subsequent internal .47 human test reported that continuous random preview
worked but automatic activity and the window previews did not. All six installed
files matched the delivered .47 archive. The matched host log contains14,923
identical protected-call errors at generated line262: `attempt to compare number
with function`. This line compares `now` and the captured `lastClock`, before the
automatic controller calls STATE. The native log contains14,923 BOLT_CANCEL
records: the pump's error path calls pause, which cancels storm activity and
diagnostic aim. The service is executing and failing, rather than merely awaiting
an undelivered queued callback.

At the end of the recorded run, the first STATE request returns REPLY1 1 and is
logged active=true; zero STORM_EVENT/START records exist. The preview entry path
can request STATE without passing through the failed update clock check. This
supports separating weather readiness from controller health. Continuous preview
has its own scheduler and does not establish automatic-controller health.

The error proves a wrong-type operand in the clock comparison. It does not identify
which operand changed or explain the target VM's capture/storage behaviour.
The same run had the separate Shadow Engine2.0.90 experimental Lua-frame repair
active; this is configuration identity, not evidence that the repair caused the
failure. No captured prototype/upvalue dump exists for the failing controller.
Desktop Lua tests had passed, so they did not model this runtime failure.

A scoped .48 mitigation places clocks, player/window state, counters and owned
slots in one strong state table instead of independent mutable captures. It
retains the existing weather gate and direct mod-owned START scheduling, without
waiting for native random lightning. The auxiliary Lua5.1 compiler reports a
maximum22 registers within this module versus30 previously; the generated bundle
reports23. These are non-target compiler measurements, not proof of native frame
safety or a repaired capture mechanism. Stack-reuse/forced-GC lifecycle fixtures
pass under that offline Lua runtime; native game acceptance remains required.

# Visible automatic activity and presentation timing

A subsequent human test of the unchanged internal2.1.50 with active A4EE regional
Lua-frame repair confirms bolts and flashes in ordinary storm weather. This
establishes automatic visibility in that configuration, while the reported
presentation remains unsatisfactory: close aligned clusters, simultaneous starts,
slow bolt/flash progression and sparse calm activity.

Source inspection distinguishes mechanism from appearance. Cluster members all
receive the same start time. Angles advance by a fixed0.045 radians, and distance
uses one center with plus/minus80 units of jitter. Independent variant/rotation
selection does not remove that shared spatial/temporal pattern. Bolt lifetime is
1.5-3 seconds; mesh boundaries occur at10/24/40/65/100 percent. The mod-owned
native flash driver scales its stepped envelope across that same duration.
Thus visual mesh readability also stretches sky illumination. These are authored
mod policies, not measured native lightning timing. The human report is not a
frame-duration capture, and replacement timing remains untested.

# Porting approved centerlines and separating event clocks (historical control)

The approved winding, forked and horizontal cloud-crawler study was converted into
15 native XBG meshes: two arrival-time reveal stages, a full channel, branch decay
and a dim main-channel tail. The original point coordinates remain unchanged;
tangent-oriented tube rings support horizontal/nonmonotonic paths. A0.04-unit
radius floor prevents quantized tip collapse; the native conversion widens authored
radii by1.8 for distance readability. All decoded vertices differ by under0.005
units, the retail template roundtrip is exact, and no quantized triangle collapses.
These are format/geometry checks, not proof of game material appearance.

Existing resource names/IDs, the World loading category and2048-unit visibility
cutoff remain. Bounds are derived per mesh instead of assuming all variants have
identical height. The inspection bolt is unchanged. The package comparison finds
only15 sky XBGs and the appended entity-library bounds changed among1910 archive
members;1894 entries, including world lighting and material/texture data, match
the prior package exactly. Centerline equality is checked against the approved
study separately from exporter roundtrip checks.

The mod-owned service now keeps a0.8-1.5s mesh lifetime separate from70-180ms sky
pulses. The main pulse begins at18 percent of mesh lifetime, aligned to full-channel
entry, and may have a weaker short echo. Thunder starts after that main-stroke
onset plus distance/343. The existing native sky output remains the rendering
boundary. A separate FLASH command queues weaker, mesh-free, silent events;
it does not implement localized illumination or replace the global sky flash.
Twelve private native event slots cover delayed thunder plus brief extra flashes.
Events combine by maximum intensity, not addition, and still retire on weather,
pause, cancellation and session loss. No new native function/layout was assumed.

Cluster planning samples a local angular region, keeps every member900-1500 units
from the player, rejects pair distances outside180-650 and rejects three-point
altitudes below90. Delays increase by120-420ms per member. Bounded failed placement
attempts reduce member count rather than introducing an unsafe fallback position.
At actual start each member samples the current player position; its resulting
world anchor remains fixed for all animation stages. A late start with insufficient
time for delayed thunder before the quiet boundary is discarded.

Offline tests cover2000 cluster plans, absolute animation phases, cadence, silent
breaks, prototype limits, twelve-slot saturation, non-additive overlap, distance
thunder, mute/cancel and cloud flashes without a mesh/audio allocation. Real bundled
Lua/native tests still work when queued callbacks are discarded and normal Script
updates run. All125 shipped Lua prototypes pass with maxima23/14/3. Five-profile
native gates and retained-lighting/archive checks pass. New target-game timing,
visibility and audio acceptance remain unobserved.


# Endpoint-domain masks and tighter distinct pairs

Human feedback on the preceding presentation rejected the horizontal crawler and
standalone cloud-flash appearance, the wide group arrangement, and the short custom
white sky pulse. This is qualitative visual evidence; no frame capture or exact
regional image was provided with the report. Offline geometry success had not
predicted those aesthetic results.

The retained winding/forked shapes each keep five reveal/full/decay stages. Only
their ten meshes and prototypes enter the payload; crawler preview source remains
historical material. Two-member groups use distinct shapes, independent rotations,
65-190 units pair separation and120-420ms stagger. Bounded rejection sampling
avoids a fixed angular row while retaining900-1500 units player distance. Two
unique retained shapes cap a group at two rather than duplicating one in a triple.
The2000-group corpus checks distance, spacing and delay; bundled-runtime tests
check different prototype names within a pair. Real moving-scene appearance is
still unverified.

The earlier UV mask used generic z/350, although the winding trunk occupies roughly
85-290 and the forked trunk70-315. Consequently its endpoints never reached both
dark texture edges. UV v now uses `(z - trunkBottom)/(trunkTop - trunkBottom)`,
clamped near0/1 and stable across reveal stages. The existing22-percent smooth
luminance fades now align to each trunk's actual endpoints. An additional upper
geometry taper spans14 percent, retaining a0.04 radius floor against quantization.
The material and BC1 texture are unchanged. This is emissive endpoint masking;
it does not create cloud volume, depth-aware occlusion or verified alpha blending.

Independent decoding checks all ten exported meshes for vertex/UV error and
degenerate triangles. Source tests verify endpoint UVs and stable coordinates
across phases. Archive comparison against the prior control finds ten changed
sky meshes, one changed appended entity library, five removed crawler meshes,
and1894 byte-identical retained entries. The inspection bolt, materials, textures
and retained world lighting remain identical.

Standalone FLASH admission is removed. Each main-channel onset instead requests
one [native animated pulse](basic-lightning.md#explicit-pulse-admission-with-native-animation).
Bolt lifetime0.8-1.5s and activity intervals7-18/6-14/2-6s remain mod-owned policy,
as do60/60/30s windows,1-in-50 peaks and20-40s quiet breaks. All124 final bundled
Lua prototypes pass31/15/15, with actual maxima23 registers/14 upvalues/3 fixed
parameters. All11 controls and existing ownership/lifecycle checks pass offline.
Visual masking, flash character and native-boundary runtime acceptance are pending.
