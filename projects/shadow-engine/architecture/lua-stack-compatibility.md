---
type: Runtime Compatibility Finding
title: WD1 Lua Packed Frame Size and Garbage Collection
description: Confirmed packed frame-size defect and matching stale item evidence; configuration-dependent
  crash causality remains unproven.
tags:
- shadow-engine
- lua
- crash
- garbage-collection
- compatibility
status: draft
sources:
- id: evidence-source-1
  resource: ../../../evidence/catalog.json#E-3fe2b424838f
  title: Sanitized technical handoff prepared for host-author review
- id: private-first-runtime-review
  resource: ../../../evidence/catalog.json#E-300ad7bb340f
  title: First user-reported success and reviewed activation/capture markers
- id: private-native-repair-test
  resource: ../../../evidence/catalog.json#E-d17c60662771
  title: Isolated captured compiler, verifier, VM-top and GC-marking regression harness
- id: private-resident-reader
  resource: ../../../evidence/catalog.json#E-e29a7dd8b047
  title: Resident-only working-control inspection
- id: private-comparison
  resource: ../../../evidence/catalog.json#E-85512729b871
  title: Address-independent full-dump prototype comparison
- id: private-dump-trace
  resource: ../../../evidence/catalog.json#E-e463e89671b2
  title: Full-dump prototype, compiler, frame and GC trace
- id: private-inspector
  resource: ../../../evidence/catalog.json#E-f2238da692f0
  title: Bounded read-only captured Lua heap and bytecode inspector
---

# Confirmed defect and current implementation

The captured Global Lua runtime truncates prototype frame counts to five bits. Internal .57 introduced an experimental 17-site Global repair retained through .80. Its first reported run loaded and tools worked; logs confirmed all 17 sites active and a completed menu capture at serial 33484. This is tested first-run evidence, not full lifecycle/Release acceptance or a proven explanation for every configuration-dependent crash. Complete Edition and the other profiles are unsupported for this repair.

In the Global runtime captured with Shadow Engine 2.0.56, the native
Lua compiler permits stack requirements below 250 but stores the count in only
five bits of Proto byte 0B. Counts above 31 truncate. The VM uses that truncated
count for both the call-frame endpoint and L->top, which bounds GC marking.
This is captured-code and live-prototype evidence, not regional validation.
[^private-dump-trace]

The retained trainer/data/Items.lua prototype declares 19 slots while its first
constructor batch uses R0..R50 before SETLIST. Required 51 modulo 32 equals 19.
Item 24 is constructed in R24, outside GC-visible R0..R18, and only subsequently
published to the collection. Its retained array reference points to memory now
owned by Lua's shared string buffer; it is the sole table-tagged array entry
absent from rootgc. The later info.category access crashes on that stale object.
The exact historical sweep was not recorded, but the invalid frame producer,
GC visibility failure and matching victim are established.[^private-dump-trace]

# Function and ownership map

All RVAs below are Disrupt Global in the captured process, not portable hooks.

| Boundary | Role and lifetime consequence |
| --- | --- |
| 1C11B0 / 1C1230 | Allocate/free a 96-byte prototype; initialize packed metadata with a16-bit zero store at+0A. Ownership of adjacent+0C/+0D padding remains an activation gate. |
| 1D5F88 | Compiler open-function path initializes the packed frame maximum to 2. |
| 1DA670 / 1DA6D0 | Compiler stack check/register reservation accepts below 250, stores count shifted into a five-bit field. |
| 1D9F65 | Binary-loader stack-size assignment also packs the input into that field. |
| 1C94BB | Bytecode dumper extracts packed count and writes one serialized byte; full-byte repair must update both load and dump. |
| 1BFE30 | Prototype pre-verifier checks frame ceiling, parameter/vararg bounds, counts and terminal RETURN. Its unsigned ceiling comparison permits 250, unlike source compiler rejection at 250. |
| 1BFEF0 / 1BFF10 / 1BFF25 | Operand verifier selects raw-register or register/constant bounds; register alternatives consume packed maximum. |
| 1BFF50 / 1BFFEF | Symbolic verifier checks instruction/register bounds. Preserve packed r15 flag value for later vararg tests; move only its derived frame bound to full-byte storage. |
| 1C28BE | Precall uses the frame count to check/grow Lua stack capacity before publishing the call frame. |
| 1C296D through 1C29B6 | Frame setup reads Proto+0B >>3, publishes ci->top and L->top. |
| 1C6068 / 1C6FDB | NEWTABLE publishes register value/tag, then may run GC before SETLIST roots the child in its collection. |
| 1C35E0 | GC thread traversal marks only values below L->top. |
| 1C3190 | Strong-table traversal marks published array children; no weak metatable exists for this collection. |
| 1C5800 / 1C8CA0 | Concatenation/buffer-space path uses global+58 buffer, capacity+68; this storage aliases the stale item pointer. |
| 1C7C80 / 1C7CC2 | Table lookup/faulting read consumes the stale table on category lookup. |

