---
type: Engine Lifecycle Contract
title: External Slice Results
description: Why indices above the native inline result array require generation-safe external
  storage, consumption, and release.
tags:
- shadow-engine
- sliceexecute
- results
- lifecycle
- release
status: stable
sources:
- resource: ../../../evidence/catalog.json#E-c681b34977c2
  title: Corrected-settings .75 safety validation and H8 acceptance
- resource: ../../../evidence/catalog.json#E-650f8fa72d27
  title: H3 correction and unchanged resource-ownership validation
- resource: ../../../evidence/catalog.json#E-ab6fdb75eac9
  title: Positive gameplay, balanced resource ownership and distinct diagnostic defect
- resource: detail-window-observation.md
  title: Explicit Detailed Observation Windows
- resource: periodic-summary-transport.md
  title: Worker-Owned Periodic Summary Output
- resource: ../../../evidence/catalog.json#E-e7bd6b8dce8a
  title: reported-positive72 runtime baseline and measurement scope
- resource: ../../../evidence/catalog.json#E-18fb04261111
  title: Identical ownership across idle recording contended and compiled-out diagnostics
- resource: overhead-measurement.md
  title: Whole-Mod Overhead Measurement
- resource: mod-performance-audit.md
  title: Measuring native patch overhead without confusing it with frame cost
- id: private-v211-result
  resource: ../../../evidence/catalog.json#E-1260c58419aa
  title: v2.0.11 Global runtime and original-v1.2.0 patch-parity audit
- id: private-v120-visual-retest
  resource: ../../../evidence/catalog.json#E-0182a0428c8c
  title: Original v1.2.0 visual retest and source-history comparison
- id: private-result-module
  resource: ../../../evidence/catalog.json#E-6c0b42188e37
  title: External slice-result implementation
- id: private-archived-findings
  resource: ../../../evidence/catalog.json#E-0042fc735065
  title: Historical indexed-overwrite evidence
- id: private-lifecycle-tests
  resource: ../../../evidence/catalog.json#E-29497cb48cfc
  title: External result ownership and ordering tests
- id: private-runtime-corpus
  resource: ../../../evidence/catalog.json#E-ebc961aaf6ec
  title: Regional byte-exact validator
- id: private-v202-rejection
  resource: ../../../evidence/catalog.json#E-3a43ad3ad536
  title: v2.0.2 post-return cleanup runtime rejection
- id: private-v120-comparison
  resource: ../../../evidence/catalog.json#E-62ab90ee39b6
  title: v1.2.0 stable lower-pressure comparison
- id: private-v203-rejection
  resource: ../../../evidence/catalog.json#E-3128dabd182f
  title: v2.0.3 early-consumer runtime rejection
- id: private-v204-result
  resource: ../../../evidence/catalog.json#E-a1fc5b80241c
  title: v2.0.4 native-boundary Global runtime result
- id: private-frame-graph-tail
  resource: ../../../evidence/catalog.json#E-d8ead1fb3b47
  title: Global ExecuteFrameGraph tail disassembly
- id: private-v205-static
  resource: ../../../evidence/catalog.json#E-7696c209b6d3
  title: v2.0.5 static recovery and offline validation
- id: private-v205-result
  resource: ../../../evidence/catalog.json#E-76d1110443ea
  title: v2.0.5 pre-finalizer Global runtime rejection
- id: private-completion-diagnostic
  resource: ../../../evidence/catalog.json#E-4937ea837086
  title: Bounded schedule-to-completion diagnostic
- id: private-scheduler-decompile
  resource: ../../../evidence/catalog.json#E-bc73c25c1787
  title: Global shadow-face scheduler decompilation
- id: private-slice-decompile
  resource: ../../../evidence/catalog.json#E-52c2765db7c9
  title: Global SliceExecute decompilation
- id: private-v207-result
  resource: ../../../evidence/catalog.json#E-a2b709cd31a7
  title: v2.0.7 Global completion-diagnostic rejection
- id: private-v208-candidate
  resource: ../../../evidence/catalog.json#E-cb640de2532e
  title: v2.0.8 corrected completion diagnostic
- id: private-v208-result
  resource: ../../../evidence/catalog.json#E-016ff2c456fe
  title: v2.0.8 Global performance rejection
