---
type: Internal Diagnostic Contract
title: Shadow Population Boundary Observation
description: Explicit bounded candidate, native eligibility, cache and renderer observation
  without changing shadow policy.
tags:
- shadow-engine
- population
- diagnostics
- ownership
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-407b79f6acdb
  title: Global87 automatic population save and lifecycle log
- resource: ../../../evidence/catalog.json#E-077cac7a56c4
  title: Global87 whole-pass population binary
- resource: ../../../evidence/catalog.json#E-823b1ce9b172
  title: Whole-pass194827-check native fixture and independent binary decoder result
- resource: ../../../evidence/catalog.json#E-1f061093e0ec
  title: Actual-source6343-check independent-control and fresh-permission-scope result
- resource: ../../../evidence/catalog.json#E-3724261dfc5f
  title: Global85 unmarked population tail, native boundaries and coverage/cost limits
- resource: ../../../evidence/catalog.json#E-196e85308760
  title: Actual-unity6062-check population fixture result and evidence limits
- resource: ../../../evidence/catalog.json#E-4a5cc55d22b8
  title: Actual-unity copied-field, native-equivalence and reporting fixture
- resource: ../../../evidence/catalog.json#E-31bc887a44c2
  title: Reproducible TinyCC fixture invocation and retained-image hash gate
- resource: wd1-shadow-eligibility.md
  title: WD1 Shadow Eligibility and Work Boundary
- resource: shadow-pressure.md
  title: Shadow Pressure Boundaries
- resource: headlight-resource-diagnostics.md
  title: Headlight Shadow Resource Diagnostics
- resource: vehicle-shadow-selection.md
  title: Vehicle Shadow Selection Diagnostic
- resource: ../../../evidence/catalog.json#E-251cc00fccb7
  title: Optional immutable field proof and copied-input gate evaluator
- resource: ../../../evidence/catalog.json#E-84862c41208e
  title: Population history ownership, copied records and worker output
- resource: ../../../evidence/catalog.json#E-6658abb69696
  title: Original candidate, actual kept list and post-native binding boundaries
- resource: ../../../evidence/catalog.json#E-9a4ab6c06cd6
  title: Native requests, quality-adjusted requests and returned resource boundary
- resource: ../../../evidence/catalog.json#E-8e4b6b03d025
  title: Existing explicit recording controls and worker polling
---

# Purpose and interpretation

The P-A observer supplies the inputs missing from earlier population captures.
It distinguishes candidate presence, actual patch keep decisions, copied native
eligibility inputs, native bindings, cached update decisions and submitted queue
work. It changes no admission predicate, scheduling rule, capacity, selection,
quality or resource lifetime. It installs no additional detour. Release excludes
the observer and its optional profile proof data.

Reconstructed eligibility is a **pre-budget copied-input result**, never an
executed branch trace. Native output is recorded independently. A passing gate
does not prove successful binding allocation, a cached binding can legitimately
skip new queue work, and a CPU resource request is not GPU or visible readiness.

# Field proof and synchronous borrowing

An optional immutable runtime-profile record supplies offsets and exact byte
spans. The Global record independently covers the new manager inputs, context
lookup, binding and cached-owner consumers; constants are checked as bits.
Observation refuses absent or changed proof, leaving existing engine behavior
intact. A matching hook prologue alone does not authorize these extra fields.
Other profiles have no population proof until independently mapped.

The manager copies original candidates before filtering, then the actual kept
list before native admission. Its post-native copy observes bindings and the
fresh current owner vector. Every borrowing scope validates its own spans;
cached addresses from before the native call are not dereferenced afterward.
Counts, alignment, pointer arithmetic and bounded capacities are explicit gates.

Rows retain full descriptor handles and, when publication is coherent and fresh,
copied vehicle tokens/full entity IDs. Ambiguous, future, stale, contended or
incomplete publication remains unknown. The observer acquires the existing
selection token without changing selection gap counters. Its scratch snapshot
and index belong to the one admitted population writer.

Cache identity at owner+78 is a native32-bit key. It cannot replace a full
descriptor or vehicle identity. Post-native bindings associate copied candidates
with aligned slots in the freshly validated current vector. Identical before/
after keys do not exclude an unseen clear/rebind, and owner+80 is initialization
policy rather than a completion fence. The pressure concept owns the scheduling
semantics; observation does not force a refresh or retain a texture.

The renderer copies dimensions before quality, actual requests after quality,
and CPU resource results after native submission. It never follows dropped
trailing entry pointers. Manager and renderer call numbers are separate
observations: full handles and time support comparisons, not a fabricated causal
call identifier. Same-address backing/resource values do not prove allocation
generation, resizing or lifetime beyond the current synchronous call.

# Recording ownership

