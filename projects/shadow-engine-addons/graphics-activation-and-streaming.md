---
type: Technical Reference
status: draft
title: Entity transforms, graphics activation and loading categories
sources:
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

# Scope

These Global Watch Dogs 1 mappings were investigated with an authored lightning
mesh. Successful entity placement is distinct from graphics activation and a
visible draw. The [asset case study](custom-lightning-asset.md) records construction
and spawn-registry failures, including the later .41 run that failed before
graphics creation. The experiments below do not override that boundary.

# Native graphics placement boundary

The subsequent distant-control feedback reports no visible bolt; it does not
enumerate controls, distances or a completed comparison matrix. It establishes no
successful distant hold and does not identify a renderer rejection condition.
The following is static evidence from the identified Global capture, not live
bolt graphics-state proof. Other profiles have not been mapped for these roles.

| Boundary | Inputs, output and ownership |
| --- | --- |
| Nexus `0x1160C0` → `0x0A4680` → `0x0A4810` | Spawn wrapper packs the requested transform and forwards it to the resolved native creation function. Omitted `spawningCategory` defaults to 9. No distance/region predicate appears in this wrapper; this does not exclude native loading policy. |
| Global `0x7E13B0` | Constructs CGraphicComponent and initializes its separately owned cached matrix at `+0x150..+0x180` to identity. Entity coordinates are a different state boundary. |
| Global `0x7D0070` | Obtains entity through `[graphic+0x10]+0x08`, reads its transform through `0x823560`, applies optional component scale and copies into the cached matrix. Forwards translation through `0x40FCA0`, then enters `0x7CC010`. |
| Global `0x7CA330`, `0x794EF0` | Creates geometry instances using cached translation; group synchronization composes the cached matrix with the model-part transform and publishes via `0x409B80` when enable predicates pass. Existing groups also reach synchronization through `0x7CC010`. |
| Global `0x78C450` → `0x409990` | `bAllowCullBySize` writes graphic `+0x109` bit5 and forwards it across owned groups to renderer record `+0x4A` bit3 (`+0x1A` within its `+0x30` subrecord). False disables this flag; it is not a general visibility override. |

Consequently, matching entity readbacks do not establish matching cached graphics
transforms, renderer placement or visibility. Identity initialization provides a
specific initialization/update path to investigate, but does **not** prove that
distant bolts remain at the world origin. The dispatch condition, a skipped update,
exact distance threshold and any region restriction remain unproved. No global
culling change, spawning-category override or graphics-memory repair follows from
this evidence. No native pointers were retained or runtime writes introduced.

# LOD selection and renderer rejection

Further human feedback describes one or two rare distant appearances elsewhere
while driving on an unspecified older candidate. This is not a matched capture
or proof of a fixed map boundary. Distance-dependent loss remains the supported
observation; an absolute inability to render outside one area is not established.

The Global geometry loader at `0x36F880` calls header parser `0x34E7B0`.
For the authored single-LOD GEOM97.50 layout it copies file offset112 to native
geometry record `+0xE8` (LOD count), offset116 to the first16-byte LOD entry at
`[record+0xE0]+0` (distance), offset120 to `record+0x170`, and offset126 to flags
`record+0x192`. Sphere center/radius at file56..68 become record `+0x70..+0x7C`.
Material-distance parsing continues at `0x346E80`, using a count derived from
geometry LOD count minus the file128 value. All fifteen authored sky meshes have
one LOD, all three serialized distances2048 and flag bytes `01 01 FF`.
These fields are consumed by native code, not merely exporter annotations.

`0x2C9CC0` selects geometry LOD from a render-object record, geometry record and
per-view settings. It measures the distance between view `+0x5C` and renderer
`+0x1C0`, subtracts renderer `+0x1F4`, clamps at zero, then applies a conditional
scale before comparing the LOD-entry distances. Selection is bounded to the
last available LOD. With one LOD it returns index0 even beyond the threshold;
this selector does not switch to a nonexistent low-detail bolt.

The renderer caller around `0x2F06A0..0x2F0C90` has separate rejection paths:
geometry quality flags, projected sphere size, a view-level size threshold,
distance and further visibility masks. `0x2F0AF5..0x2F0B53` derives a rejection
distance from the **last LOD entry**, renderer `+0x1F4` and view fields
`+0x98/+0x9C/+0xA4`; the flag returned by the selector chooses the scale field.
Its result reaches the rejection at `0x2F0C69..0x2F0C70`. The copied header field
`geometry+0x170` alone is therefore not a complete rendering-distance contract.
The size-cull bit gates one check at `0x2F096A`; it does not bypass every later
check. No observed bolt has yet been tied to one of these rejection branches.

