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