Action14 starts one60-second whole-pass recording; action16 can stop it early.
The worker stops and saves automatically at the deadline. The menu needs no
reaction-time mark. Native action15 remains an optional annotation and never
shortens the window. Actions7/8/9 retain the independent black-world/flicker
capture. Start refuses an active or saving population window.

Each independent stream owns1200 absolute50ms buckets. The first successfully
reserved callback in each bucket is retained; later callbacks are counted as
rate-skipped, with no overwrite and no catch-up burst. Missing buckets and
contended callbacks are separate counts. Manager packets copy at most512
candidates and8 cache owners; renderer packets retain the existing31-entry
bound. Raising the diagnostic row bound does not change native capacity.
The fixed patch-owned storage is below128MiB, allocated/reset by the worker on
explicit Start and retained for process lifetime. Idle callbacks do no scanning.

A stream ticket owns its packet across native execution. The ticket identifies
the session and absolute bucket; sequence counts admitted samples. Reservation
precedes packet clearing, so the later begin timestamp can cross a bucket
boundary. There is no diagnostic lock across native execution. Stored addresses
are numeric tokens, never deferred pointers. Reporting/reset waits for both
in-flight native calls to return; an unreturned call can leave saving pending.

Callbacks copy raw floating-point bits and MXCSR. The offline decoder
reconstructs gates from these inputs; the stored gate-result slot remains
unknown. No new floating-point evaluation, allocation, log formatting or file
write runs in a game callback. Observer QPC intervals exclude reservation and
packet clearing and are neither pure CPU cost nor a complete perturbation bound.

QPC determines buckets and elapsed time. The unsigned tick deadline also bounds
the window if QPC fails. A clock anomaly sets partial and clock flags, preserves
raw timestamp values and makes derived timing unavailable; automatic expiration
still reports60 seconds and1200 expected buckets. An early stop retains the
actual elapsed window. Expected buckets include every touched bucket; gaps do
not prove missing shadows or failed native work.

# Whole-pass file and completion

After tickets drain, the worker writes a unique
`ShadowEnginePopulation-<pid>-<UTC-filetime>-<serial>.bin` beside the ASI using
CREATE_NEW. Existing files are preserved. Every complete retained packet is
written as its fixed numeric prefix plus exactly its copied rows. No live state
object or unused candidate storage is serialized. The text log contains concise
coverage/save summaries, so its former16MiB population-row budget cannot
truncate the binary timeline.

