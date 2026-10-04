---
type: Host Callback Contract
title: Shadow Engine Menu Host Compatibility
description: Verified installed-host slider and queued callback roles behind the .77 menu correction.
tags:
- shadow-engine
- nexustools
- lua
- callbacks
- settings
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-shadow-a4ee-menu-crash-20261004
  title: Two A4EE null-pointer Lua VM crashes after menu registration marker
- resource: ../../../evidence/catalog.json#E-shadow-tools-frame-20261004
  title: Observed menu startup rejection and reproduced Lua frame-budget violation
- resource: ../../../evidence/catalog.json#E-9cb07d147454
  title: Script property storage, dummy getters and native scheduling evidence
- resource: ../../../evidence/catalog.json#E-3f4aab0a475b
  title: Reproducible integer-command binding and callback inspection
- resource: ../../../evidence/catalog.json#E-607e1cac8a83
  title: Queued callback binding, drain order and mutex lifetime proof
- resource: ../../../evidence/catalog.json#E-523c4f1bacfd
  title: Strict host-aware menu fixture with delayed callbacks and save failures
- resource: ../../../evidence/catalog.json#E-048959912eaa
  title: Offline full-prototype register budget with target-runtime limits
- resource: saved-settings.md
  title: Persisting mod policy without blocking native callbacks
- resource: lua-stack-compatibility.md
  title: WD1 Lua Packed Frame Size and Garbage Collection
---

# Runtime identity and evidence level

The read-only inspection covers the inspected NexusTools host image, 15,337,984 bytes,
SHA256 `8120389BA4D144DC465E9FED2648B5690A6BBF0CDF5B052EF6EE3B738BE5DCFC`,
PE timestamp `6A82F9AC`, preferred image base `180000000`. Windows file/product
version metadata is empty. Addresses below are RVAs for this exact host only,
not game-profile mappings. Inspection did not load, execute or modify the host.
The evidence notes link reproducible scripts and bounded disassembly.

The .76 Global status proves downstream/profile 2 and quality readiness 1,
while the screenshot shows the untouched initial reading message. This confirms
failed menu synchronization, not the exact value of each host scheduling predicate.
That engine completed startup; a separate .71 timeout is separately owned
by [startup supervision](startup-supervision.md).

# Verified roles and consumers

| Boundary | Role, inputs and outputs | Ownership and consumer |
| --- | --- | --- |
| Script constructor `11B790`; setter `11BF70` | Assignments store Lua registry references: OnLoad+4C, OnUpdate+50, OnRender+54, InitCallbacks+58, OnUnload+5C | Native Script retains references; cleanup `FBF70` releases them |
| Script getter `11BD70`, dummy `11C870` | Callback property reads return a zero-result placeholder | Calling `script:OnUpdate()` in a plain-table fixture did not model host dispatch |
| Script manager `FC700` | Invokes the stored OnUpdate reference; requires state 0 and a game/time scheduling flag | Missing OnLoad falls through to OnUpdate check `FCEEB`; OnLoad is not a prerequisite. No automatic OnRender dispatcher was proved |
| RegisterInt `102010` | Eight args: id, label, description, menu, default, min, max, callback | Constructs type 9 command. Shadow tools retain its unique ID and Script owner |
| SetStateInt `105D20`; setter `107960` | Two args: command ID and integer. Writes command+94; no third silent flag; zero Lua results | Type 9 command lookup required. Caller validates 0..10. `pcall` success, not a nonnil result, proves submission |
| Setter callback `107D70`; dispatcher `349F0` | Calls registered Lua callback with no new-value argument, even for equal values | Callback reads current GetStateInt. Matching host thread runs inline; other context queues through `3B360/3B400` |
| NextTick `A11E0` | Function plus optional integer delay, minimum/default 1; registry-retained closure; zero Lua results | Forces queue through `349F0`; one-shot callback, not a periodic Script registration |
| Queue `C580E8`; drain `3B530` | Callsite `1B7E5C` precedes Script manager call `1B7E9B` | Independent of the later Script pause/game gate; unresolved outer host-loop gate `1B7E2B` still applies |
| Delayed deque and mutex | Positive delays park until a future drain; constructor `31A7F` selects reentrant mutex mode via `3B1AE0` | Queuing one successor inside a callback neither recursively executes it in that drain nor deadlocks on the same-owner mutex |

# Implemented scope and safety limits

.77 restores the limiter slider with observed-value echo suppression that survives
delayed callbacks. Before hydration it samples an unobserved user drag so an
older save result cannot overwrite the latest choice. First hydration and session
change deliberately discard widget defaults and old-session intent. Failed setter
calls retain the actual-widget observation baseline. No default save is emitted.

