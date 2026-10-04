---
type: Compatibility Investigation
title: Addons Lua Frame Defect Attribution
description: Comparison of historical Addons failures with the confirmed Global frame-size and
  GC visibility defect.
tags:
- shadow-engine-addons
- lua
- gc
- compatibility
- attribution
status: draft
sources:
- resource: ../../evidence/catalog.json#E-addons-a4ee-runtime50-provider95-20261004
  title: Unchanged Addons runtime succeeds with active A4EE Lua-frame repair
- resource: ../../evidence/catalog.json#E-addons-a4ee-table-crash50-20261004
  title: Repeat A4EE table-lookup crash despite retained menu ownership
- resource: ../../evidence/catalog.json#E-trainer-items-frame-correction-20261004
  title: Incremental item publication and full-data GC-stress equivalence
- resource: ../../evidence/catalog.json#E-addons-a4ee-table-crash49-20261004
  title: Matched A4EE table-lookup crash, package hashes and complete installed Lua audit
- id: comparison
  resource: ../../evidence/catalog.json#E-9c52b3b42ef6
  title: Existing-event, packaged-source and reference-heap comparison
- id: defect
  resource: ../shadow-engine/architecture/lua-stack-compatibility.md
  title: WD1 Lua Packed Frame Size and Garbage Collection
- id: authoring
  resource: ../../compatibility/nexus-tools-extension-authoring.md
  title: Nexus Tools Extension Authoring
---

# Result

Insufficient evidence to classify historical Addons menu-related native failures
as the same mechanism or as a different defect. Shared frame truncation remains
a credible explanation. Historical assertions that particular Addons callbacks,
category counts, traffic removal or thunder caused those failures are not
established by retained evidence and must not guide feature removal.

# Evidence comparison

Original .5/.6/.7/.13/.15 Windows events and the reference captured process share Disrupt
timestamp5CD045B4 and C0000005 at1C7CC2. The .6 loader log independently identifies
Global-5CD045B4. Historical events lack full image hashes, captured native
compiler bytes, registers, Lua frames, victim ownership and GC state. No dump
matched to those historical Addons sessions was found in the searched evidence.

Compile-only screening of15 ZIP entrypoints plus current/historical modules
covers66 files/870 prototypes. None exceeds24 registers; accepted .21's packaged
maximum is18. The bundler preserves package.preload function boundaries. This
uses the bundled FCBConverter Lua5.1 compiler, NOT the WD1 target compiler.
It includes compiler temporary reservation but is not an all-operand target
verifier and cannot establish the failed sessions' required/declared frames.

The reference process's actual GC chain contains5194 objects and Trainer's
20314-instruction data prototype with declared19, first SETLIST A0/B50 and
NEWTABLE through R50. The reference concept owns the stale item24 and string-
buffer/GC interpretation; the historical sweep itself remains unobserved.

The same reference chain contains four public Addons reporter prototypes. Their
source SHA256 D32C895BAF5B9116ECEDDD7E5A8286C5079626DCF217E7B5A69004E17F75BFB9
matches our public source exactly. Declared frames7/5/3/4 and instruction counts
28/20/7/25 agree with the corresponding retained functions' offline screen.
None has an out-of-frame NEWTABLE. Top-level/loadExport prototypes were not
found in that chain; no absence-based safety inference is valid. This is
co-presence with the demonstrated Trainer defect, not proof of Addons causation
or full validation of its internal historical builds.

# Attribution and repair limits

A shared exception RVA and successful compatibility run cannot establish the
historical corrupting operation. A matched exception dump would need caller/key,
object storage, actual prototype frames and GC membership to distinguish causes.
The experimental native repair has unresolved activation/lifecycle gates; its
presence must not be silently assumed by another mod. One owner must control
the native patch to avoid competing writes. Normal GC and unrelated functions
remain essential controls when testing the proposed mechanism.

# A4EE table-lookup failure with compliant Addons bundle

A matched A4EE signed-variant process (PE timestamp `5CD13864`, installed DLL
SHA256 `a4eead7a645ab4340a67622da4bfc91789e8cecfd53f605499a0e4b09b3ee60a`)
with Addons internal2.1.49 crashed at `004D93A2`, a string-key lookup inside the
native Lua table getter. The faulting instruction is `cmp dword ptr [rax+18],4`;
RAX=`6E69676E67659E1D` is an invalid node address. The preserved caller return
and matching code identify the Lua gettable/GETTABLE path, not a bolt draw call.
This classifies the failing operation, not the earlier corruption writer.

