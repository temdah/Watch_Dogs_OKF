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