Immediate registration/page/action reads share protected status polling with one
loaded-owner NextTick chain, delay 30 host drains. It contributes 30 toward the 60
tick fallback, avoiding single-precision wall-clock quantization stalls. Script
OnUpdate is fallback only when queue submission is unavailable. Unload makes old
callbacks expire without a successor. The delay is not a millisecond promise;
neither pre-world execution nor execution while the host loop stops is proved.

The native settings owner alone persists/applies valid policy. Lua holds scalar
desired/in-flight state and UI roots, never engine pointers. The strict fixture
passes 445 checks including paused Script dispatch, inline/deferred setter and
user callbacks, old save success/failure, session reset, missing APIs and unload.
Offline Lua 5.1-derived compilation inspects 57 prototypes, maximum 25 registers.
That stays under 31 but does not certify the captured modified target compiler.
The existing Global 17-site Lua repair is unchanged; Complete Edition remains
unsupported for that separate repair. The .77 host investigation preceded later acceptance of the .78 menu. Static scheduling proof and offline register checks remain narrower than complete target-host/runtime validation.

The accepted .78 UI removed static active/default labels and uses a single fresh-settings notification. The callback and hydration boundaries here remain applicable; the historical .77 interface is not a requirement to restore stale labels. Experimental .80 extends only the current settings protocol/control semantics, with its own runtime gate.

# Module-root frame regression and required independent checks

The .92 Global session reached native rendering with the user reporting stable
gameplay, but the tools failed before menu registration. NexusTools recorded an
attempt to call the `tool` table as an upvalue at the first `stage` call inside
registration. The installed ASI matched the candidate and its log recorded the
Global Lua repair active. Neither fact establishes correct Lua chunk execution.
The exact corruption path was not captured; this error is not proof of one
particular GC event or native writer.

Offline compilation independently reproduces an existing-contract violation:
the entrypoint root needs 34 registers and the settings field-list constructor
needs 35. Desktop behavior tests passed despite both exceeding the documented
31-register ceiling. The automatic builder omitted that independent gate, so
its earlier successful tests did not establish frame safety.

The corrective source stores selected presentation helpers on the existing
owned tool object, scopes path data inside its reader and constructs the status
field list incrementally. All 78 prototypes then fit within 29 registers, with
the same 728 host-aware menu assertions passing. Native hooks, policy and ASI
bytes are unchanged. The inspector is pinned as a local build input; the
mandatory `lua-register-budget` step scans every shipped Lua file and inspects
all child prototypes as well as roots. Missing or failed gates prevent automatic
qualification. This bound must hold on profiles without the Global-only repair.

The corrected menu failed subsequent A4EE startup verification, as detailed below. Renaming its folder,
manifest identity, autostart path, virtual Lua namespace and displayed name is
a separate installation migration; enablement must refer to the new identity
and the previous installation must not run alongside it.

# A4EE startup failure despite the offline register bound

Two runs of the A4EE signed variant (DLL SHA256
`a4eead7a645ab4340a67622da4bfc91789e8cecfd53f605499a0e4b09b3ee60a`,
PE timestamp `5CD13864`) with ASI 2.0.92 and tools 2.0.93 failed at
`Disrupt_b64.dll+004D7561`. Both exception records prove a read access violation
`C0000005` at address `10`, with `RCX=0` and `RDI=1`. Captured fault bytes decode
to `mov rdx,[rcx+10]`. In the matching preserved A4EE image, preceding instructions
load the current closure from `[rsp+40]`, then its indexed pointer at
`[closure+rdi*8+28]`. This is statically consistent with the Lua GETUPVAL path
dereferencing a null upvalue object at index 1; it does not identify the writer
that invalidated that object.

The latest NexusTools log ends after the tools' register-menu marker. Native
shadow patch preflight and downstream installation completed, while the optional
Lua frame repair explicitly remained unsupported on this profile. The last
resident-work snapshot contains no populated shadow entries. These facts locate
the observed failure during Lua startup; they neither certify native rendering
nor exclude an earlier native write as a contributor.

Both minidumps omit the presumed closure heap and current Lua instruction.
Module-valued words found on the stack are not an unwound call stack. Therefore
the exact Lua closure/call and corruption mechanism remain unresolved. No
tools-disabled control was performed. The 29-register offline maximum is a
necessary check, not proof of target compiler, closure or lifecycle correctness.
Do not extrapolate the Global-only repair or passing desktop fixtures into
regional runtime acceptance.

Subsequent compiler/VM inspection identifies an independent contract violation:
this registration function captures16 upvalues, overflowing the native four-bit
count even though its register frame fits. See the owning
[packed Lua metadata finding](lua-stack-compatibility.md#independent-four-bit-upvalue-and-parameter-counts)
for producer/consumer addresses and evidence limits. The corrected request
interface reduces captures to12; unchanged menu behavior passes728 desktop checks.
This repairs a confirmed source defect without widening native metadata or
removing controls. A successful game test is still required.
