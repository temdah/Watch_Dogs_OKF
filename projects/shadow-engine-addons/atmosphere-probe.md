---
type: Diagnostic Boundary
title: Bounded Atmosphere Snapshot Probe
description: Internal v2.1.1 read-only game-data capture, exact native layouts, ownership, and
  unresolved runtime limits.
tags:
- shadow-engine-addons
- atmosphere
- diagnostic
- lightning
- sky
status: draft
sources:
- id: storm-dispatch
  resource: basic-lightning.md
  title: Basic Storm Lightning and Moon-Shadow Separation
- id: serial-v213
  resource: ../../evidence/catalog.json#E-5c4f1061d314
  title: Shared exact diagnostic serial correction
- id: build
  resource: ../../evidence/catalog.json#E-69f4e9024e55
  title: Candidate scope and offline verification
- id: preflight
  resource: ../../evidence/catalog.json#E-4992769d7fd2
  title: Knowledge preflight and preserved control
- id: disassembly
  resource: ../../evidence/catalog.json#E-42bb87648dce
  title: Native scheduler and compiled curve evaluation
- id: lookup
  resource: ../../evidence/catalog.json#E-b68f5b4ff27d
  title: Record constructor and loaded lookup evidence
- id: probe
  resource: ../../evidence/catalog.json#E-7b93a7232d8b
  title: Signature-gated sky observer
- id: reader
  resource: ../../evidence/catalog.json#E-fcf75efe1c81
  title: Bounded loaded-table reader
---

# Scope and evidence tier

v2.1.22 retains the observer and its requested snapshots. Its single sky hook
now dispatches the optional [storm sidecar](basic-lightning.md) around the native
sky call, then captures as before. Snapshot code remains read-only; the separate
storm module owns the RGB contribution and native audio. The old observer-only
installation marker describes the probe itself, not the entire Addons runtime.
The .21 run captured loaded Moon/Storm settings. Later storm runtime
results belong to [the scheduler investigation](basic-lightning.md); they do not
automatically validate every optional capture path.

v2.1.1 is an internal observer candidate, not basic-lightning restoration or
flare alignment. Native layouts below were recovered statically from captured
`Disrupt_b64_runtime_rebuilt.dll`, SHA256
`D8004145FB17BD6A9073466EBB9BFC19589AAD7D08D8EC3FD45733A5D8AD0855`,
image size `0x6595000`. No multi-region or live layout validation is claimed.
Four function-byte signatures gate installation; they are not a whole-image
identity check. Fixture tests prove bounded reader/control behavior, not game
compatibility. Fixture success alone establishes no visual result.[^build]

# Confirmed static mappings

| Location | Semantic role / consumer |
|---|---|
| Image + `0xA53860` | Sky orchestrator `(environment, float dt, float weatherBlend)`; publishes internally before returning. Probe calls original first, then reads only when requested. |
| Image + `0xA89600` | Typed lightning resolver; passes type/key to loaded lookup, with unresolved fallback. Never called by probe. |
| Image + `0x132A20` | Loaded-library/key lookup whose explicit bucket layout is reproduced read-only. Never called by probe. |
| Image + `0x3B59050`, `0x362B63C` | Database manager pointer and lightning library type ID, respectively. |
| Manager + `0x58`, `0x60` | Library bucket count and pointer. Library node next/type at `+0/+8`; loaded state `+0x20 == 1`; record bucket count/pointer at `+0x50/+0x58`. |
| Record node + `0/+8/+0x10` | Next node, key, borrowed record pointer. Only exact Storm A `0x75637933` and Moon `0x302E09E1` keys requested. |
| Lightning record `0x88` bytes | Constructor `0xA14280`; vtable image + `0x2F520C0`, type ID `+0x10`, curve pointer/count `+0x60/+0x68`. Probe verifies type/vtable before decoding. |
| Curve evaluator `0x498530` | Native knots stride `0x20` bytes. Capture logs all eight raw words per knot; XML knots must not be assumed to be native-layout bytes. |
| Environment + `0x290/+0x298` | Selected sky triple array/count; each `0x18` triple has cloud record, time step, context pointers. |
| Environment + `0x498/+0x4A0/+0x4A8` | Selected lightning record, native state pointer, sound-enabled byte; probe reads record and flag, never schedules the state. |
| Cloud record `0xC0` bytes | Crossfade values `+0x30/+0x34`, sun bias `+0x78/+0x7C/+0x80`; `+0x14/+0x18` keys retained as raw labels. Time step is `0xA8` bytes, first word hour; remaining words logged raw. |

These fields support observation of settings/selection; they do not prove the
final sun projection, renderer flare direction or safe mutable record lifetime.
The mutating cloud-key setter `0x1E1C800` remains prohibited for observation.
See [basic lightning](basic-lightning.md) and [alignment](sun-flare-alignment.md).

# Ownership and safety limits

`atmosphere_probe.c` owns process-lifetime hook/trampoline state and atomic
pending/capturing flags. Lua requests one capture; repeated pending requests
coalesce. Idle calls forward to original with no game-data snapshot or logging.
Shutdown cancels a pending request, but cannot abort a capture already running.
The DLL is pinned because installed detours outlive menus. No hot-unload of
native code is claimed.

All probe game-data reads use `ReadProcessMemory`; addresses exist only during
the callback. The reader walks registered tables, never an arbitrary heap scan.
Caps are 4096 buckets, 512 library nodes, 1024 record nodes per lookup, 16 native
knots and 16 sky entries. Unreadable, changed, absent and over-limit inputs are
reported without loader fallback. Table headers are rechecked; captures are
still not atomic snapshots and may miss concurrent changes or address reuse.
Do not use a diagnostic address as permission for later engine writes.

Installation validates four byte signatures before changing code, creates a
trampoline and rolls back target bytes if protection restoration fails. Once
a jump was published its trampoline is retained for possible in-flight calls.
The detour publication is not a thread-suspending atomic patch transaction;
live installation/concurrent execution still requires runtime validation.
No engine database or lighting data is written, but installation does patch
code. Capture performs synchronous bounded file I/O on the callback thread;
a brief requested-capture hitch is possible and has not been measured in game.

# Output and interpretation

Markers: `ATM_INSTALL`, `ATM_CAPTURE_BEGIN/END`, `ATM_LOOKUP`, `ATM_RECORD`,
`ATM_KNOT`, `ATM_SKY_ENTRY`, `ATM_SKY_STEP`. `CAPTURE_COMPLETE` means the request
was processed, not that every record was readable or that a visual feature was
restored. Check per-record results. Multiple modules trying to own the same sky detour can conflict;
observer and storm ownership must be coordinated.

[^build]: v2.1.1 internal build report

# v2.1.3 diagnostic serial correction

The bundled TinyCC `InterlockedIncrement` updates storage but returns sign/zero;
v2.1.1 used that return for `ATM_CAPTURE_BEGIN id`. v2.1.3 uses the shared
saturating CAS serial helper. Actual-hook tests now request two captures and
require IDs1 then2 while retaining read-only data and coalescing behavior. The
v2.1.2 Global run requested no atmosphere capture, so this corrects a statically
confirmed diagnostic risk rather than reclassifying runtime atmosphere behavior.[^serial-v213]

[^serial-v213]: v2.1.3 exact repeated serial tests and unchanged atmosphere mechanism
