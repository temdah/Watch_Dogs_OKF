---
type: Implementation Design
title: Lua Frame Compatibility Fix Design
description: Proposed complete frame-size lifecycle repair with transactional activation and
  independent GC-focused validation.
tags:
- shadow-engine
- lua
- compatibility
- design
- lifetime
status: draft
sources:
- id: private-defect
  resource: lua-stack-compatibility.md
  title: WD1 Lua Packed Frame Size and Garbage Collection
- id: private-transaction
  resource: patch-transactions.md
  title: Patch Transaction Model
- id: private-rules
  resource: ../../../evidence/catalog.json#E-56efbf5ff3f6
  title: Engineering and ownership contract
---

# Scope and remaining gates

Internal .57 introduced the experimental 17-site Global-only repair, retained in subsequent Internal candidates including .80. Initial Global loading/tools operation succeeded and activation was logged; this is not full lifecycle, host, regional or Release acceptance. The design below states the complete contract and remaining gaps. It is independent of shadow policy, and no tracer or controlled historical lifetime comparison has been completed.

# Required invariant

Each executable prototype has an exact validated required-register count.
Compiler register reservation, loaded bytecode metadata, stack allocation,
call-frame endpoints, GC visibility, debug/verifier and serialization consumers
must agree. Every live temporary must be rooted during a collection; returning
from calls must not retain dead values indefinitely. Existing argument, vararg,
upvalue, coroutine and result-count semantics remain unchanged.

Preserve the supported native upper-bound convention after verifying all its
consumers. The observed compiler rejects requirements >=250; this design does
not raise that ceiling, argument limits, instruction limits or other bitfields.
The mapped binary pre-verifier uses a different unsigned comparison allowing 250;
preserve that distinction rather than silently changing bytecode acceptance.

# Architecture

One dedicated Shadow Engine compatibility subsystem owns installation state,
profile-specific immutable site descriptions, any new metadata and teardown.
Separate storage/accessors, hook mechanisms, profile validation, orchestration,
and diagnostics. No dependency on shadow admission, quality policy or UI state.
Enable before any affected source compilation/bytecode loading, not on save-load
or first menu drawing. This is not a user-toggleable optimization.

## Exact frame-size storage: decision gate

Preferred candidate: a proven unused byte inside the existing prototype layout.
Store the full supported count without changing the structure size or shifting
fields. This avoids per-call hash lookups and pointer-lifetime registries.
Zero bytes in one dump are NOT proof of unused storage. Map allocation size,
initialization, copying, alignment, loader, dumper, host accesses, destruction
and every overlapping read/write before selecting an offset. Preserve low flag
bits and unrelated fields. Do not guess a spare byte or leave old packed readers
active for large frames.

Fallback design if no safe in-object space exists: exact per-prototype external
metadata, with one lifetime owner. Publish before execution/GC can observe the
prototype; remove on actual prototype destruction, not closure destruction.
Address reuse must not inherit old metadata. Map execution concurrency and
reentrancy before choosing synchronization. Allocation failure or unknown
metadata cannot silently fall back to the truncated count. Quantify call-path
overhead before accepting this option. This is a decision alternative, not two
concurrent mutable sources of truth.

## Complete boundary inventory

Map and cover:

* Prototype creation and every compiler maximum-stack update, including inline
  copies and register reservation. Preserve exact count before truncation.
* Source compilation and binary loading; nested prototypes and error cleanup.
* Bytecode verification and register bounds, including implicit multi-register
  operands, SETLIST payload words, calls, returns, loops, varargs and closure
  binding instructions. A scan of NEWTABLE destinations alone is insufficient.
* Stack preallocation, Lua/C call transitions, tail calls, coroutine resume,
  frame top restoration, GC stack traversal/shrinking and debug inspection.
* Serialization/dump and reload: exact count must survive round trips without
  silently changing the accepted file-format contract.
* Native and host-side structure access, copying, cached function pointers and
  pre-existing hooks. Scope external integration changes separately if needed.

Do not reconstruct existing corrupted metadata using count modulo 32 or only
the highest A operand. A late-loaded patch requires a separately proven complete
verifier/migration before those prototypes execute; preferred activation avoids
that situation entirely.

## Installation and failure behavior

Read-only preflight validates the complete site set, runtime identity, expected
instructions and host compatibility before any write. Apply transactionally
before Lua execution at a proven startup boundary; do not patch a live compiler
or race executing functions. A failed write rolls back the owning early transaction. In the .88 integration,
an unavailable host or pre-write Lua-site proof skips only this optional repair;
the independently validated shadow plan may continue. See the
[host compatibility case study](../compatibility/nexustools-init.md). Inactivity is NOT proof
that the underlying unpatched Lua runtime is safe.

Once active prototypes depend on new metadata, do not hot-unload or switch the
subsystem off. A mapped dependency lifetime/pinned module is required. Runtime
validation failure should prevent the affected chunk from executing via a
proven host error boundary, not continue with a wrapped count or swallow errors.
Interception of other scripts changes the host compatibility boundary and needs separate review.

# Verification and release gates

1. Complete mapping and independent site/operand inventory. Verify host and
   regional compatibility; unsupported runtimes remain explicitly unsupported.
2. Offline proof harness using verified semantics or actual extracted/owned
   implementation, not a mock that repeats candidate constants. Test counts
   30/31/32/33, 50/51, 63/64/65 and 248/249/250 with expected rejection at the
   proven upper bound. Exact bytes and metadata should be independently checked.
3. Stress GC at allocation/constructor boundaries, especially before SETLIST.
   Verify child identity and contents afterward, bounded live memory, and cleanup
   after dropping roots. Include closures/upvalues, varargs, tail calls, nested
   calls, coroutine yield/resume, exceptions and binary round trips. Do not alter
   production GC policy to make these tests pass.
4. Fault-inject metadata allocation failure, unsupported sites, transaction
   rollback and prototype reuse where relevant. Prove no partially active fix.
5. Internal runtime candidate retains the current shadow policy and every tool.
   Validation covers repeated same-save loads, all menus including Trainer, normal play
   and dense traffic. Measure frametimes and memory against the unchanged baseline.
   Relevant regional runtime gates remain mandatory for native hook changes.
6. Only after runtime acceptance may future features depend on this subsystem.
   Release keeps startup compatibility/version information and bounded fatal
   diagnostics, not continuous per-call logging or GC tracing.