- id: private-v209-candidate
  resource: ../../../evidence/catalog.json#E-3b9deea1bb66
  title: v2.0.9 lightweight marker-order diagnostic
- id: private-v209-result
  resource: ../../../evidence/catalog.json#E-7a5be4e301e5
  title: v2.0.9 Global marker-order runtime result
- id: private-v210-candidate
  resource: ../../../evidence/catalog.json#E-66499c4207bc
  title: v2.0.10 producer-epoch diagnostic
- id: private-v210-result
  resource: ../../../evidence/catalog.json#E-785bd689215b
  title: v2.0.10 Global producer-epoch runtime result
- id: private-v211-candidate
  resource: ../../../evidence/catalog.json#E-428c7948bd98
  title: v2.0.11 producer-owned lifecycle implementation and validation
- id: public-constants
  resource: ../../../evidence/catalog.json#E-176d7aee808c
  title: Result-store sites and lifecycle state
- id: public-historical-findings
  resource: https://github.com/temdah/Shadow-Engine/blob/2082a3bec1bfc4213ae4572b0e14b4f20c17906b/docs/okf/findings-and-evidence.md
  title: Historical public indexed-overwrite evidence
- id: public-native-cycle-test
  resource: ../../../evidence/catalog.json#E-2347b2daa639
  title: Actual-source producer-cycle lifecycle harness
- id: cloth-result-module
  resource: ../../../evidence/catalog.json#E-2b606cbf5e75
  title: External slice-result implementation
- id: cloth-constants
  resource: ../../../evidence/catalog.json#E-6d95aa568f93
  title: Result-store sites and lifecycle state
---

# Ownership contract

Module 40 owns external result storage. Native SliceExecute keeps indices 0-16 in the 17-qword array at record+0x70..+0xF0; indices 17+ would overwrite unrelated +0xF8/+0x100/+0x108/+0x110/+0x118 fields. Only higher indices are redirected into patch-owned storage. At 30 maps there are 13 external result indices, 17-29.

A record pointer, constructor generation and independent monotonic producer-cycle token identify publication. The existing renderer-queue hook opens that lineage before native scheduling, including synchronous completion. The later builder supplies diagnostic identity only and never resets the publication cycle. Normal consumption occurs at the frame-graph pre-finalizer.

Stores require matching initialized lineage and an open consumer. Each accepted index atomically publishes its pointer and written bit. First completion wins; an arriving duplicate is retired. SliceExecute acquires a nonnull primary before publication, so every rejected nonnull completion still owns one acquisition that must be released, even when pointer values coincide. Both relays carry the exact resource context from queue+0x47458 and rejection invokes the native wrapper with active=0.

Opening refuses an unconsumed prior producer. Reset claims consumer exclusion, verifies no active writers or pending mask, and only then clears lineage. Failure preserves existing pointers/lineage and quarantines new publication; constructor generation advances only after successful reset. Reset does not spin. The bounded active-writer guard at normal consumption remains required. No diagnostic history, native job wait or inferred fence owns these resources.

The written mask is 32-bit; more than 32 external indices requires a new representation and a complete atomic-reader/writer audit.

# Native boundary map

All addresses are Global RVAs unless a profile is stated.

| Boundary | Semantic role |
| --- | --- |
| 0x003E0F80 | CFrameRendererBase::ExecuteFrameGraph. PostCallObjectRenderers schedules this work; it does not establish completion. |
| 0x003E1727 / 0x003E17A6 | Loop collecting 17 native pointers followed by one native wrapper batch call. RBX is renderer, RDI record; following code uses renderer+0x1D8. This is one batch, not 17 wrapper calls. |
| 0x003E1848 / 0x003E18CA / 0x003E1959 | Further resource-wrapper submissions after the first batch. |
| 0x003E19E3 / 0x003E0E70 / 0x003E19F4 | Final sequence loads argument 3 from [RBP+0x68], argument 2 from [RBP+0x60], passes RBX as argument 1 and invokes acquisition/retention finalizer 0x003E0E70; epilogue starts at 0x003E19F4. RDI retains record identity. The patch drains before reconstructing/calling that native sequence. |
| Asia 0x00A584E3 / 0x00A57940 | Independently mapped pre-finalizer boundary/finalizer. |
| 0x003C1350 | Render-record release; rejected as an early normal-consumption point. |
| 0x002D6070; Asia 0x008F0E90 | Per-face scheduler. Argument 3 is queue-entry/result index; argument 4 is face index; argument 5 is inline result base. Synchronous mode calls SliceExecute; asynchronous mode submits a named task carrying renderer, queue and indices. |
| 0x00306E60; Asia 0x00940510 | Complete nested producer loop enclosing scheduler calls. Argument 7 is record+0x70 result base. Existing face-guard hook supplies observation and cycle opening without an additional detour. |
| queue+0x27170 -> +0x47460 | Original -> expanded result-base field written by scheduler. |
| entry+0x20A0 | Face count. SliceExecute publishes resultBase[entryIndex] only on the final face. First 17 entries are native, not first 17 scheduler invocations. |

