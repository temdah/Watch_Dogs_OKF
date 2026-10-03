---
type: Experimental Compatibility Contract
title: Internal Lua Frame Repair Candidate
description: Global-only full-byte Lua frame metadata experiment, activation checks and unresolved
  safety boundaries.
tags:
- lua
- compatibility
- internal
- experimental
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-33b0008ea85f
  title: Immutable frame-format sites and host identity data
- resource: ../../../evidence/catalog.json#E-92609b1378ab
  title: Read-only preflight and transaction-owned application
- resource: ../../../evidence/catalog.json#E-327d2bb22e5d
  title: Actual-site commit and all17 write-failure rollback checks
---

# Scope

Internal v 2.0.57 includes an experimental 17-site frame-size repair for the mapped
Global runtime only. Release excludes the sites and activation code. Other
profiles retain their existing behavior and log the repair as unsupported;
regional shadow-layout deltas are never applied to these Lua sites.

The candidate keeps a full-byte count at prototype+0C, with original flags at
+0B. Prototype initialization also clears+0D. It updates source initialization,
both compiler maximum-stack writers, stack-capacity/top readers, binary count
load/dump and register/argument verifier consumers. The source compiler still
rejects 250; the native binary pre-verifier retains its distinct allowance 250.
Prototype size, shadow policy, tools, ordinary GC and physical capacity remain
unchanged. There is no new detour, runtime side table or per-call logging.

# Activation and limitations

All site bytes and overlaps are checked before mutation and rechecked before
the format writes. Writes join the existing early transaction; any write failure
rolls back the complete early plan. An activation marker follows commit.
The mapped host identity, manager-not-started flag and helper interception/
readiness exports reject observed late startup. The host is only read.

These checks are NOT a synchronous exclusion mechanism. They do not prove that
every native Lua state is absent. Existing prototypes are not migrated. Complete
padding ownership, race-free startup, full GC/coroutine/serialization lifecycle,
regional compatibility and actual crash resolution remain unvalidated. This
candidate must not be described or distributed as a production crash fix.

# Verification boundary

The isolated copied-native-instruction test demonstrates preservation of the
full count and GC visibility before constructor publication. Actual-site
transaction tests cover all 17 failures and successful commit. Offline passes
do not establish safe game loading or menu behavior; runtime acceptance is independently reported.
The original .57 validation retained every tool function. Later tool changes
have their own [host and saved-settings contract](../architecture/saved-settings.md).

# Tool-authoring implications

The underlying mapped defect concerns simultaneous Lua registers, not a 24-item
menu limit. A51-slot requirement wraps to 19 in the original five-bit field.
Prefer small cohesive functions and incremental strongly owned table
construction for large tool datasets, without removing any functionality.
These are mitigations, not proof of safety: inspect actual required registers
and declared frames throughout the generated chunk and nested prototypes.
On the mapped unpatched runtime the count must fit 31; source line counts,
widget counts, desktop Lua tests and a limited NEWTABLE scan cannot certify it.
Do not disable GC or treat pcall as protection from native memory corruption.

A working configuration can retain the same defective native code. A menu
change can expose the problem through allocation timing without being its
origin. Similar crashes in other mods require their own evidence; neither
NexusTools fault ownership nor universal crash resolution is established.
Do not duplicate this experimental runtime patch in each mod or make it an
undeclared release dependency. A shared fix needs coordinated ownership,
startup safety and explicit supported runtime identities.