The little-endian schema1 contract is defined in
[the format include](../../../evidence/catalog.json#E-e0bc55c568c7):

| Record | Contract |
| --- | --- |
| Header192bytes, magic `SEPOP01` plus NUL | Explicit schema/endian/layout sizes,512/31/8 row bounds,1200 buckets,50ms period,60000ms window; process/session/serial, QPC frequency/start/stop, UTC FILETIME, actual stop reason, counts/skips/gaps and optional annotation. |
| Record header24bytes | Type1 manager or2 queue; header size, absolute bucket, payload bytes, admitted-sample sequence, zero reserved field. |
| Manager payload |576-byte prefix including before/after cache copies, then exactly copied-count168-byte candidate rows. |
| Queue payload |72-byte prefix, then exactly copied-count112-byte queue rows. |
| Footer64bytes, magic `SEPOEND` plus NUL | Schema, counts, exact byte totals, flags/expected buckets and CRC32/IEEE over header plus all records, excluding footer. |

Header/footer flags are bit0 optional annotation, bit1 partial coverage and bit2
clock anomaly. Partial includes missing bins or incomplete candidate/queue
censuses; each individual field's validity remains authoritative even when the
aggregate flag is clear. Maximum valid file size is108221056bytes. Header,
packet padding and reserved bytes are zero. Full64-bit identities, signed
cache ages, raw float bits and both independent call counters survive export.

Worker polls limit output to32 records, 1MiB of records and approximately20ms per batch;
a conservative size check occurs before the next record, with up to64 extra
footer bytes. The time threshold is checked between records. A single record,
flush or filesystem call can exceed them. Open, short/full write, flush and close
failures cannot receive a saved receipt. An incomplete file may remain for
failure diagnosis. Save also requires a successfully flushed END summary;
`STAGE_POPULATION_SAVE_RESULT` distinguishes artifact success from summary
failure and never claims its own durability. Main-log rotation is independent
of the preserved binary file.

The standard-library
[decoder](../../../evidence/catalog.json#E-e0aea2f2e861) validates a bounded
immutable file snapshot, exact record layout/counts/tickets, completion footer
and CRC before producing summary JSON or optional complete JSONL rows. It
rejects truncated, corrupt or unsupported files. Timing derived from anomalous
clocks remains unavailable. Native bindings, reconstructed eligibility and CPU
resource observations remain different evidence types.

SE9 preserves the29 SE8 fields and appends window milliseconds, sample
milliseconds and native elapsed milliseconds. The menu shows a countdown,
automatic saving and the matching serial's saved/partial/failure result. An
unmarked whole pass is normal. Tools87 accept older SE7/SE8 for established
settings/diagnostics but require SE9 for whole-pass population controls.

Queue copying retains a fresh stack readability-region cache per before,
prepared and after-native phase. Permission results never survive the native
call. Before-resource validation preserves the original helper's complete
candidate/backing/resource spans, including partial-valid and null behavior.
This lowers redundant queries without changing copied fields or native policy.

# First runtime evidence and diagnostic correction

The Global .85 report saved completely with256 manager and256 queue packets,
zero writer skips and no output suppression. It was unmarked:6983 calls occurred
over the recording window, but6727 overwritten packets leave only the final
approximately2.073 seconds. Complete report output does not restore that earlier
history or associate the retained tail with a visible onset event.

The retained observer intervals averaged0.313ms per manager call and1.436ms per
queue call, with peaks0.8504ms and2.6891ms. These QPC scopes can include scheduling
and exclude reservation overhead; they are neither pure CPU cost nor FPS. Saving
used70 batches with1.726 seconds summed active elapsed time and40.015ms peak;
the between-batch worker sleeps add wall time. The .85 unscoped queue copies
repeated region queries per field. The scoped phase-local copies above address
that measured observer burden; the separate .87 scopes below provide runtime
observations, not a controlled same-scene speed comparison.

The .85 coupling to flicker actions also allowed a second detail window while
the first population report was still saving; its accepted legacy receipt did
not start a second population window. Separate controls and SE8 status remove
that ambiguous control/completion relationship. The eligibility and pressure
concepts own the native admission and refresh findings from the retained tail.

# Global .87 whole-pass result

The first whole-pass runtime file validates its complete schema,2400 records,
31705344-byte length and CRC32 `43749EB8`. Both streams retain every bucket0..1199:
1200 packets each from8100 attempted callbacks,6900 intended rate exclusions,
zero contention, missing bins, clock anomalies or output-partial flags. A single
Start completes automatically without an annotation. The native saved receipt
and SE9 session/serial match the binary; file flush/close and summary flush pass.

Manager samples span10.4457..59950.1177ms after Start, and queue samples span
11.6338..59950.8415ms. Maximum gaps between actual sampled starts are71.1812ms
and70.5035ms despite complete bucket coverage. Native-call numbers remain
independent; equal time buckets do not establish call lineage. Worker deadline
recognition occurs after the fixed sampling window, so stop QPC can exceed60s.

Every manager census is complete, with47..297 candidates and no512-row clipping.
The disabled limiter keeps all165520 copied candidates. Admission copying is
valid in all1200 packets; full vehicle-identity publication is healthy in1188,
with4 gap-marked and8 overflow-marked packets retaining explicit uncertainty.
The eligibility, pressure and resource concepts own their respective conclusions.

Recorded observer intervals total459.4033ms manager and64.0522ms queue, means
0.38284ms and0.05338ms per selected callback, with peaks0.9996ms and0.2994ms.
These intervals exclude reservation/clearing, can include descheduling and do
not measure FPS. Export uses76 worker batches,86.230ms summed active elapsed
and7.766ms peak batch; inter-poll sleep adds save wall time.

Continuous face counters record peak29/30 requests with no clamps or dropped
entries. Recorded lifecycle failure/rejection/stale/late/duplicate counters stay
zero. A manual report balances122343 nonnull releases plus24238 null results
against146581 consumed results. Later live snapshots may include in-flight work.
The separate H3 detail window was not armed, so its empty history does not prove
queue-tail or visual acceptance. A full sampled pass does not identify an exact
visible headlight or prove GPU completion.

# Acceptance boundary

Actual-source fixtures must establish optional proof rejection, copied field
semantics, malformed memory handling, identity ambiguity, native output/list
equivalence, bounded storage and ticket/drain lifetime. Static image proof and
synthetic fixtures do not establish visual acceptance. The finite register
requires a manually driven whole-pass capture and a visual report before
selecting a rendering correction. An exact event mark is not a progression gate;
sampling gaps and lack of exact visual correlation must qualify any inference. Presentation FPS is independent of this evidence boundary.

The .86 actual-unity fixture established6343 checks for independent proofs,
native outputs, list restoration, fresh permission scopes and separate controls.
The whole-pass extension passes194827 native checks covering first/last-bucket retention,
rate-skip versus contention accounting, tick-wrap/clock-failure handling,
automatic no-mark completion, native-call drain, full512-row payload export and
truthful file failure handling. Nine independent decoder test groups check exact numeric
round trips against four C artifacts and reject corruption/truncation. Synthetic results do not execute
the game or establish runtime observer cost, visual improvement or GPU readiness.
