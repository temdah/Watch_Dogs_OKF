---
type: Diagnostic Boundary
title: World Batch Loader Timing Probe
description: Integrated Addons native loader observer, exact Global vtable mapping, bounded
  captures and unverified runtime scope.
tags:
- shadow-engine-addons
- cbatch
- loader
- diagnostic
- native
status: draft
sources:
- id: world-shadow-v214
  resource: ../../evidence/catalog.json#E-c47192e28e88
  title: Current unified build retaining this observer beside world-data enablement
- id: batch-v213
  resource: ../../evidence/catalog.json#E-5c4f1061d314
  title: Bounded serialized batch identification candidate
- id: runtime-v212
  resource: ../../evidence/catalog.json#E-039329308e68
  title: Global live loader timing, installed identity and diagnostic label limitation
- id: unified-build
  resource: ../../evidence/catalog.json#E-3753f6afc889
  title: Complete internal build, retained features and superseded companion
- id: build
  resource: ../../evidence/catalog.json#E-20dc105009c5
  title: Candidate, validation, limitations and manual handoff
- id: preflight
  resource: ../../evidence/catalog.json#E-395071e4c623
  title: Knowledge lookup and independent diagnostic scope
- id: native
  resource: ../../evidence/catalog.json#E-08b8ef96f0d7
  title: Process-lifetime vtable observer and copied-sample ownership
- id: corpus
  resource: ../../evidence/catalog.json#E-15a8c66e7ed1
  title: Saved Global image verification and other-profile rejection
- id: disassembly
  resource: ../../evidence/catalog.json#E-216975c5db02
  title: Batch-loader body and vtable/static data boundary
---

# Observer experiment

The loader observer is integrated into one complete internal build. **Addons v2.1.3-internal** continues the
observer in the same ASI, identity and menu as the atmosphere and bolt diagnostics.
DAT/FAT/NFO are byte-identical through v2.1.2; no additional database/world payload,
README or reference assets. Zero shadow/fade writes. Public Addons and Shadow
Engine are unchanged. The old separate World Light Probe v0.1.0 is a frozen
historical control, not the current install route. Disable it before v2.1.2;
both would own the same slot. Fresh process required.[^unified-build]

# Mapped boundary and identity

Static mapping belongs to captured Global image size `0x06595000`, timestamp
`0x5CD045B4`. Saved mapped image SHA256
`5F4259790890B52F3B05825572E93D3DB3932D3E470EA4BE8DB5DCB4E9E5ED6D`;
rebuilt PE/disassembly SHA256
`D8004145FB17BD6A9073466EBB9BFC19589AAD7D08D8EC3FD45733A5D8AD0855`.
The runtime guard uses header fields, three exact signatures and vtable pointers;
it is not a full live-image hash. All other four known corpus profiles are
deliberately inactive, not guessed compatible.[^corpus]

| Location | Role and boundary |
|---|---|
| Vtable `image+0x2EFE8E0`, slot `+0x20` | Pointer at `image+0x2EFE900` selects batch load `image+0x73E4E0`; atomically replaced only if still original. |
| Slot `image+0x2EFE8E8` | Adjacent type-accessor link to `image+0x759410`; additional ownership check. Type metadata `image+0x3B7AEA4` is `0xC58A3AB9`. |
| Loader `image+0x73E4E0..0x73E8BA` | Native processor/stream inputs; definition loader call then instance allocation/deserialization. Callback forwards both arguments and native integer-register return without changing loader data. |
| Stream `+0x28` | Serialized read cursor, observed before/after the native call. Native loader owns cursor advancement. |
| Processor `+0x30` | Definition input to `0x7C7F70`; shared settings then read through `0x259C960`. Existing caster/max/fade field mapping is in the batch concept; no shared-pointer mutation here. |

Vtable membership/signatures are confirmed statically, and v2.1.2 now confirms
live Global dispatch through this slot after bootstrap and manual checkpoints.
This does not establish every dispatch path or final renderer publication. Do not hook the generic shared loader globally
based on this limited batch-specific observer.[^disassembly]

# Ownership and behavior

NexusTools Lua autostart loads and pins the native DLL. Installation validates
before mutation, temporarily makes only the vtable page writable while preserving
execution permission, compare/exchanges one aligned pointer, restores protection,
and rolls back only its own pointer on failure. Failed restoration/ownership is
reported. There is no instruction detour or trampoline. Cross-mod coordination
outside this owned pointer is not established.[^native]

The native module owns eight append-only phase buffers, each capped at 64 samples.
Each producer atomically reserves one slot, copies a 64-byte input prefix and
scalar timing/cursor-distance evidence, then publishes completion. No retained
game pointer is subsequently dereferenced. After each phase fills, the hook only
counts/forwards calls. A single worker writes copies/counts every two seconds;
there is no loader-callback I/O, allocation, wait or VirtualQuery. LastError and
native argument/return behavior are preserved in the harness.[^native]