# Isolated repair evidence

The 17-site repair recipe uses
candidate full-byte storage at Proto+0C while leaving low flags at+0B intact.
It covers allocation initialization, source initial maximum and both compiler
updaters, precall capacity/top, loader/dumper and verifier consumers. This isolated harness preceded .57 integration; it does not independently prove deployment safety.

One native-code harness passes 48,362 assertions using copies of the captured
instructions in its own process. Source compiler output feeds actual VM-top
arithmetic, then actual GC thread traversal/object marking at every construction
boundary through R50. Original instructions preserve 19 of 51 objects; candidate
instructions preserve 51 of 51, including R24. After publication, native strong-
array traversal protects all 50 child tables in either case. Thus the rooting
mechanism is reproduced independently of a new game crash. This does not record
the historical sweep or establish Shadow Engine's triggering allocation.

The harness also tests all counts 2..251 against source-compiler rejection at 250,
all low flags, register/constant bounds and verifier ceiling/vararg handling.
Only error reporting in the harness compiler copy is replaced with a marker;
the rejection branches remain native. No game process or third-party DLL is
loaded. Full GC lifecycle/coroutine tests, serialization roundtrip, padding
ownership, complete host/regional validation and startup ordering remain open.

Captured NexusTools host initialization is at RVA0A0E00, checking/setting its
instance guard byte before logging Initializing CustomLuaManager. Callers at
1B6B38 and 2A3AFC pass the static instance at host+C62AE0. This maps the manager
initialization guard, NOT a proven Lua-state creation boundary or patching lock.
The .56 startup log records callbackCalls=0 and DllMainDeferredFallback;
asynchronous worker readiness checks alone are not proof that no Lua prototype
exists or can execute during a format transition. Those checks do not establish the missing ordering/lifetime contract.

# Safety and remediation boundary

Changing allocations/menu layouts can alter GC timing and expose the malformed
frame. That does not identify one historical menu allocation as the trigger or
prove every reported crash shares this cause. The first-run .57 success does not close the remaining causality and safety gates.

A bounded-register incremental item constructor is a source-level workaround that preserves menu functionality. It does not repair the native runtime contract. A general runtime
fix requires coherent treatment of compiler/loader/frame consumers, not one
larger stack constant. Global GC disabling and feature removal are not fixes.

The dump inspector flags 1760 out-of-frame NEWTABLEs in the item-data prototype;
no other retained prototype triggers that limited check. This is not a complete
bytecode verifier and must not be called a clean bill of health for all scripts.

[^private-dump-trace]: Full-dump trace and captured native instructions.
[^private-first-runtime-review]: User report and log review; original session log was later overwritten.

# Working-control comparison and attribution limits

A working control contained NexusTools and Addons without Shadow Engine. Resident-only reads recovered a retained populateItems closure with 2,753 valid table children; each appeared in the 5,157-object GC-next suffix through null, and the collection/closure headers were unchanged on reread. Item 24 was intact. The suffix was not an independently located rootgc, and reads were non-atomic. Searching for the exact 20,314-instruction constructor was inconclusive; it may have been collected after execution, so absence cannot prove corrected frames.

Four small ranges - compiler stack check, loader assignment, frame setup and GC thread traversal - were byte-identical between working and failing captures. Thus the defective contract also existed in the working control, without establishing that control constructor's declared frame or the exact collection that exposed the failure. GC timing/lifetime remains a supported hypothesis, not recorded causal attribution. Changing menu allocations can change exposure without identifying a historical triggering allocation.

The address-independent comparison reproduces the 19/51 mismatch. A full-dump attempt of a working control was incomplete and coincided with an application hang/closure; capture impact cannot be excluded, so it is not evidence of spontaneous baseline failure. Resident-only reading avoids suspension/injection/modification but is not guaranteed zero-impact. Native lifetime hooks remain unimplemented because register preservation and startup ordering are not proved; ordinary ABI detours need not be transparent to optimized internal Lua calls.

The integrated repair has complete site-byte preflight, explicit Global immutable profile data, readiness checks and early transaction rollback; all 17 failed-site positions and commit were tested. Observed late startup is rejected. Readiness checks do not prove synchronous format-transition safety or ownership of Proto+0C/+0D padding. Release excludes the experiment. No host response independently confirms the diagnosis or closes those gates.
