---
type: Engine Subsystem
title: Retail Storm Audio Dependency Loading
description: Retail selected-lightning dependency collection and the isolated Storm A resource
  extension.
tags:
- shadow-engine-addons
- thunder
- loading
- resources
- moon
- tfowc2
status: draft
sources:
- id: public-storm-promotion
  resource: public-storm-runtime.md
  title: Separating a storm hook host from optional observers
- id: v227-first-entry-rear
  resource: ../../evidence/catalog.json#E-607303853326
  title: First-entry native storm loading and repaired rear specular references
- id: collector-live
  resource: ../../evidence/catalog.json#E-917b18ede199
  title: Environment registration and live enabled hook with absent resources
- id: legacy-comparison
  resource: ../../evidence/catalog.json#E-4d67ab11f55a
  title: Supplied134 identification and legacy107 initialization comparison
- id: v226-runtime
  resource: ../../evidence/catalog.json#E-db426a3dbb71
  title: Seven resource failures with installed but unobserved collection hook
- id: preflight
  resource: ../../evidence/catalog.json#E-06d7c75a9caa
  title: Retail loading and release knowledge preflight
- id: native-environment
  resource: ../../evidence/catalog.json#E-cedc32cad096
  title: Exact selected-lightning sound dependency enumeration
- id: native-resource
  resource: ../../evidence/catalog.json#E-22abb8cb608d
  title: Native sound-ID collection helper and resource loading/release boundaries
- id: typed-resource
  resource: ../../evidence/catalog.json#E-5035f108662e
  title: Typed CSoundResource acquisition and lifecycle consumers
- id: package-path
  resource: ../../evidence/catalog.json#E-543f1201a5f6
  title: Native SoundBinary path construction and dependency collection
- id: settings
  resource: ../../evidence/catalog.json#E-899743091a0e
  title: Lightning settings construction and resolver fallback limits
- id: records
  resource: ../../evidence/catalog.json#E-92432a7aadb5
  title: Storm IDs and silent Moon record
- id: live
  resource: ../../evidence/catalog.json#E-7934fc497f4f
  title: Live root resource absence and archive audit
- id: implementation
  resource: ../../evidence/catalog.json#E-7937e14368fb
  title: Native collector extension without Moon writes
---

# Consequential runtime evidence

v2.1.22 showed storm visuals but no audible thunder; copied sound IDs and gate
inputs alone did not establish playback. v2.1.23 restored native-update scheduling
and still produced no audible thunder. v2.1.24 observed 13 accepted event 1B2CA
submissions with distinct valid handles, readiness 1/1 and 39 valid pulse summaries;
deadlines progressed once per pulse approximately 0.517–0.864 seconds after
creation. Acceptance did not prove downstream resource resolution or mixing.

v2.1.25 recorded 15 matching command results 8000E002. Live reads found all 32
package header IDs absent, with resident positive controls; 16 inspected mod FATs
contained no matching override paths. Initial v2.1.26 collection installation was
ready but had zero callback records and seven exact event/handle failures. A
same-process save reload invoked the collector once, loaded all four storm sound
roots and changed commands from 15 failures to nine successes; thunder became
audible. The observation established the missing collection/first-entry boundary,
not a volume defect or reason to reset global audio. v2.1.27 added first-entry
Environment-owned acquisition and received the later runtime confirmation above.

The mechanisms below explain this sequence. The later
[host separation](public-storm-runtime.md) has independent offline evidence.

# Missing retail step

Legacy comparison: The inspected legacy package exactly
matches all seven packaged files in archived1.0.34. It is the bolt/rear-light
diagnostic with automaticWeather=0, not the storm/thunder reference. Its logs provide additional runtime evidence.

The reference remains1.0.7 ASI SHA256
82761EC3C600115F17E9BF7867523D1563ED7644A005F0C1BE061352700E23D1.
Recovered legacy VA10001CD7 initializes natural/manual scheduler states and a
manual settings clone. VA10001B15 uses VirtualQuery region scanning to locate
existing Storm A settings; it does not establish sound-resource loading. These
are static legacy implementation roles, consumed by its update hook; raw process
scanning does not establish valid borrowed-record lifetime.
Legacy VA10001C85 forwards the resolved-output lookup, not a sound-bank preload.
The old Lua/bootstrap and one-entry headlight NFO supply no separate sound
player or packaged soundbank. Decompiler function fragments limit whole-binary
claims. Resource residency during the historical successful run remains unrecorded.
The older successful run did not record initial resource residency, so it cannot
by itself explain first-entry loading.

Retail dependency callback9FC8E0 reads the selected lightning record at
environment+498 and calls275DC0 with its strike+7C and thunder+80 IDs. Both calls
are gated by strike != FFFFFFFF (the second gate deliberately checks strike
again). TFoWC2's selected Moon record has both IDsFFFFFFFF. Thus that callback
does not request either storm sound for Moon. Addons' private Storm A scheduler
had no equivalent dependency collection, despite requesting the correct events.

