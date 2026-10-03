---
type: Internal Diagnostic Contract
title: Explicit Detailed Observation Windows
description: H3 bounds completion, admission and tail detail while preserving continuous safety
  ownership and truthful coverage.
tags:
- shadow-engine
- overhead
- diagnostics
- ownership
- windows
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-c681b34977c2
  title: Corrected .75 runtime, H3/H5 acceptance, H8 closure and settings-continuity request
- resource: ../../../evidence/catalog.json#E-650f8fa72d27
  title: Packaged correction, 516 scope checks, retained ownership and runtime gate
- resource: ../../../evidence/catalog.json#E-ab6fdb75eac9
  title: Positive73 gameplay and H4 with confirmed H3 diagnostic correctness blocker
- resource: ../../../evidence/catalog.json#E-668316df5863
  title: Frozen73 inputs, producer-at-entry contract and correction scope
- resource: ../../../evidence/catalog.json#E-cf7266a4d2fd
  title: Deterministic source reproduction with native passthrough intact
- resource: ../../../evidence/catalog.json#E-e354c7ee5760
  title: Final73 stage evidence, artifact identity and pending runtime acceptance
- resource: ../../../evidence/catalog.json#E-32d759678f10
  title: Full sanitized H3 ownership, correlation and reporting contract
- resource: ../../../evidence/catalog.json#E-e7bd6b8dce8a
  title: Accepted .72 baseline and two 0/4096/4096 cost windows
- resource: ../../../evidence/catalog.json#E-d54c0069d255
  title: Preserved dirty .72 inputs and reviewed H3/H4 design
- resource: ../../../evidence/catalog.json#E-d86512b44ff8
  title: Explicit scalar scope, status and worker control interface
- resource: ../../../evidence/catalog.json#E-4937ea837086
  title: Sole history/window owner, copied reporting and completion matching
- resource: ../../../evidence/catalog.json#E-6658abb69696
  title: Scoped post-native admission observation
- resource: ../../../evidence/catalog.json#E-9a4ab6c06cd6
  title: Scoped tail observations and continuous face protection
- resource: ../../../evidence/catalog.json#E-8e4b6b03d025
  title: Independent action dispatch and existing worker polling
- resource: overhead-measurement.md
  title: Whole-Mod Overhead Measurement
- resource: external-slice-results.md
  title: External Slice Results
- resource: ../../../evidence/catalog.json#E-787e3a2c5e59
  title: Actual-source epoch, control, drain, copied-report and output-failure checks
---

# Accepted scope

The corrected .75 Global run at 0/4096/4096 exercised producer-scope closure
and the separate world-validation change. It records 6,483 starts/seals and zero missing seals, TLS/control-close/overlap
failures or history-reuse losses. All 25 retained generations are sealed with
26 scheduling calls each; the saved frozen report remains unchanged later.
The first .75 run also exercises 32 missed optional seals without closure failure.
No stale-serial runaway recurs. No separate .74 game test or all-profile
acceptance is claimed.

v2.0.73 has positive reported gameplay/stability/quality results, lower sampled
inactive-detail costs and accepted H4 periodic transport in the tested scope.
Its explicit recording exposes a diagnostic correctness defect: a skipped seal
can leave a producer serial active, and later refused producers then add known
scheduling to that old history. This is source-reproduced; the precise live
trigger remains an inference. Permitted missing observations and unknown
asynchronous correlation do not authorize this scheduling attribution.

The v2.0.74 correction separates producer scope/closure from optional history.
Its offline checks preceded the combined .75 runtime validation; no separate .74 runtime test is claimed. v2.0.72 remains the
continuous-observation comparison baseline. The .74 change
uses shared Internal patch code, with no native hook, ABI, regional mapping,
rendering policy or capacity change. The reproducible Internal build, 516 scope
checks, 32156 lookup-oracle comparisons and 112 equivalent ownership scenarios
pass alongside retained regression gates. The combined .75 run supplies the reported runtime/visual gate.

