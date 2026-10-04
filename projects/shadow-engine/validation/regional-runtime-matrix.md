---
type: Validation Plan
title: Regional Runtime Matrix
description: Regional runtime evidence and calibrated offline compatibility gates.
tags:
- shadow-engine
- validation
- runtime
- compatibility
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-shadow-five-profile-runtime95-20261004
  title: Same-artifact five-profile acceptance and calibrated builder pass
- resource: ../../../evidence/catalog.json#E-shadow-a4ee-capture-20261004
  title: A4EE capture and five-profile automatic byte-validation result
- resource: ../../../evidence/catalog.json#E-shadow-compat-builder-20261004
  title: Automatic compatibility pipeline and regression evidence
- id: profiles
  resource: ../../../evidence/catalog.json#E-4d85852a0d8b
  title: Supported runtime profiles
- id: regional-handoff
  resource: ../../../evidence/catalog.json#E-981855846ea9
  title: Regional runtime test handoff
- id: matrix-evidence
  resource: ../../../evidence/catalog.json#E-9c66531d0987
  title: Refactor regional runtime evidence
- resource: ../../../evidence/catalog.json#E-1f29073db08d
  title: Supported runtime profiles
- resource: ../../../evidence/catalog.json#E-360aab196a1f
  title: Global83 gameplay and bounded workload evidence
- resource: ../../../evidence/catalog.json#E-6dc601f4ed20
  title: Global83 preceding startup evidence
- resource: ../../../evidence/catalog.json#E-201317dc5ab5
  title: Global83 runtime review and reported-positive baseline
---

# Profile and evidence contract

Global/04DF, Shev/A4EE, VMPless, Complete Edition and Asia/Miru form the regional
matrix. An all-five runtime-verified claim requires the same frozen candidate across all five.
Each result records exact ASI/runtime identity, expected profile, complete
preflight, operational activation, routing/integrity counters and the tester's
visual/stability report. Missing markers or silence do not manufacture a crash,
pass or human review. Preserve complete logs before changing their candidate.

The completed v 1.2.1 matrix is a historical regional baseline, not automatic
acceptance of later hooks. Apply the smallest justified tier after offline gates:

| Changed surface | Manual gate |
| --- | --- |
| Documentation/packaging with no runtime effect |Offline verification unless the diagnostic itself needs live evidence |
| Shared policy with unchanged profile/signature/resolver/preflight/hooks/ABI/transactions |After initial calibration, automated corpus and regression gates; another full manual matrix is not a routine requirement |
| Explicit regional mapping/address |Independent affected-profile proof; review whether focused live evidence is needed |
| Profile selection, resolver, signatures, preflight, bootstrap, detour topology, ABI or transaction |Automatic qualification stops for boundary review and focused recalibration; expand to a complete matrix only where the change warrants it |

Failure expands scope and blocks the affected candidate. The tester controls
launch/closure and visual classification; file preparation, hashes and marker
analysis do not replace that judgment. Intermediate Global-only research remains
explicitly outside all-profile compatibility claims.

# Recorded same-artifact regional observation

On2026-10-04,2.0.95 was reported working on Global, A4EE, VMPless, Complete
Edition and Asia/Miru with the identical menu-capable ASI. Each preserved
session confirms its expected profile,17-site Lua repair, downstream shadow
installation and Tools2.0.94 ready. Five explicit observations were recorded
against the frozen candidate; the subsequent35-gate build passed with no
calibration blocker and reproduced the same ASI hash.

Core shadow and Lua activation does not make every optional feature portable:
Global has driver/player-relative proofs; A4EE lacks the vehicle-identity and
finite-limiter hooks. Extended population proof remains Global-specific. The
separate compiler preset named Release has no corresponding manual observation.
There is no FPS benchmark or exhaustive engine-lifecycle guarantee in this matrix.

# Automatic compatibility builder

The mod-owned local builder composes the canonical compiler with existing
independent byte validators and native regression harnesses. It never loads a
captured game DLL as executable code. Its inputs are five fixed regional PE
identities, hash-identified private runtime images, the preserved source reference,
known Nexus host images and the compiler/toolchain. It produces reproducible
Internal and Release ASIs, allowlisted two-file packages and a machine-readable
report containing each gate, actual regional feature coverage and artifact hashes.

Qualification has three states: passed, failed and incomplete. Missing images or
initial calibration are incomplete; a byte mismatch, failed regression, omitted
profile or omitted required gate is failed. A failed run cannot package an
installable. A candidate package from an incomplete run is not release approval.
Interrupted runs retain an explicitly unsuccessful report. A run owns its lock,
logs and frozen output directory; it does not replace earlier deliveries.

The initial manual record binds an actual observation to the exact frozen ASI,
tested regional identity, Internal/Release profile and complete source hashes.
It cannot be created from failed checks, modified artifacts or changed source.
Subsequent qualification compares compiler identity, profile feature coverage,
native-boundary fingerprints and the gate implementation against that reference.
Native fingerprints include profile data, state layout, preflight, transaction
machinery, bootstrap and complete hook definitions. Routine policy changes outside
that surface use regression tests; a changed boundary stops automatic qualification.
This is conservative regression assurance, not proof of arbitrary future code or
of visual quality, game scheduling, GPU correctness or frame rate.

