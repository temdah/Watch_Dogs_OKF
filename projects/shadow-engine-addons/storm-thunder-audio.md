---
type: Engine Subsystem
title: Storm Thunder Audio Submission
description: Retail and installed TFoWC2 comparison, captured native sound submission ownership,
  and missing-thunder investigation limits.
tags:
- shadow-engine-addons
- lightning
- thunder
- audio
- tfowc2
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
- id: v225-candidate
  resource: ../../evidence/catalog.json#E-7eb2f33e9233
  title: Native command-result observer and retained package audit
- id: v224-runtime
  resource: ../../evidence/catalog.json#E-c380e3b89fba
  title: Thirteen accepted native thunder requests, explicitly inaudible
- id: v224-candidate
  resource: ../../evidence/catalog.json#E-2cb595ca312e
  title: Scoped native thunder trace and retained profile validation
- id: trace-source
  resource: ../../evidence/catalog.json#E-557824e0255f
  title: Guarded vtable observer and private pulse summaries
- id: v223-runtime
  resource: ../../evidence/catalog.json#E-45a8263d9818
  title: Missing thunder after stage restoration and exact readiness predicate
- id: v223-candidate
  resource: ../../evidence/catalog.json#E-1a8bb05ece30
  title: Native update stage candidate with private output and offline verification
- id: legacy-hook
  resource: ../../evidence/catalog.json#E-c32dd8c89293
  title: Preserved v1.0.7 scheduler call and output restoration
- id: legacy-acceptance
  resource: ../../evidence/catalog.json#E-248f854f86b5
  title: reported synchronized-thunder report and archived binary identity
- id: override-audit
  resource: ../../evidence/catalog.json#E-dfb767e4800d
  title: Fresh installed TFoWC2 and retail record comparison and native trace
- id: getter
  resource: ../../evidence/catalog.json#E-78bcd3dd9f62
  title: Native audio singleton getter
- id: lifetime
  resource: ../../evidence/catalog.json#E-9171625dfee3
  title: Singleton allocation and retirement writers
- id: constructor
  resource: ../../evidence/catalog.json#E-6fafefaba016
  title: Audio interface constructor and vtable assignment
- id: dispatch
  resource: ../../evidence/catalog.json#E-f8213bf74b9d
  title: Native sound request guards and returned handle
- id: send
  resource: ../../evidence/catalog.json#E-90906db52d5e
  title: SND_SendSoundEvent command producer and unmapped readiness lead
- id: sidecar
  resource: basic-lightning.md
  title: Basic Storm Lightning and Moon-Shadow Separation
---

# Scope and experiment outcome

These mappings distinguish storm scheduling, accepted audio requests,
resource resolution and audible playback. The complete failed controls
and successful resource-collection experiment are recorded in
[storm audio loading](storm-audio-loading.md). The .27 runtime report
accepted thunder, flashes and retained moon shadows; the later
[host/observer separation](public-storm-runtime.md) has separate offline evidence.

# Submission versus playback

The .22 and .23 experiments produced visuals but inaudible thunder. Restoring
native-update scheduling alone was insufficient. In .24, thirteen event
`0001B2CA` requests returned distinct valid handles with readiness flags 1/1.
All 39 pulse summaries had valid data and the expected audio vtable; each pulse
submitted once about 0.517–0.864 seconds after creation. Capture limits were not
exhausted. This excludes early rejection for those requests, not downstream
resource failure. The .25 [execution observer](storm-sound-execution.md) then
recorded `8000E002` failures; the loading concept owns the eventual diagnosis.

Serialized Storm A/B fields and curves in the inspected TFoWC2 archives matched
retail completely. Moon.Shadows was silent and remained selected for moonlight.
No named audio/bank replacement appeared in those four archive inventories.
This does not identify every indirect interaction or establish TFoWC2 as a cause.