This statically recovered selection/loading mechanism is consistent with the live absence
of event1B2CA and related1B2C8. TFoWC2 does not replace these files in the inspected
packs. The missing behavior is loading the additional sidecar's resources, not
increasing volume or replacing retail audio. Audible restoration is still an
in-game validation gate, not proven by static reasoning or offline tests.

# Native boundaries

The .26 controlled reload confirmed audible thunder. Before reload the
registered Environment slot points exactly into Addons, ready=1, active=1 and
counter=0; all four storm roots are absent. After returning to the main menu and reloading the same save without restarting, counter=1 and all four have loaded
payloads. The log changes from15 commands8000E002 before collection to9 successful
commands afterward. Runtime feedback reports "Yes, thunder is audible now". Native sound
IDs/helper/playback work in this scenario; the remaining defect is first-entry
resource initialization. Late initialization is the leading explanation, but
exact first-load chronology was not instrumented. The .27 first-entry experiment below addressed this lifecycle boundary.
Reload alone was a workaround, not a general initialization repair.

Additional captured Global mappings (all native-owned; read-only inspection):

| RVA | Role and ownership |
| --- | --- |
| A5EFD0 / A49730 | Named Environment constructor/destructor; primary vtable2F5FA60 confirms collection slot virtual+30. |
| 15D7A0 | Base subsystem constructor registers owner/function callback in collection registry global3B593A8. |
| 148FA0 | Seven-byte thunk preserving incoming registers and tail-jumping through owner virtual+30. Environment resolves to9FC8E0. |
| 148F60 / 148F80 | Set/clear owner+E0 and forward virtual+20/+28 to Environment auxiliary-resource publication/clear9FC7C0/9FC880. Flag is not thunder-loaded state. |
| 1545B0 / 154620 | Copy48-byte callback entries into first/second registry vectors; owner at entry+8, target+10. This mapping does not establish a safe Addons list-mutation boundary. |
| 152990 / 1503B0 | Callback removal delegation / registry initialization. Engine owns registration lifetime. |

For frozen26 ASI hash172DFEA862B4DC0CB7E8D4CA2D11123EC3523CBAE897093F54948BB104B7773C
only, compiled hook RVA86E9 reads ready10C28, active10C2C and counter10C30;
forwarding pointers10C10/10C18 resolve to the native callback/helper. These offsets
are inspection evidence, not a runtime ABI. Live code-prefix/forward checks and
repeated bounded registry reads passed. Snapshot agreement is not atomicity.
The list's emission phase is still unproved; do not manually invoke it or
construct a collector based on registration alone.

Global captured Disrupt SHA256
`D8004145FB17BD6A9073466EBB9BFC19589AAD7D08D8EC3FD45733A5D8AD0855`,
base7FFC39BF0000, timestamp5CD045B4, image size6595000 only. All addresses are RVAs.

| Boundary | Role, inputs and ownership |
| --- | --- |
| 9FC8E0 / pointer slot2F5FA90 | `(environment, collector) -> void`. Adds selected strike/thunder resources and retains unrelated environment dependencies through collector virtual+120. Full159-byte body recovered. |
| 275DC0 | `(soundID, collector) -> void`. Ignores invalid ID; converts valid ID to resource key, obtains a typed CSoundResource reference through294D00, adds it through collector+118, then balances its temporary tagged reference. Full138-byte body recovered. This is the exact helper used by retail lightning. |
| 294D00 | `(resourceManager, taggedReferenceOut, key) -> taggedReferenceOut`. Looks up/creates via150D00/150BD0, verifies CSoundResource metadata, acquires a temporary reference and invokes virtual+10 for the tagged case. Not a read-only lookup. |
| Resource manager global3B593C0 | Engine-owned resource-object manager used by the native helper. Separate from audio payload registry3C0D030. Addons must not replace either singleton. |
| 292820 | Registers/returns CSoundResource type metadata; type token is at3B5C4A8. Called by native acquisition when needed. |
| 953140 | Other retail dependency visitor explicitly builds SoundBinary\\%08x.spk from numeric sound IDs, obtains typed resource objects and forwards to a collector. This corroborates file identity, not an alternative Addons loading entry. |
| 271BF0 | Native resource load path walks sound dependencies, opens the resource stream, reads its content and invokes virtual+100; balances the stream/buffer according to native results. Reentrant/native lifecycle method, not an arbitrary safe preload API. |
| 26BF80 | For a resource reporting loaded via virtual+58, clears a state bit and invokes virtual+108. Native unload/reset boundary; Addons does not call it directly. |
| 2B9700 / 2B9BB0 | Native audio lifecycle consumers enumerate CSoundResource objects and invoke unload/reload paths around broader audio-state transitions. Not narrow thunder-loading APIs. |
| A14280 | Constructs lightning settings including invalid default sound IDs and curve storage; does not establish storm audio resource ownership. |