The complete offline corpus proves current core bytes on all five profiles.
The [A4EE capture](runtime-corpus-gate.md) fills the previously missing mapped
input; an old gameplay report alone did not supply that proof. Vehicle
owner/batch/retirement/handle paths remain mapped on Global, VMPless, Complete
Edition and Asia, and disabled on A4EE. Driver identity, player-relative selection, optional Internal Lua frame
repair and extended population proof remain Global-only. Their absence elsewhere
is disclosed feature coverage, not a newly implemented port. Global checks include
eight driver spans/class metadata, local-player binding/position-reader spans and
17 Lua sites, alongside synthetic activation/rollback tests. Core recognition
must not be confused with equivalent optional features on every region.

The observed builder run passed both reproducible build profiles, all 21 native
harness scripts, Python regressions and desktop Lua menu checks. The Python
discovery pass's intentionally skipped private decoder integration is subsequently
run against newly exported native fixtures. The complete five-profile run has
31 passing steps; only the unrecorded initial manual test keeps automatic
qualification incomplete. The A4EE capture was taken with Shadow Engine disabled
and must not be recorded as a manual acceptance test of the mod candidate.

Internal and Release differ: Release omits the menu mailbox and optional Lua
repair. A recorded Internal test is never evidence that Release was manually
played. Hosted compilation lacks the private corpus/calibration, so automatic
publication is disabled; approval and publishing are separate from compilation.

# Calibrated baseline results

The unchanged `ac74c2a` refactor ASI, SHA256
`006CEBE876D2997CBDFE5D525D5CFBD071FA3A9FF1D00C053C3C2210519A9EBC`, passed
all five profiles on 2026-08-24 without a reported crash or baseline shadow regression.

| Profile | Scoped result |
| --- | --- |
| Global |Approximately 20 minutes stable; later full activation superseded an observer timeout |
| A4EE |Clean pass, diagnostic failure counters zero |
| Asia |Pass with one isolated unconfirmed flicker and known nonfatal two-store/stale/late diagnostic pattern |
| VMPless |Extreme traffic 20 entries/23 of 24 faces with temporary world-shadow loss |
| Complete Edition |Same pressure behavior at sampled 21/24 faces, apparently faster recovery |

The v 1.2.3 frozen ASI SHA256
`5510E9F34F62DD61F6C49E4F946664A9241A743C9E989B98DABF335506ED4CC2` also passed
all five and matched offline profile predictions. Complete Edition activated
manager state after its one-time observer timeout; later owner reserve,
B4=21/A8=4, extra capacity, renderer and lifecycle markers proved operation.
This was a classifier false negative, distinct from later genuinely abandoned
startup described in [supervision](../architecture/startup-supervision.md).

Complete Edition still showed rapid spotlight/moon-shadow reacquisition at 26
admissions/26 of 30 faces: shared admission/residency pressure, not regional
failure. The subsequent shared B4=25 experiment passed unchanged corpus and a
representative extreme-load Global run with no reported flicker/crash/regression.
v 2.0.0 only changed the embedded version from the tested v 1.2.4 binary.

# Global .83 baseline evidence

The September12 Global/04DF Windows11 test used Internal .83 SHA256
`362F4178EB53AA50BE053A3DF39A285BF34887CD04EDAA2B0F62599586FFAA27`.
The tester reported that it seemed okay. Both preserved sessions restored
revision57 and completed startup; same-session SE7 status confirmed0/4096/4096.
The gameplay log's20 lifecycle snapshots balance results and resource releases.
Its final totals are314,600 nonnull plus65,892 null equals380,492 consumed,
with314,600 released resources and zero recorded lifecycle failure counters.

The manual capture has23 readable entries/26 faces, continuous peak29/30 and
zero clamps/dropped entries. Normal transport delivered19/19 summaries without
drops or write failures. A five-second workload has50 manager/50 queue samples,
mean57.32 candidate vehicle owners and26.02 faces, with no sampled fail-open or
unreadable records. These are CPU observations and scoped baseline evidence.

Detailed admission/tail history was not recorded. DXGI ETW error5 produced no
presentation intervals or FPS measurement. Limit0 bypassed selection, so this
does not independently retest finite-limit driver protection, resolve pop-in,
prove GPU completion or extend acceptance to other profiles. The startup timing
boundary is recorded in [supervision](../architecture/startup-supervision.md).

# Historical lifecycle and observer failures

| Candidate | Runtime result and compatibility consequence |
| --- | --- |
| .3 release boundary`0x003C1350` |Two crash-free bridge crossings still produced 20,130 stale/11 late results and visual/audio/frame stutter. Crash-free alone was insufficient. |
| .4 first wrapper batch`0x003E17A6` |No crash/freeze/audio/game stutter; ownership/rejected cleanup exact, zero release/orphan/reset failures.25,945 stale/13 late remained.221 candidates, 30/30 faces, 1,695 clamps/2,077 dropped entries; separate ground-local blink preceded churn. Four profiles had 63 exact checks; A4EE's old attestation did not cover the added site. Not ready for release matrix. |
| .5 later pre-finalizer`0x003E19E3`→`0x003E0E70` |Three additional wrapper submissions precede this boundary. Final serial 106,112 still 17,496 stale/10 late with exact ownership and zero release/orphan/reset failure; rapid bridge headlight/shadow turnover reported. Static instruction order was not completion proof. |
| .12 intersection observer |Regional lookup detour required live kind 3 lookup evidence and visual report, then affected-profile testing. Four 71-check images did not certify A4EE or all-five hook operation. |

These rejected gates retain their outcome, not an instruction to rebuild or
repeat them. The known local blink remains distinct from the result-lifecycle
churn. The .83 baseline recorded above
does not retroactively accept rejected candidates or unsupported profiles.