Normal play retains continuous resource/safety accounting and actual owner,
writer, lineage, quarantine, retirement and face protections. Detailed module 19
producer/scheduler/completion/marker history, module 20 admission scans and
module 30 tail checks require an explicit recording. Prior-to-arm history and
all-session detail peaks are not recorded. Tail observation is distinct from
the continuously enforced queue face budget and count restoration.

# State and lifetime

Module 19 owns `ShadowEngineContext.detail_window`, allocated by the existing
tools worker on first detailed recording and retained for process lifetime.
Its epoch never reuses a positive value. OPEN admits new producer records;
DRAINING continues observations for previously admitted producers; FROZEN stops
history mutation and permits copied reporting. No native resource ownership is
stored in the diagnostic window. Record addresses are identity tokens only.

Every production history read/write/reuse uses one short nonwaiting metadata
lock. Admission reads the epoch before acquiring and rechecks it after acquiring.
An entry pointer never escapes that ownership or crosses a native call. Numeric
producer tickets and manager/renderer epoch tickets may cross native calls.
Old tickets reject frozen or mismatched windows. Native scheduler calls occur
after releasing metadata ownership. Contention skips observation and is counted;
it never blocks native execution or changes resource acceptance.

## Producer scheduling scope and return closure

Module 19 owns a dedicated TLS index and process-lifetime atomic active-serial
control cells separately from optional history. The worker initializes TLS at
first recording; it is independent of intersection TLS. TLS stores only a
numeric admitted serial or zero. A stack-owned `DetailProducerTicket` carries
serial, epoch, control-slot index and prior numeric TLS value across the native
producer. No ticket or history pointer is stored in TLS.

Once TLS is initialized, every producer first binds zero, including calls that
cannot admit history. This shadows an outer producer during rejected nested
work. Accepted admission publishes its unique serial. Scheduler attribution
requires that thread's explicit serial and matching record/history; it does not
guess from a record's old active field. Unbound pre-arm work has no admitted
serial, and unique IDs reject old scopes after history rearm. Unrelated records
can record concurrently; the correction does not impose global single-producer
eligibility.

Native return restores prior numeric TLS and closes the control cell with an
expected-serial CAS before optional seal observation. A skipped metadata update
can leave incomplete seal evidence but cannot leave scheduling scope active.
Control cells are not reset with history; an old return cannot clear a newer
serial. The ticket is consumed once. These controls own diagnostic scope only,
never native producer/resource ownership or scheduling.

TLS allocation/read/write failure must stop detailed attribution honestly while
native work continues. A binding failure must suppress the older outer TLS value
before native execution; a restoration failure must disable future attribution
before returning. Return-side control closure still runs when observation is
disabled. Worker freeze/report remains available to describe failure. TLS helper
operations preserve the caller's last-error value. Before first recording there
is no TLS work; after initialization, producer binding/restoration remains
necessary even during inactive detail to preserve nesting/rearm correctness.

Manager admission scans and paired before/after tail checks enter through the
same interface. Post-native checks can retain an admitted epoch during drain;
a renderer ticket does not admit a producer whose actual entry misses the
deadline. Tail diagnostics copy any invalidity decision, release the metadata
lock, then emit urgent evidence. No file I/O holds that lock.

Recording uses the existing 60 s limit and 1.5 s post-mark deadline. Closing stops
new producer admission. The worker polls retained history for seals, completion
masks and markers, then freezes once drained or after a 5 s drain deadline.
Timeout is missing diagnostic coverage; it does not wait for, cancel or reset
native jobs. Storage remains patch-owned. FROZEN rejects history entry, and
callbacks carrying an old epoch or producer serial cannot update a reused
entry. A completion without such a native identity remains subject to the
correlation limits below, including after rearm. Tail/admission pairs can be
incomplete if the window freezes before the returning callback is observed.

# Correlation and reports

