---
type: Validation Reference
title: Offline Refactor Gates
description: Source-equivalence, regional corpus, transaction, and reproducibility checks before
  runtime testing.
tags:
- shadow-engine
- validation
- reproducibility
- rollback
status: draft
sources:
- id: compiled-release
  resource: ../../../evidence/catalog.json#E-4876b4762f69
  title: Compiled PE exports, version and release policy checker
- id: equivalence-test
  resource: ../../../evidence/catalog.json#E-e36d4c66ae9b
  title: Refactor equivalence validator
- id: transaction-test
  resource: ../../../evidence/catalog.json#E-820b9a555189
  title: Transaction fault-injection test
- id: corpus-test
  resource: ../../../evidence/catalog.json#E-ebc961aaf6ec
  title: Regional runtime corpus validator
- id: main-release-workflow
  resource: ../../../evidence/catalog.json#E-6df38af71cae
  title: Main-branch installable release workflow
- id: cloth-fixed-scheduler-test
  resource: ../../../evidence/catalog.json#E-846d584e50de
  title: Cloth fixed-rate scheduler validator
- resource: ../../../evidence/catalog.json#E-9848c23a92f8
  title: Refactor equivalence validator
- resource: ../../../evidence/catalog.json#E-1cb9f190a794
  title: Transaction fault-injection test
- resource: ../../../evidence/catalog.json#E-ec0b5999a154
  title: Regional runtime corpus validator
- resource: ../../../evidence/catalog.json#E-6f54d2e97f8e
  title: Main-branch installable release workflow
- id: cloth-diagnostic-test
  resource: ../../../evidence/catalog.json#E-2dbe625a8957
  title: Cloth diagnostic corpus validator
---

# Required validation by mechanism

Use actual-source native harnesses, source contracts, independent byte/layout
checks and warning-clean reproducible TinyCC0.9.27 win 64 builds through
`build.ps1`. Tests prove only their exercised mechanism; offline success never
establishes injected execution, rendered fidelity or in-game performance.
The [regional matrix](regional-runtime-matrix.md) sets the manual tier.

- Preserve shared policy, complete profile signatures and the Asia explicit map.
 Unknown/ambiguous builds remain read-only and fail closed.
- Relocation expectations must be derived independently from the candidate:
 all 46 source sites retain their own0x24C0/0x24C4/0x24C8 region stride.
- External results 17–29 require drain before the reconstructed finalizer, exact
 rejected-result retirement, first-wins duplicate handling and a 32-bit written
 mask. Publish the native resource wrapper before relays are callable.
 Record release and post-frame-graph-return code are not normal consumers.
- Mutation fault injection proves reverse-order restoration and allocation
 cleanup. Two clean official builds must be byte-identical where required.
- Capacity/layout/relocation or regional addresses require the
 [runtime corpus gate](runtime-corpus-gate.md), followed by the justified manual tier.
- Current finite selection, quality, queue validation, publication, settings,
 startup, driver identity, copied diagnostics and Lua host/register behavior
 require their owning actual-source/frozen-reference fixtures. Do not replace
 behavioral equivalence with source spelling assertions or synthetic timing.
- `validate_release.py` inspects the compiled x64 PE without loading the DLL:
 exports/ordinals, version and fixed policy. Redistributable CI gates complement
 locally held proprietary corpus evidence; CI success is not regional runtime proof.

# Historical gate definitions

| Gate | Frozen boundary |
| --- | --- |
| Equivalence |Accepted v 1.2.1 policy and ABI |
| `--capacity-target-v123` |B4=21/A8=4, 30 maps, 31 entries, 28 external pass slots, 13 external results |
| `--policy-target-v200` |Same 30/31/28/13 layout with B4=25/A8=4; historical experiment, not current B4 value |
| `--lifecycle-hotfix` |PostCall removal, exact-context rejected cleanup and one inline pre-finalizer relay; exactly two added Global RVAs and independent Asia mappings for boundary/native target |
| `--intersection-diagnostic` |Three lookup calls, three builder stores and target/prologue: seven additional checks, 71 per usable image versus 64 baseline in the .12 gate |

Historical lifecycle validation had 79 Asia mappings and a separately recorded
88-check Asia gate. Counts identify those validator revisions, not a current
promise that the test suite has a fixed size. The .12 milestone recorded 38 Python
tests; .15 release preparation recorded 51 plus lifecycle/intersection/rollback
native harnesses. The current source/test inventory remains authoritative.

The separate cloth fixed-rate experiment independently models 120/240Hz inputs
converging on60Hz major solves, no long-gap catch-up burst and suppression only
inside the exact intended adapter/solver gate. Movement 30/60/120/280Hz convergence
passed offline while every controller intervention failed runtime; mathematical
scheduler convergence is not engine safety or visual acceptance.
