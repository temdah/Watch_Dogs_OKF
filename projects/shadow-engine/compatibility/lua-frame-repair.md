---
type: Experimental Compatibility Contract
title: Internal Lua Frame Repair Candidate
description: Five-profile full-byte Lua frame metadata experiment, activation checks and unresolved
  safety boundaries.
tags:
- lua
- compatibility
- internal
- experimental
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-shadow-five-profile-runtime95-20261004
  title: Five-profile runtime acceptance and calibrated qualification
- resource: ../../../evidence/catalog.json#E-shadow-asia-lua-runtime95-20261004
  title: Human Asia acceptance and matching repair activation
- resource: ../../../evidence/catalog.json#E-shadow-complete-lua-runtime95-20261004
  title: Human Complete Edition acceptance and active-repair session
- resource: ../../../evidence/catalog.json#E-shadow-vmpless-lua-runtime95-20261004
  title: Human VMPless acceptance and matching active-repair session
- resource: ../../../evidence/catalog.json#E-shadow-a4ee-lua-runtime95-20261004
  title: Human A4EE acceptance and matching active-repair session
- resource: ../../../evidence/catalog.json#E-shadow-lua-regional-20261004
  title: Independent five-profile mapping, native semantic checks and transactional activation tests
- resource: ../../../evidence/catalog.json#E-33b0008ea85f
  title: Immutable frame-format sites and host identity data
- resource: ../../../evidence/catalog.json#E-92609b1378ab
  title: Read-only preflight and transaction-owned application
- resource: ../../../evidence/catalog.json#E-327d2bb22e5d
  title: Actual-site commit and all17 write-failure rollback checks
---

# Scope

Internal v2.0.95 extends the experimental17-site frame-size repair to Global,
A4EE/Shev, VMPless, Complete Edition and Asia/Miru. Release continues to exclude
the sites and activation code. Each region has an explicit independently
matched table; regional shadow-layout deltas are never applied to Lua sites.
The earlier Global-only implementation remains the historical control.

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
padding ownership, race-free startup and full GC/coroutine/serialization
lifecycle remain unvalidated. All five regions have bounded human acceptance
of the same2.0.95 artifact; that does not establish exhaustive lifecycle safety.

# Verification boundary

All85 regional patch locations match their native bytes. Ten surrounding
functions/instruction blocks per region have independent frozen fingerprints.
The symbolic verifier match stops before its region-specific jump-table access;
relative call/branch and RIP-address displacements were masked for discovery,
then exact regional block hashes were frozen for subsequent validation.
No site is found by applying a shadow-address delta or an unchecked live scan.

Isolated copies of each region's compiler, pre-verifier, operand checker and VM
top calculation pass48,256 checks per region. Original51-slot input records19;
repaired input records51. Tests retain flag bits, valid small frames, source
rejection at250 and the binary pre-verifier's existing ceiling semantics.
Compiler error calls alone are replaced with test-process rejection markers;
no game DLL is loaded or game process accessed. These tests do not execute a
full regional Lua interpreter or prove full GC/coroutine/serialization lifecycle.

The actual activation module and transaction journal pass8,941 checks across
five regional recipes and two exact NexusTools host fixtures. Every site-write
failure rolls back, every mismatched site is rejected, and late/unknown host
conditions remain inactive. The builder requires these gates and reports Lua
repair coverage separately from unrelated optional Global-only features.

The isolated copied-native-instruction test demonstrates preservation of the
full count and GC visibility before constructor publication. Actual-site
transaction tests cover all 17 failures and successful commit. Offline passes
do not establish safe game loading or menu behavior; runtime acceptance is independently reported.
The original .57 validation retained every tool function. Later tool changes
have their own [host and saved-settings contract](../architecture/saved-settings.md).

# A4EE runtime observation

On 2026-10-04, the user reported that everything runs and A4EE is stable with
the unchanged 2.0.95 candidate. The matching session (PID6252) selected
`a4ee-signed-variant`, completed the17-site Lua repair and downstream shadow
installation, and continued rendering. Native and NexusTools logs were preserved
with the ASI and game-DLL identities in the evidence record. This supports
resolution of the reported startup failure in the tested configuration. It does
not identify the historical corrupting object or establish other-region gameplay,
full lifecycle safety, or a performance improvement.

# VMPless runtime observation

On 2026-10-04, the user reported the same2.0.95 candidate working on VMPless1.06.
Session PID32320 selected `vmpless-1.06`, activated all17 Lua repair sites and
installed downstream shadow hooks. Tools2.0.94 reported ready. Periodic shadow
summaries recorded zero store/release failures, stale lineage and duplicate
resources. Nexus also logged P203/P336 relative-call range errors and an unnamed
hook failure; these are preserved and not described as a clean host log or
attributed to the Lua repair. Human success covers the tested configuration,
not every host hook, full Lua lifecycle, or other regional builds.

# Complete Edition runtime observation

On 2026-10-04, the user reported the2.0.95 candidate working on Complete
Edition1.06.329. PID33156 selected the matching profile, activated all17 Lua
repair sites, installed downstream shadow hooks and loaded Tools2.0.94 to ready.
Periodic native summaries recorded zero store/release failures, stale lineage
and duplicate resources. Nexus retained an unnamed hook error and a missing
trackingconfig JSON error; human success does not certify every host feature.
Native and host logs and the previous DLL were preserved. Full Lua lifecycle
safety and untested regions are not inferred from this result.

# Asia/Miru runtime observation

On 2026-10-04, the user reported2.0.95 working on Asia/Miru1.06.329. PID18360
selected the matching profile, activated all17 repair sites and installed
downstream shadows. Tools2.0.94 reported ready. Preserved host logs include
two unnamed hook failures and a trackingconfig JSON error; user acceptance
does not establish every host feature or full Lua lifecycle safety.

# Global observation and completed regional comparison

On 2026-10-04, the user reported Global working, completing the same-artifact
five-profile cycle. PID33528 selected Global, activated17 repair sites, installed
downstream shadows and loaded Tools2.0.94 to ready. Periodic native summaries
showed zero store/release failures and stale lineage; unrelated host hook and
trackingconfig errors remain preserved. All five observations were bound to
the frozen ASI/source hashes and the automatic builder subsequently passed
all35 gates with calibration present. Optional regional capabilities differ;
this does not validate every optional collector, full Lua lifecycle or FPS gains.

The publicly packaged menu-capable artifact is built with the preset named
Internal. The optional compiler preset named Release still omits this repair.
Compiler preset names must not be confused with public availability.

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

## Regional function coordinates

The following RVAs identify the mapped producer/consumer functions, not shadow
layout offsets. Every listed function is checked against the frozen regional
code fingerprint before release qualification.

| Profile | Prototype allocation | Compiler check | Register reserve | Lua precall block | Loader | Dumper |
| --- | --- | --- | --- | --- | --- | --- |
| supported-04DF | `001C11B0` | `001DA670` | `001DA6D0` | `001C28B9` | `001D9D80` | `001C93B0` |
| a4ee-signed-variant | `004D2890` | `004EBD50` | `004EBDB0` | `004D3F99` | `004EB460` | `004DAA90` |
| vmpless-1.06 | `004E4D60` | `004FE240` | `004FE2A0` | `004E6469` | `004FD950` | `004ECF60` |
| complete-edition-1.06.329 | `0192EC20` | `019480E0` | `01948140` | `01930329` | `019477F0` | `01936E20` |
| asia-miru-1.06.329 | `004CAA00` | `004E3EC0` | `004E3F20` | `004CC109` | `004E35D0` | `004D2C00` |
