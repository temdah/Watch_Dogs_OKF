---
type: Engine Subsystem
title: Storm Sound Command Execution and Resource Resolution
description: Captured Global command-result boundary, resource rejection paths and bounded internal
  observation.
tags:
- shadow-engine-addons
- thunder
- audio
- resources
- diagnostics
status: draft
sources:
- id: public-storm-promotion
  resource: public-storm-runtime.md
  title: Separating a storm hook host from optional observers
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
- id: preflight
  resource: ../../evidence/catalog.json#E-5345c96e1d34
  title: Active knowledge and provenance lookup
- id: executor
  resource: ../../evidence/catalog.json#E-0e1e812b8be8
  title: Full native command virtual executor
- id: dispatch
  resource: ../../evidence/catalog.json#E-4bd991f5ab9b
  title: Immediate or queued command dispatch and handle allocation
- id: execution
  resource: ../../evidence/catalog.json#E-ee860f28accb
  title: Native execution gate and result propagation
- id: resources
  resource: ../../evidence/catalog.json#E-c4404a3cccc3
  title: Resource presence/type checks and delayed or immediate event execution
- id: lookup
  resource: ../../evidence/catalog.json#E-847f3a205ff8
  title: Locked reference acquisition
- id: node
  resource: ../../evidence/catalog.json#E-b8b00b33409c
  title: Bucket search and missing-node allocation
- id: media
  resource: ../../evidence/catalog.json#E-e068a83904cf
  title: Extracted retail sound package identities and byte observations
- id: source
  resource: ../../evidence/catalog.json#E-491c1a4a77d0
  title: Bounded command-result observer
- id: submission
  resource: storm-thunder-audio.md
  title: Storm Thunder Audio Submission
---

# Scope and experiment outcome

These mappings distinguish storm scheduling, accepted audio requests,
resource resolution and audible playback. The complete failed controls
and successful resource-collection experiment are recorded in
[storm audio loading](storm-audio-loading.md). The .27 runtime report
accepted thunder, flashes and retained moon shadows; the later
[host/observer separation](public-storm-runtime.md) has separate offline evidence.

