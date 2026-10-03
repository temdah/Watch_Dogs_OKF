---
type: Validation Plan
title: Regional Runtime Matrix
description: Completed baseline matrix and risk-based manual gates for later candidates.
tags:
- shadow-engine
- validation
- runtime
- compatibility
status: draft
sources:
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
matrix. An all-five claim requires the same frozen candidate across all five.
Each result records exact ASI/runtime identity, expected profile, complete
preflight, operational activation, routing/integrity counters and the tester's
visual/stability report. Missing markers or silence do not manufacture a crash,
pass or human review. Preserve complete logs before changing their candidate.

The completed v 1.2.1 matrix is a historical regional baseline, not automatic
acceptance of later hooks. Apply the smallest justified tier after offline gates:

| Changed surface | Manual gate |
| --- | --- |
| Documentation/packaging with no runtime effect |Offline verification unless the diagnostic itself needs live evidence |
| Shared policy with unchanged profile/signature/resolver/preflight/hooks/ABI/transactions |Regional corpus plus representative Global high-load visual/stability run |
| Explicit regional mapping/address |Every affected profile after corpus proof |
| Profile selection, resolver, signatures, preflight, bootstrap, detour topology, ABI or transaction |Complete five-profile frozen-candidate matrix |

Failure expands scope and blocks the affected candidate. The tester controls
launch/closure and visual classification; file preparation, hashes and marker
analysis do not replace that judgment. Intermediate Global-only research remains
explicitly outside all-profile compatibility claims.

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