Known serial lookup retains v2.0.71's validated ring index. Unknown-ID completion
matching retains the oldest pending search. Completions carry no independent
diagnostic producer ID, so correlation remains heuristic: boundary attribution
is always unknown. When an admission check observes a new unadmitted producer
during drain, it marks that record contaminated; a later completion is excluded
from latency/lag attribution to an older observed batch. Contention can also
leave gaps in observation. Lifecycle identity is diagnostic context, not a newly
invented native fence.

History is `upTo8SlotsPerRecord`, placed by `globalSerialModulo8`. The process-wide
serial can be sparse for one record: serials 1 and 9 reuse the same slot even if
that record has only two generations. This does not promise its latest eight
generations or all-window history. Reusing an unsealed, pending or incompletely
marked entry records lost coverage. Contention, stale epochs, contaminated completions,
unadmitted batches, serial exhaustion and timeout are explicit. Counter totals
remain cumulative over recorded windows, avoiding delayed updates into reset
counter storage. Admission peaks are likewise over recorded windows; last-known
values may be stale and cannot describe current unrecorded play. Zero before
any recording is labelled notRecorded. A contended status snapshot is unknown.

One separate report owner protects a preallocated copied snapshot through
formatting and I/O. Copying happens under metadata ownership; formatting never
does. Output labels open, draining, last-window, busy or notRecorded coverage.
Frozen does not mean saved. Final detailed report success requires its output
and flush without an observed write failure. Failure retains the frozen history
and marks the report failed; ordinary worker polls do not automatically retry
that failed final report.
Explicit finish/report queues a retry. A new explicit recording may replace
failed history once no report is pending, incrementing `discardedFailedReports`.
A pending report or a draining window can refuse a new recording. Report-buffer
ownership remains independent, so an already copied report stays stable while
later live history changes. Reports never claim globally atomic engine state or
complete native job attribution.

# Controls and independent measurements

Actions 7/8/9 retain start-stop, mark and finish/report semantics. Bounded pending
bits preserve these requests across metadata-lock contention; the existing
worker consumes them after acquiring ownership. Repeated requests for the same
pending action coalesce; this is not a command FIFO. They reach both
the detail-window owner and existing intersection owner independently; unavailable
intersection TLS cannot disable detailed observation. Action 9 still requests the continuous safety
report when no detail was armed and cannot recreate prior history.

Action 11 only measures overhead. It never arms detailed observation. Its report
identifies windowed policy, start/end detail phase/epoch, unknown snapshots and
changes since request (including lead-in). Cost comparisons use stable inactive
detail; a separate explicit recording checks diagnostic functionality in the
same acceptance session. The workload progress button describes workload state,
not the detailed recorder's draining/saved state. Lua menu lifetimes and the Global .57 repair remain.

Detail-window tests must exercise idle passthrough, entry/close/drain, late callbacks,
contention, history reuse, timeout, rearm, copied reports and output failure.
The corrected .75 run supplies the runtime/visual acceptance scope alongside
these offline checks. It has one contention, 694 unadmitted batches and 4159
contaminated completions; a missing reset marker yields a bounded drain timeout
before successful saving. These are explicit coverage limits, not native job
failure. Runtime rearm coverage is not claimed.

# Additional diagnostic evidence

The deterministic .73 defect fixture reports firstSerial=1, nextAdmission=0, oldScheduledCalls=2 and outsideProducer=0 while both native calls still execute. The particular missed seal causing the live serial 6508 total of 81,114 calls remains an inference.

The accepted .75 recording lasts 50.078 s, with 34,912 scheduled/matched external results and 18,046 outside-scope scheduler calls. Its bounded drain times out on a missing reset marker before saving successfully. Those figures describe diagnostic coverage, not resource failures. Inactive admission/tail diagnostic means changed from about 5.7/12 us in .72 to 0.08/0.09 us in .73 under different samples; no total-mod CPU or FPS attribution follows. Bridge shadow popping in 40+ car stress scenes remained reported with no proven cause.