The historical first-wrapper relay maps to Asia 0x00A582A7. Four available profiles passed 63 exact checks for wrapper/tail placement; later producer-cycle integration passed the then-current 64-check corpus. A4EE's older attestation did not cover the new boundaries and remained manual-required. Static byte proof is not live completion or profile acceptance.

# Accounting and diagnostics

Healthy accounting obeys:

- accepted nonnull + accepted null = consumed results;
- accepted nonnull = normal released resources;
- store failures = rejected nonnull + rejected null;
- rejected nonnull = orphan-release resources + orphan-release failures;
- orphan-release failures, normal-release failures and reset-pending = 0.

After producer-lineage correction, stale/late/rejected paths should normally remain zero. Their occurrence signals degraded handling even when retirement succeeds and no crash is observed. Non-atomic snapshots can differ transiently; neither a difference nor a later balance proves every lifetime boundary.

STAGE_Y_REASONS distinguishes invalid input, missing record, closed consumer, zero generation, unopened cycle, generation mismatch, cycle mismatch, duplicate index and quarantined cycle, plus separate cycle-open failures. frameGraphTailDrains counts boundaries owning external results; frameGraphTailEmpty counts those without a pending mask. STAGE_Z uses lineageKey=constructorProducer; earlier builder-keyed same/changed metrics are not directly comparable.

H2 moved mandatory lifecycle lookup outside the optional diagnostic compile guard in .72. This fixed a source-confirmed uninitialized-pointer defect when telemetry was compiled out; it did not identify a prior Internal failure. H3 history, admission/tail observation and H4 worker output have no ownership authority. Detailed windows are separately bounded and may lose coverage through contention, reuse or timeout without authorizing resource loss. H1 timing never arms H3.

Actual-source validation ran the same 28 ownership scenarios in idle, recording, contended and compiled-out modes with digest 391B292D: 112 scenario-runs, including 84 drained H1 windows in the .74 fixture. The earlier Internal fixture drained 28 active captures. These checks cover early-before-builder completion, all 13 external entries including null, builder preservation, all rejection causes, duplicates, reset/overlap quarantine and exact retirement. They do not prove every native thread interleaving.

# Rejected placements and diagnostic models

| Experiment | Observation | Durable conclusion |
| --- | --- | --- |
| .2 post-ExecuteFrameGraph cleanup | frameGraphCalls equaled reentrant release calls, ending at 55,494; ownership balanced but the process hung with Application Hang 1002. | Post-return wrapper placement is unsafe despite balanced totals. |
| .3 record-release consumer | Two bridge crossings without crash; 20,130 stale and 11 late completions, headlight/shadow flicker plus audio/game stutter. | Record release is too early for normal results. |
| .4 first native wrapper batch | Balanced accepted/rejected ownership; 24,108 rejected nonnull resources retired; no reported crash/freeze/audio/game stutter, but 25,945 stale and 13 late completions. | Retirement contains the leak; first wrapper call is not a complete barrier. |
| .5 pre-finalizer, old lineage | At serial 106,112, 17,496 stale and 10 late results retired with balanced ownership; a late interval rose from 235/1 to 14,439/7 stale/late. Rapid on/off headlights and forward shadow pop-in remained. | Instruction order alone did not prove worker completion; lineage ownership still needed investigation. |
| .7 ordinal-based scheduler correlation | 692,552 scheduled-native, zero scheduled-external and 181,370 unmatched completions. | Per-face call ordinal is not result index; diagnostic zero masks were invalid evidence. |
| .8 corrected entry/final-face correlation | 4,141 scheduled external = 4,093 accepted + 48 rejected, zero overflow, but severe freeze/stutter before bridge. | Index mapping was correct; added per-face VirtualQuery was the leading controlled-difference performance suspect, without profiler attribution. |
| .9 first-observed-face marking | 229,114 scheduled = 192,403 accepted + 36,711 rejected (36,707 stale, four late), exact ownership, no release/orphan/duplicate/reset failure. All entries first appeared after old pre-finalizer/reset markers. | Old diagnostic epoch was misanchored; a wait seeing empty expected masks would not establish a join. First-face latency was under 16 ms, mainly 2-4 ms, and global serial distance was not generation lag. |
| .10 producer epoch | 46,645 starts/seals; 24,509 external-work batches all pending at producer return. Of 219,366 matched completions, 4,868 preceded seal and 214,498 (97.78%) followed it. | Producer return establishes the expected batch, not completion. No observed overlap/active-clear/missing-lifecycle/outside-producer error occurred. |