The internal automatic observer samples exact caller-owned IDs at spawn, the
next host drain and before removal. It calls only the existing-reference lookup
`0x18B620`, not allocating wrapper `0x1B6EF0` or entity factory. After Global
signature/vtable gates, copied reads check entity identity, unique graphics
component, owner backpointer, matrices, counts and render groups. Producer and
published renderer views are read through registry `+0x90/+0x98`; `0x25AEA10`
establishes the latter. Renderer instance handle `+0x38` selects registry
`0x36BB2C0`, whose sole part `+0xE0` carries batch handle `+0x30` into
`0x36BB4C0`; its geometry handle `+0x18` selects `0x36B7A30`.

`SKY_GRAPHICS` records entity/cache positions and flags. `SKY_RENDER` records
producer/published LOD-reference position, matrix translation, enable and size
flags, geometry LOD count/cutoffs/sphere and availability guards. Log names
`batchReady` and `lodReady` report the native batch `+0x10` value and LOD entry
`+4` flag; **neither is proof of GPU residency or a draw**. Failed status lines
contain partial/zero defaults and must not be interpreted as valid geometry.
Copied observations are not atomic across renderer publication; unavailable or
changed identity is reported and no pointer is retained. A nonzero renderer
object is not a visibility verdict, and per-view effective cutoff, occlusion
results and final GPU draw are not sampled by this candidate.

One shared Lua owner caps selection at two entities per second and600 per module
lifetime; native output is additionally capped at1800 requests per process.
An adjacent fixed request file and existing native log transport the observations.
No new menu, hook, engine memory write, update forcing, near-distance fallback or
asset change is introduced. Unsupported layouts fail closed. Unit tests exercise
malformed/exact IDs, read failures, publication absence and copied layouts; the
relocation corpus checks observer lifetime before removal. Captured-layout checks
are Global only. Neither these checks nor package validation is visual acceptance.

The native position setter is not a demonstrated repair: `0x11EB4D0` reaches
`0x83DF30`/`0x83A2C0` and transform commit `0x836240`, which returns when the new
matrix compares equal to the current entity matrix. Reapplying the same position
cannot be assumed to force graphics publication. A displacement nudge or calling
the recurrent graphics update outside its established dispatch phase remains an
unperformed, unvalidated experiment.

# Completed component identity and first observer failure

The first matched automatic-observer run contains610 requests at351.747..898.757
horizontal units and610 matching entity-position readbacks. Its187 sampled IDs
join exactly across host/native logs, with561 spawn/update/end observations.
Every native observation stops at `graphic_not_unique`; there are zero
`SKY_RENDER` records. Human feedback again reports visible bolts near the familiar
area and none outside. No per-bolt visibility markers were supplied, so this run
cannot locate a renderer transition or establish the cause of that restriction.

The observer contained a concrete identification error. Constructor `0x7E13B0`
installs base table `0x2F13200`, but registered factory `0x81F320` then writes
**`0x2F17D30`** to the completed component before returning it. Registration at
`0x7E6D2E` supplies that factory. The completed table retains class getter
`0x7EF6B0` and recurrent update `0x7D0070`. The base table is also restored during
base destruction at `0x7D6E80`; it is not the appropriate live-object identity.
Matching only the base table rejects a valid factory-created component. The old
failure message did not record whether there were zero or multiple matches; do
not infer either count from that run or interpret it as missing game geometry.

The corrected internal observer requires the factory's completed-object table,
checks the factory's RIP-relative table load/store bytes in its Global gate, and
retains component count, match count and up to four module-relative vtable values
when a snapshot fails. Unrecognized components remain rejected. The offline gate
derives the final table from captured factory instructions and checks registration,
construction order, final store and class/update slots. The native fixture uses
that independently checked value and tests rejection of the base table. Earlier
tests verified a self-consistent base-table fixture but missed the factory's
replacement; they did not validate the live component identity.

This repairs observation, not the lightning visibility issue. The correction and
build alone establish no live state or visibility result. The subsequent matched
capture below supplies the first successful observations. Bolt resources and
spawn behavior remain unchanged, with no new controls or game-memory writes.

# Observed graphics activation failure

The matched corrected-observer capture contains1,769 random placements across
player X-945..1889 and Y270..1497, plus1,771 exact entity-position readbacks.
Requested horizontal radii cover350.655..1497.197 units. The installed native and
Lua files match the delivered package. All545 selected IDs join between host and
native logs, with spawn, next-drain and final observations over about286 seconds.
These are sampled **mesh instances**, not a census of all phases or storm events.