The precise sound-ID hash helper implementation and broader native collector
internals need not be reproduced by Addons:275DC0 already performs the same
acquisition, collection and temporary release as retail. Protected/incomplete
decompilation in some unrelated resource callers is not callable-ABI proof.
In particular, incomplete138820 fallback output must not be treated as a safe
database preload operation. No such fallback is introduced.

# Internal v2.1.26 implementation

After the existing Global identity/storm gates, validates all159 callback bytes,
all138 native helper bytes and the original callback slot before mutation.
Compare/exchange replaces only slot2F5FA90. Protection restoration failure rolls
back that owned slot; forwarding storage remains resident for in-flight calls.
The pointer write is aligned, not thread-suspended initialization atomicity.

Original collection runs first with unchanged environment and collector. The
extension adds retail Storm A strike1B2CB and thunder1B2CA through275DC0 using the
same collector. It skips any ID already contributed by the selected record,
including retail's both-on-strike-valid gate. Unreadable selection fails closed.
No selected record, Moon scalar, scene selector or audio-ready byte is written.
The IDs match the inspected retail/TFoWC2 Storm A records; different authored
sound IDs in other mod configurations are not a validated compatibility claim.

The native collector owns retained dependencies and normal load/release. Addons
retains no resource object or reference, performs no manual bank parsing/load,
and calls no global audio restart. Stop disables future additions; existing
dependencies continue under the collector's native lifetime. Reload re-enables
addition. Collection logs cap at16, without stopping subsequent resource adds.
Original callback LastError is preserved. All modules stay in the single ASI.

The new actual-source harness checks code/slot gates, protection rollback,
foreign ownership, exact collector forwarding and original-first ordering,
Moon/record sentinels, native-ID deduplication, stop/resume, unreadable selection
and bounded logging. Captured-image checks independently verify both functions
and original slot. Runtime must show collection additions, resource resolution
and audible thunder while preserving moon shadows/tools. A ready hook or an
added-dependency log alone is not evidence that asynchronous loading completed.

The retained [execution observer](storm-sound-execution.md) distinguishes request
acceptance from resource failure. No duplicate sound submission or changed
scheduler timing is included. World/vehicle payloads and public releases remain
under the existing [profile contract](build-profiles.md).

# Internal v2.1.27 first-entry acquisition

The controlled26 reload proves audible playback once resources are collected.
27 also uses the existing Environment-owned container on first valid native
gameplay update, before the weather gate. It does not create a collector or
invoke the unproved callback-list emitter. Source and full captured bodies are
in v2.1.27-first-load-rear-20260905 and retail-thunder-loading-20260905/container-*.txt.

Captured Global mappings, statically confirmed. The .27 audible result does not
independently trace every mapped native branch:

| RVA / layout | Role, ownership and consumer |
| --- | --- |
| 15D7A0 | Subsystem base constructor embeds resource container at owner+8 and requests all three demand levels through its virtual+98. Environment consumes this base. |
| 15BAA0 / 15B9C0 | Container constructors; derived vtable2E59D00. Tagged native gate resource at container+C0 is allocated/owned by the container. |
| 156DF0 | Constructs the native gate resource, vtable2E59100, recording its container backpointer at gate+38. |
| 146080 / slot2E59E18 | Ten-byte virtual+118 forwarding thunk to virtual+120, preserving incoming resource argument. |
| 155140 / slot2E59E20 | Container add-child operation: deduplicates child parent-links, increments native ref, propagates each nonzero demand count at container+28/+2C/+30 via child+98, stores both link directions and updates readiness. Existing retail helper275DC0 consumes this interface. |
| 154D70 | Propagates readiness changes to native parents with reentrancy guard at resource+34. Called when adding a pending child makes the previously ready container pending. Not called directly by Addons. |

Install gates full forwarding/add bodies and original slots alongside26 gates.
The serialized update validates Environment and container vtables, gate type and
backpointer, and three positive bounded demand counters before calling275DC0
for1B2CB/1B2CA. Only identity tokens are retained by Addons. Native ownership
controls child load/release and readiness; no global reset or manual bank load.
Once transferred this native ownership is not rolled back by Addons. Normal
collection hook remains for later scene collections. Invalid objects fail closed.
Requests issue once per observed Environment/gate identity. Code preserves
LastError and does not write Moon/settings/selectors or enqueue duplicate playback.

Actual-source tests cover invalid type/backpointer/demand, disabled acquisition,
exact two IDs/container, repeat suppression and replacement owner. Offline
native/profile and full captured byte checks pass. firstEntryRequested is only
a loading request, not completion or audibility. At this candidate stage, first-process/first-load audibility remained untested; the preceding audible control was 26 after reload. Later 27 runtime feedback is recorded above.