In .10, lifecycle did not change inside producer calls, but 206,350 completions (94.07%) observed a changed generation/builder marker afterward, near 206,379 accepted results. The 13,016 same-marker completions nearly matched 12,987 rejects (12,979 stale/eight late); the 29-event difference remains race/association uncertainty, not forced one-to-one attribution.

All 107 sampled producers had positive constructor generation and builderCall=0 at entry and return. The old store rejected builder_call<=0 as stale; the later builder reset then initialized that marker. Early current work hitting this zero-builder gate was the leading cause. Producer-correlated pre-finalizer masks were complete in all 107 records and outstanding-generation counts were zero; all 219,366 callbacks matched without unmatched/ambiguous/lagged observations. This superseded .9's inference that the native pre-finalizer preceded the relevant work. It supported opening lineage before scheduling and removing builder reset, not adding a producer wait or changing native expected-job counts.

The .10 intersection black blink added zero stale/late results between marker and recovery; both bridge legs added thousands. That localized visual symptom remained separate. Similar later black-world appearance did not prove the original indexed overwrite persisted.

# Runtime outcome and comparison limits

The first .11 Global run balanced 293,410 scheduled/matched/consumed results: 266,980 nonnull releases plus 26,430 null. Rejected/stale/late/duplicate/cycle-open/reset/release/orphan failures were zero. Every completion retained constructor/producer identity and preceded its correlated pre-finalizer. Headlight flicker was tentatively absent while the intersection symptom remained. Rejected-result cleanup was not exercised and cannot explain that occurrence; no broad crash/stutter/visual acceptance follows.

Original v1.2.0 controls were visually stable at lower pressure but still contained unretired rejections: one 24-map/seven-external/B4=16 run had 527 stale and 11 late; another had 1,365 stale plus 33 late (1,398 rejects) without the reported black flicker or disappearing headlights, though coarse/pop-in shadows remained. These were not controlled scene benchmarks. Reject counts alone neither explain visible differences nor prove old acquisition ownership safe.

Source history separates the unchanged-layout 1.2.1 refactor (24 maps/seven external/B4=16/A8=4), corrected 1.2.3 expansion (30/13/B4=21, following rejected 1.2.2 stride derivation), and 1.2.4 B4=25 increase. The 1.2.4 -> 2.0.0 difference was version-only. Known indexed guards remained; old pre-render repair/sidecar hooks were already uninstalled in v1.2.0. This bounds investigations without claiming complete semantic equivalence.

Corrected .75 Global at 0 / 4096 / 4096 balanced 178,125 nonnull + 36,026 null = 214,151 consumed, with 178,125 releases and zero inspected store/release/lineage/rejection/duplicate/quarantine/cycle-open failures. Earlier concurrent snapshots differed by 5/6 results and 4/5 resources before balance; that is not leak evidence. Twelve tracked vehicle owners had no observed teardown, so this run adds no teardown proof. The positive gameplay report and retained H3 correction close the agreed overhead scope, not all profiles or release readiness. .73 likewise balanced 206,340 results while its separate diagnostic-attribution defect remained.

The older ClothResearch description of builder-owned generation, post-call/release consumption and distinct-pointer submission is superseded by the producer-cycle and per-acquisition retirement contract above. No unique confirmed active lifecycle guarantee is taken from that ancestor.