The unified host starts after existing Addons initialization pins the ASI.
One worker owns log output after startup, using `WorldLightProbe.log` beside
`ShadowEngineAddons.asi`; main native shutdown stops capture and requests worker
exit. Lua owns only its seven-request checkpoint count. No extra menu or watcher.

Menu checkpoint commands advance phases, not game state. Menu removal or script
unload stops capture; pinned forwarding code survives to process exit. Restart
to rearm after unloading. Already-running callbacks may finish after stop.
The small publication-to-activation window and all pre-bootstrap history are
unobserved. Zero calls do not prove early database loading; direct dispatch or
an unexercised path are also possible. Prefixes are not yet unique resource IDs
and may cross definition boundaries within a readable serialized buffer.

# Bounded batch-identification continuation

v2.1.3 retains the exact Global vtable/signature hook and extends reserved
samples with at most4,096 bytes from the cursor interval consumed by the native
call. Copy is post-call but synchronous, bounded to measured consumption, and
publishes no partial bytes on read failure. A pre-call64-byte prefix comparison
flags a changed interval. Each immutable copy is emitted in128-byte hex chunks
by the sole worker; no game pointer reaches it. The existing8x64 cap bounds
storage at2MiB and a fully populated log near5.5MiB. No data/fade/shadow write.

This advances content correlation, not ownership. The private parser accepts
only the newest v2.1.3 appended session, rejects corrupt/order/bounds errors and
allows exact matching only for complete, prefix-stable copies against independently
hash-verified audited cbatch spans. Duplicate content is ambiguous. Truncated,
changed, failed and unmatched samples are ineligible. Even a unique content
match identifies serialized batch content and owning static resource; it does
not prove a live pointer lifetime, renderer admission, physical fixture identity
or underground clearance.[^batch-v213]

v2.1.3 also replaces return-value uses of TinyCC `InterlockedIncrement` with one
saturating compare/exchange serial helper. World ordinals are exact under4,000
concurrent calls and atmosphere IDs are exact across sequential captures. Calls
whose return value is ignored retain ordinary atomic increments. The compiler
headers are untouched.[^batch-v213]

# Validation and continuation

Offline native/Lua/corpus/rebuild/package gates passed. The first unified Global
runtime review now confirms installed package identity and successful AddTrace,
atmosphere and world-loader installation. Counts by phase are1,355 /287 /54,
all completed; phases1/2 start at27,844/80,453ms. Captured182 prefixes with zero
prefix/cursor read failures; first at141ms and last at98,266ms. There are341
calls after manual checkpoints. The batch loader remains reachable during the
travel session after Addons initialization, so early bootstrap is not a blocker
for this observed path. These are load calls, not unique lights/resources.
Other profiles, complete coverage, renderer publication and mutation safety
remain unverified. Runtime feedback reported completion only; no broad visual acceptance.
Missing stop marker does not classify a crash.[^runtime-v212]

**Known diagnostic label defect:** every saved sample has call=1. The bundled
TinyCC InterlockedIncrement implementation updates storage correctly but returns
sign/zero, so return-based ordinals are invalid. The minimal reproduction confirms
stored3 versus returns1/1/1. Reservation, phase totals and copied samples remain
usable; do not use call labels as identities. A compare/exchange-loop reproduction
returns exact ordinals; InterlockedExchangeAdd did not link in this toolchain.
The existing atmosphere capture_serial has the same return-value dependency
(static risk, not exercised by this run). Fix serial consumers and assert exact
values before the next unified candidate; tested source/ZIP remain unchanged.

v2.1.4 retains this observer unchanged but does not use it as the enablement
mechanism. The implementation selected independently rebuilt retail world data for the initial
enable-all candidate, plus a separate aimed-endpoint marker for later exclusions.
The observer still supplies bounded loader research only; it proves neither
renderer publication nor marker-to-light identity. Fade tuning remains a
separate experiment.[^world-shadow-v214]

[^build]: Full candidate handoff, hashes and verification limitations
[^preflight]: Required knowledge-first inspection and preserved prior logs
[^native]: Actual observer source, publication and lifetime boundary
[^corpus]: Global static validation; all other profiles inactive
[^disassembly]: Saved native load body and vtable references

[^unified-build]: Current v2.1.2 complete internal package and offline integration validation

[^runtime-v212]: Preserved runtime evidence, timing totals and independent counter-return reproduction

[^batch-v213]: v2.1.3 mechanism, exact serial correction, offline tests and limits
[^world-shadow-v214]: Current unified data payload and anomaly-marker build retaining the observer