All six installed Addons members match the delivered package byte for byte.
Compile-only inspection of its **final installed bundle**, including its outer
chunk and every nested prototype, passes all120 prototypes: maxima23 registers,
14 upvalues,3 fixed parameters. The outer chunk is23/0/0. These auxiliary
compiler results do not expose the target VM's live prototype or GC state.

The same process completed Addons native initialization and reached deferred
menu tab-layout callbacks. The installed built-in Trainer's `data/Items.lua`
root independently requires52 registers, above31; its category loader executes
that file and later traverses item tables from its deferred layouts. The
optional Global Lua-frame repair explicitly did not activate on A4EE. This is a
concrete neighboring source-contract violation and a credible table-lifetime
failure mechanism, consistent with the earlier captured Trainer defect. It is
not proof that the failed object belonged to Trainer or that Addons was uninvolved.

The minidump does not contain the candidate table, key string, Lua state or
current bytecode heap. Checking smaller/adjacent captured regions did not recover
them. Stack module-valued words are not a fully unwound call stack. No isolated
Trainer-disabled control was observed. Consequently exact Lua source attribution,
the corrupting operation and a successful repair remain unproved. Do not remove
Addons features or declare regional runtime acceptance from the offline pass.

## Bounded source-level correction of the oversized constructor

For the inspected Trainer Items input (SHA256
`ac0db24223d4a62e0d996a9a166139a250bbd767692aa92b4c196d1ae571c439`),
replace the bulk outer array constructor with a rooted local table and sequential
`items[index] = { ... }` assignments, then return that table. Each complete item
is published before the next is created. Field literals, numeric array order and
all Trainer consumers remain unchanged. This removes the need to keep50 pending
item references in temporary registers before SETLIST without changing native VM
metadata or relying on another mod's optional frame repair.

Auxiliary float-Lua compilation reduces the one shipped data prototype from52
registers to4, with0 upvalues and0 fixed parameters. A real-runtime semantic test
compares all2753 ordered records and11012 fields with the original data oracle,
retaining72 category memberships. The original oracle loads with GC stopped;
the corrected constructor runs with normal GC and289 additional hook-triggered
full collections. Every record remains readable and equal afterward. The bounded
transformer rejects an unrecognized source hash and malformed data grammar; it
does not evaluate arbitrary source during generation.

These checks repair a demonstrated source/frame contract violation. They are not
execution in the game's packed VM, proof of the missing historical corruption
writer, or successful gameplay acceptance. A later host update changing the
source requires a fresh audit rather than silently reusing the old data override.

# Repeat after explicit menu ownership

The subsequent A4EE run with internal2.1.50 still faults at `004D93A2`, with
RAX=`6E69676E67659E1D` and RCX=`00408517`, identical to the previous run despite
changed heap addresses. All six installed members match the package; the final
121-prototype bundle passes23 registers/14 upvalues/3 fixed parameters. The
native ASI is byte-identical to the previous run. The host log again ends during
deferred tab layout. Retaining the category/callback owner therefore did not
resolve this failure. It does not isolate or exonerate another mechanism.

The new minidump again omits the affected table, key and Lua state. Matched module
identity and repeated invalid pointer narrow the failure signature; they do not
identify the script or memory writer. A read-only failure snapshot needs the
register-reachable heap, native stack, closure/prototype chain and source data.
Existing source-limit checks must remain distinct from this runtime attribution.

# Working session after regional frame repair

With the same six installed Addons2.1.50 files, the human tester reports that the
mod now works after enabling provider2.0.95. The new provider session identifies
A4EE and records `LUA_FRAME_REPAIR_ACTIVE` at17 sites. The host continues through
startup and accepts Addons storm-event requests. This is positive runtime evidence
for that installed combination on A4EE, beyond the earlier offline frame checks.
It strongly supports the shared Lua-frame defect as the startup blocker, but does
not identify the exact object or corrupting operation in the two prior dumps.

No Addons capture/repair build or Trainer data override was installed for the
successful run. The proposed exception snapshot was withdrawn before delivery;
its offline fixture results are not runtime evidence. Detailed bolt appearance,
audibility and the other four regional builds are not established by this report.
The world-observer log retained an older PID header and was excluded from the
new matched record; a file's fresh modification time alone is insufficient to
assign every contained line to the current process.