# Evidence and diagnosis boundary
The .24 runtime submitted13 thunder events with valid handles, but no thunder was reported audible. Static analysis now proves that those handles precede the resource and
event execution checks. The25 runtime now confirms missing-resource rejection; the later live/resource-loading investigation identifies the absent root and
missing dependency phase; see [retail loading](storm-audio-loading.md). TFoWC2's selected Moon record remains untouched.
Mappings below apply only to the captured Global image SHA256
`D8004145FB17BD6A9073466EBB9BFC19589AAD7D08D8EC3FD45733A5D8AD0855`,
base `7FFC39BF0000`, timestamp `5CD045B4`, image size `6595000`.
VAs are preserved where the source exports use them; subtract this base for RVA.
| Address/boundary | Confirmed static role and limits |
| --- | --- |
| VA7FFC3BF1A4E0 | Command allocation path obtains/stores a handle before execution. A valid submission handle is not a voice or resource result. |
| RVA234E400 | Command dispatcher queues when manager+402B8 equals1; otherwise invokes command virtual+48. Immediate dispatch status cannot substitute for queued execution status. |
| Vtable RVA31D7AD0, slot31D7B18 ->232A010 | SendSoundRequestCommand executor ABI `(command, uint32_t *statusOut) -> pointer`. Full37-byte body forwards command+1C event ID, command+20 parameters, command+18 handle to23CA920, then returns statusOut. |
| RVA23CA920 | Initializes status80000001; requires a nonzero native engine state and matching first parameter token in the native global range before resource dispatch. Returns the downstream status and performs native tracking/cleanup. Exact state/token semantic names remain unresolved. |
| VA7FFC3BF5E4A0 / RVA236E4A0 | Acquires the sound resource. Missing wrapper/payload yields8000E002; a payload with wrapper type nibble other than10000000 yields8000E003. Otherwise dispatches immediately or queues authored delay. These are observed code conditions, not official error names. |
| VA7FFC3BF29410 | Derives authored/randomized timing used for delayed scheduling. This field must not be treated as volume. |
| VA7FFC3BF5DD40 | Further event-kind/condition paths and voice-construction dispatch. Missing resource can also return8000E002; unsupported event kind returns8000E004. Other failures and later voice/mixer outcomes remain possible. |
| VA7FFC3BFE9070 ->7FFC3BFC3490 | Acquires a resource wrapper under a native manager lock and increments its reference count. Not a read-only availability API. |
| VA7FFC3BFC1C90 / RVA23D1C90 | Searches a low-ID-byte bucket of16-byte entries; on absence it allocates and inserts an empty resource node. Never call this as a harmless resource probe. |
Native resource wrappers, commands, delayed work, handles and voices retain
engine ownership. Addons must not retain their pointers, construct replacements,
force readiness, load/unload guessed banks or alter reference counts. Status0
at this executor can mean a delayed event was queued; it does not prove a mixed
or audible voice. Error results must be interpreted against this captured build.
# Live lookup mapping and validation
Global manager pointer at RVA3C0D030 owns256 ID-low-byte buckets. Bucket
manager+8+24*(id&FF) has capacity0, entry begin8, end10 (hex offsets). Each16-byte
entry contains uint32 ID0 and node pointer8. A node begins with payload pointer0,
ID8 and type/flagsC; native acquired-reference count is at10.23D1C90 searches and
allocates missing nodes;23D3490 takes a native lock and acquires a reference.
These remain native-owned mutation boundaries, never callable read-only probes.
The external inspector uses only process query/read rights, full Global PE gate,
four32-byte native signatures, bounded copies and repeated-read agreement. It
retains no pointer for later runtime mutation, acquires no native reference and
calls no game function. Snapshot agreement is not engine-lock atomicity. Its
fixtures reject changing headers/oversized buckets and identify absent roots and
exact missing child IDs; live controls confirm the decoder finds resident nodes.
Native type2 constructor235BD40 assigns vtable31D9C60; virtual+8 ->236F700 walks
16-byte child references at event payload+A8, count+A0. Missing child payloads
can propagate8000E002, explaining the earlier status ambiguity. The live top-level
CA node is absent, so no child walk is needed to explain the current failure.
Owner-function exports follow chained PE unwind records; raw fragment starts
must not be treated as complete ABIs. These are captured Global-only mappings.
The two live snapshots in the captured process find all32 package header IDs absent, while
same-bucket controls1531CA,231CA and240CA have payloads. Thunder's on-disk file is
soundbinary/0001b2ca.spk; associated1B2C8 is also absent from resident resources.
The exact archive audit establishes no matching path hashes in TFoWC2 or other
inspected packs, not the absence of every indirect loading effect. Next recover
normal native preload/registration and release for this sound family; do not
replace Moon or force audio-ready bytes. See the linked live RESULT for evidence.
# Retail package evidence
Read-only extraction from retail `data_win64/worlds/windy_city/windy_city.fat`
finds soundbinary/0001b2ca.spk (thunder) and0001b2cb.spk (strike), each132 bytes.
Their final serialized IDs are1B2C8 and1B2C9; corresponding packages are present.
1B2C8 is1,850,884 bytes with28 header IDs and an OggS marker at offset2420.
This proves the files exist and contain an audio-container marker; it does not
prove those resources are loaded, decoded, non-silent or routed in the observed session.
The trailing ID relationship is a dependency lead, pending full serialization/
loader mapping. No volume gain or loading fix follows from these bytes alone.
Raw extracted Ubisoft files stay private evidence and are excluded from builds.
# Internal v2.1.25 observation
The optional observer validates the complete37-byte executor and original vtable
slot after the existing Global storm gate. A compare/exchange replaces only its
own slot; failed protection restoration rolls that slot back. Forwarding state
stays process-resident for in-flight calls. Foreign slot ownership is refused.
This is aligned pointer replacement, not thread-suspended installation atomicity.
Every call forwards its original two arguments exactly once and preserves the
return pointer and LastError. Only event1B2CA/1B2CB commands reserve one of64
slots. Each executing thread copies event and handle before native execution,
then status after return, and atomically publishes the copied record. No worker
performs log I/O. The serialized private scheduler flushes completed records.
Slots are never reused; exhaustion stops capture while playback continues.
The observer includes native storm commands too: join event/handle with the
scoped STORM_SOUND_EVENT log before attributing a result to Addons. It deliberately
does not depend on scheduler TLS remaining active during asynchronous execution.
Missing results may reflect capture limits, no execution, or no subsequent
scheduler flush; missing markers alone are not a failure classification.
The actual-source harness checks signature/slot/protection failures, unchanged
arguments/return/LastError, preserved pre-execution identity, failure/success
results, foreign silence and four concurrent workers beyond the64-record limit.
Captured-image gates verify the whole executor and its downstream call target.
Runtime25 confirms15 resource failures; audible restoration remains unfulfilled.