# Captured native boundaries
Static mapping only, for Global Disrupt image SHA256
`D8004145FB17BD6A9073466EBB9BFC19589AAD7D08D8EC3FD45733A5D8AD0855`,
captured base7FFC39BF0000. These are not portable mappings. Only the guarded
slot described below is used by the .24 internal diagnostic.
| RVA / boundary | Role, ownership and limits |
| --- | --- |
| 2B7DC0 / global3B5C828 | Returns the borrowed engine-owned audio singleton. Addons must not construct, replace, retain or free it. |
| 2BBEC0 / 2BB0E0 / 2BBF10 | Allocate910-byte object, construct with vtable2E70840, then native teardown/free and clear global. Captured ownership only; no live lifetime observer. |
| 9F5D80 | Private pulse/time/IDs/threshold inputs; waits for deadline, chooses strike above threshold or thunder otherwise, then marks handled. Its sound-result handle is ignored, so handled does not prove acceptance. |
| Vtable2E70840 +100 -> 2BBFE0 | EventFFFFFFFF returns an invalid output handle; otherwise forwards to2BB480. Result is written through an output pointer. |
| 2BBFE0 six-argument ABI | Self, output-handle pointer, event ID, emitter, float parameter5, uint32 parameter6; returns a pointer. Complete64-byte body verifies both stack arguments. Parameter semantics beyond the native zero defaults are not inferred. |
| 2BB480 | Rejects invalid event or failed virtual+40 readiness; returnsFFFFFFFF on those paths. Builds native sound parameters and returns the downstream handle. Null emitter used by thunder bypasses its optional spatial-owner/distance checks. |
| 23BE190 | Builds the named SND_SendSoundEvent command from event ID and parameters, then dispatches to native sound machinery. Submission is not bank availability or audible mixing proof. |
Readiness slot+40 resolves to2BC560. Exact captured bytes now establish a true
return only when both native-owned bytes self+14 and self+17 are nonzero.
Their semantic names/writers remain unknown; .24 sampled both flags as1. This does not
establish a mute or thread gate. Do not force readiness, mixer, weather or
audio-lifetime state. Preserve native ownership and ordinary calls.
# Internal v2.1.24 observation contract
After the existing Global storm identity gate, the optional trace validates
all64 submit bytes,18 readiness bytes, and original submit/readiness vtable
slots. It atomically replaces only slot2E70940 with a forwarding observer.
Compare/exchange refuses foreign ownership; tested protection failures restore
the owned slot. Callback/TLS lifetime remains process-resident for in-flight
calls; shutdown has no active scheduler scope and foreign calls forward silently.
It never replaces/retains the audio singleton or forces either readiness flag.
All six arguments, native return and LastError are preserved. Only a TLS scope
around Addons' serialized private scheduler collects matching authored event IDs
with a null emitter. Native calls execute exactly once. At most64 event lines
record sampled readiness flags and the returned handle; accepted means readable
and notFFFFFFFF at this interface, not guaranteed audible mixing or bank lookup.
Other sounds remain unobserved; no fabricated delayed or forced playback call.
At most96 pulse-transition/retirement lines copy the private vector before/after
scheduling. They record clock, pending/deadline/due counts, event-call count and
sampled singleton readability/vtable identity/flags. This detects retirement
before a deadline and exposes coverage gaps if the native audio object differs.
Tokens/pointers are not retained for later dereference. Fixed .23 log lifetime
is retained. After capture limits, native playback continues without diagnostic
copies. Offline tests cover forwarding, acceptance/rejection, invalid vectors,
limits and rollback; the .24 runtime report is inaudible as recorded above.
# Diagnostic boundary
The 2026-09-05 comparison against the preserved v1.0.7 binary takes priority
over adding speculative audio hooks. Its SHA256 was rechecked as
82761EC3C600115F17E9BF7867523D1563ED7644A005F0C1BE061352700E23D1.
The recovered hook10002242 calls the original selected-lightning update first,
then advances the private Storm A scheduler using that update's delta and
environment sound byte+4A8. It saves/restores the shared output scalar+364 and
retains storm intensity separately for sky contribution. v2.1.22 instead
advances the scheduler inside sky publication using the sky callback's delta,
and writes the scalar exclusively into private output. Both use native timing,
Storm A sound IDs and the environment sound byte; neither uses Lua PlaySound.
The old decompilation has incomplete branches, so this comparison is scoped to
the recovered call path, not complete binary equivalence or proven thread identity.
v2.1.23 implements scheduling after native lightning update A2F7E0, retaining
private output, validated owned settings and sky RGB contribution. Captured
Global callsites A6080B and A6081D establish lightning-before-sky order and the
same XMM9 delta. The update takes its own dt, original weather input and native
enabled byte, forwards all arguments first, then advances the private scheduler.
Sky consumes only copied result/settings and records copied weather/context
identity for the following update. One-second freshness and serialized pulse
retirement guard the boundary. This stage difference is confirmed structurally;
its role in missing thunder is unproven. Old shared scalar writes, raw-memory
scanner and manual button remain excluded. Offline gates pass; the .23 audio report confirms thunder is still inaudible. Other detailed visual gates remain open.
The sequence demonstrates why input markers and a valid early handle cannot
establish successful playback. Pulse progression, returned handles, downstream
command status, loaded resources and audible results answer different questions.