| Final sample | Count | Copied state |
| --- | ---: | --- |
| Graphics still uninitialized | 534 | Entity position correct; graphics translation zero; zero render groups/objects; entity flags `22049280`. |
| Renderer object created | 10 | Entity, graphics and both renderer views agree; matrix error zero; entity flags `A2179284`. |
| Entity unavailable | 1 | No valid final graphics state; excluded from both categories above. |

All545 spawn and next-drain samples have zero render objects. The20 successful
producer/published records occur at final observation. Each has enable1,
size-cull0, one LOD,2048 cutoff/header distance and zero distance bias. These ten
instances prove that the resource chain can reach the renderer at distant
coordinates; they do not prove a GPU draw. Nine have requested X2291..2637, while
one is at approximately(-1105,29). Human feedback reports many bolts near the
familiar area and very rare appearances elsewhere, but supplies no per-bolt
markers. The spatially clustered renderer creation is consistent with that report;
it is not an exact correspondence between a logged instance and a visible bolt.

The Global lifecycle establishes a concrete boundary behind this split:

* `0x856AC0` sets entity `+0x60` bit2 and dispatches each component's vtable
  `+0x30` callback, followed by `+0x38`. Completed CGraphicComponent `+0x30`
  resolves to `0x7D0050`, which calls group activation `0x7CBD80`.
* `0x8236A0` reads entity bit2. The graphics resource-completion path at
  `0x7CBF70` calls `0x7CBD80` only when that predicate is true.
* Bit2 is clear in every valid failed final sample and set in all ten successes.
  The failed graphics state still matches pre-activation initialization. A
  correct entity transform alone therefore does not ensure graphics activation.

This locates the observed failure **before creation of a drawable render object**.
Changing the mesh's LOD cutoff alone does not address that captured state.
The upstream activation/streaming decision, any distance threshold, and whether
activation was delayed beyond these short mesh lifetimes remain unresolved.
Point samples cannot exclude intervening state transitions or additional renderer
rejection after activation. No arbitrary spawning category, global culling change,
forced callback, lifetime change or near-player workaround is validated by this
capture. A repair must respect the entity lifecycle and renderer execution phase.

# Sky loading-category correction

The appended sky prototypes inherited `wlucatLoadingUnitCategory=2` from the
blood-prop template. This is **Near**, not an unspecified default: the Global
name table at `0x3626970` assigns World0 and Near2, also exposed by the entity
serialization registration at `0x85EE10`. Getter `0x8237B0` extracts entity
flags `+0x60` bits11..14; setter `0x77B740` replaces those bits. Registration
binds those callbacks to `wlucatLoadingUnitCategory`. All544 valid final samples,
including the ten renderer successes, decode to Near2. This is separate from
the Nexus spawn wrapper's omitted `spawningCategory` argument, whose default9
is retained; no interpretation or override of that argument is required here.

Native provider selection `0x69EB40`/`0x6DB2C0` indexes the loading manager's
`+0x130` provider array using that category. Constructor `0x6E6AF0` selects
local grid providers for Near2. For World0 it constructs one world-wide unit
through `0x6E15E0`/`0x6B7790`. Initialization enumerates category0's unit and
requests state2 at `0x6E6F83..0x6E6F8E`; its callback `0x6DBB50` retains a
loading demand through unit `+0x15A` and forwards `0x6D55F0`. The World query
`0x6AF700` checks only overlap with that unit's world rectangle via `0x6F0430`,
not distance from the player. This is not infinite off-map coverage.

Normal queued loading work at `0x6DB8C0` checks entity resource readiness and
dispatches entity vtable `+0x68` at `0x6DBA11`. For CEntity this is `0x856AC0`,
which sets the activation bit and dispatches the graphics activation callback.
Changing the authored category therefore changes loading ownership before
normal activation, rather than bypassing resource readiness or manually invoking
graphics updates from Lua.

Only the fifteen appended sky-stage prototypes now declare **World0**. The
inspection prototype and all existing entity trees remain byte-identical. A
comparison with the preceding payload finds exactly fifteen `02` to `00` byte
changes in the entity library; the other1,909 archive inputs are identical.
No model/material/texture, range, cadence, animation lifetime, weather gate,
sampling control, engine hook or runtime write changes. Existing exact-ID
removal still owns each short-lived instance; World category does not make
the Lua effect permanent or move its spawn point.

Captured-policy checks independently verify enum identities, serialization bits,
provider construction, world-unit demand and the readiness-gated activation
callback. Payload tests require World0 on every sky prototype and retain Near2
on the original template and inspection prototype. The normal build gates also
verify actual archive/input bytes and existing lighting/world features.
This is an evidence-supported correction candidate, **not yet a visually
accepted repair**. Resource latency, off-map bounds and renderer rejection after
activation remain possible limits. Existing automatic S/T/E logs retain entity
flags and renderer state for evaluating the resulting activation rate.
