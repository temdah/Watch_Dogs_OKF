---
type: Internal Diagnostic Contract
title: Bounded Shadow Workload and Presentation Capture
description: Five-second in-memory workload comparison with worker-state notifications and preserved
  session evidence.
tags:
- shadows
- performance
- diagnostics
- vehicles
- etw
status: draft
sources:
- resource: detail-window-observation.md
  title: Explicit Detailed Observation Windows
- resource: periodic-summary-transport.md
  title: Worker-Owned Periodic Summary Output
- resource: ../../../evidence/catalog.json#E-e88c2f23e9a3
  title: Previous-session rotation, append fallback and report flush
- resource: ../../../evidence/catalog.json#E-8e4b6b03d025
  title: Worker-owned capture status publication
- resource: ../../../evidence/catalog.json#E-b6e7111dd577
  title: Request-scoped menu notifications
- resource: incoming-vehicle-readiness.md
  title: Incoming Vehicle Shadow Readiness
- resource: ../../../evidence/catalog.json#E-f91ce7e5358a
  title: Capture ownership, sampling and worker output
- resource: ../../../evidence/catalog.json#E-1e3416db155c
  title: Process-scoped Windows presentation event consumer
- resource: ../../../evidence/catalog.json#E-0d61335f10ac
  title: Minimal Windows x64 tracing ABI
- resource: ../../../evidence/catalog.json#E-03fe02e150a3
  title: Independent Windows header layout checks
- resource: ../../../evidence/catalog.json#E-f4a82f305d4e
  title: Actual-source bounded sampling and synthetic presentation tests
- resource: ../../../evidence/catalog.json#E-11709f6daf7f
  title: Actual-source pairing, failure ownership and ordinary-user private DXGI delivery tests
- resource: ../../../evidence/catalog.json#E-06ca149b8e66
  title: Passing fixtures and actual ordinary-token private DXGI transport, all probe calls
    occluded
- resource: https://learn.microsoft.com/en-us/windows/win32/etw/configuring-and-starting-a-private-logger-session
  title: Microsoft private in-process trace permissions and file consumption
- resource: https://learn.microsoft.com/en-us/windows/win32/etw/logging-mode-constants
  title: Private in-process sequential mode and incompatible realtime mode
- resource: https://learn.microsoft.com/en-us/windows/win32/etw/configuring-and-starting-an-event-tracing-session
  title: Microsoft trace session configuration and ownership
- resource: https://github.com/GameTechDev/PresentMon/blob/main/PresentData/ETW/Microsoft_Windows_DXGI.h
  title: Intel DXGI event provider and Present start/stop declarations
- resource: https://github.com/GameTechDev/PresentMon/blob/main/PresentData/PresentMonTraceConsumer.cpp
  title: Named DXGI properties and runtime presentation interpretation
- resource: ../../../evidence/catalog.json#E-c681b34977c2
  title: Corrected .75 runtime, H3/H5 acceptance, H8 closure and settings-continuity request
- resource: ../../../evidence/catalog.json#E-650f8fa72d27
  title: Passed .74 offline gates; no standalone runtime test claimed
- resource: ../../../evidence/catalog.json#E-ab6fdb75eac9
  title: Positive .73 gameplay and H4 with confirmed H3 diagnostic blocker
- resource: ../../../evidence/catalog.json#E-e7bd6b8dce8a
  title: reported-positive72 runtime baseline and measurement scope
- resource: ../../../evidence/catalog.json#E-06078fbd86b8
  title: 69 three-window measurements, lifecycle and duplicate notification finding
- resource: ../../../evidence/catalog.json#E-ddb6d6bf0c6b
  title: 68 cost split, complete0/4 windows and protected10 native omissions
- resource: ../../../evidence/catalog.json#E-e19e149211e9
  title: Completed67 windows, harsh4-limit selection cycle and clean lifecycle
- resource: ../../../evidence/catalog.json#E-67fea055e0bb
  title: Preserved67 runtime capture
- resource: ../../../evidence/catalog.json#E-0b7bf602c2fb
  title: Capture reliability scope and knowledge lookup
- resource: ../../../evidence/catalog.json#E-f1081166c00e
  title: Surviving66 startup log after reported launcher restart
- resource: ../../../evidence/catalog.json#E-61f2d4dbd0b6
  title: reported's65 downstream and bypass vehicle capture
- resource: ../../../evidence/catalog.json#E-e35092dcfa55
  title: Downstream boundaries and capture drain preflight
- resource: ../../../evidence/catalog.json#E-e419c1365822
  title: Six64 workload windows in10/4/0 repeated order
- resource: ../../../evidence/catalog.json#E-1a8b7ae4af61
  title: reported's63 movement and0/10 workload captures
- resource: ../../../evidence/catalog.json#E-554eb2f6c301
  title: reported completed62 workload and two-car movement captures
- resource: ../../../evidence/catalog.json#E-cbf42da6d1aa
  title: Sanitized implementation and interpretation contract
- resource: ../../../evidence/catalog.json#E-14251a5e5830
  title: Knowledge preflight and retained invariants
- resource: ../../../evidence/catalog.json#E-16ccb9c14e8c
  title: Preserved Global parent computation and native cadence
---

# Current capture contract

Internal action 11 uses a three-second lead-in and five-second recording window,
with 50 manager and 50 queue slots at10Hz. The original .62 ten-second/100-slot
shape is historical. Release excludes this capture. Worker-owned process-lifetime
memory contains copied scalar records; hooks use nonwaiting admission and sample
at most once per 100 ms bucket. Native pointers exist only in synchronous scratch.
Idle capture hooks check state; a busy request never restarts active storage.

Manager observation copies/classifies before the preparation timer, even at
limit 0, providing comparable coverage but potentially warming caches or changing
publication contention. Observer time does not include every measurement effect.
Queue records distinguish entries/faces, exact recent vehicle type 1/type 3 handles
and owners, other types, unknown and ambiguous. Unknown identity does not prove
world ownership; admission never proves acquired/visible/GPU-completed work.
Worker output includes aggregates and at most 80 representative movement rows;
counts are per sampled call, not frames. Coverage/settings changes are explicit.

H1 overhead instrumentation shares action 11 but has independent arming/tickets/
calibration/drain. It never arms H3 detail. Detail phase/epoch and changes since
request, including lead-in, accompany results; unknown state remains unknown.
Normal periodic output uses the existing worker before reporting. Both reports
must be emitted without observed write failure and flushed before success.
The [measurement](overhead-measurement.md), [detail](detail-window-observation.md)
and [periodic transport](periodic-summary-transport.md) concepts own their state.

# Capture lifetime and durable reporting

Action 11 now samples five seconds after the same three-second lead-in, with 50
slots per stream at10Hz. Downstream and turnover measurements below remain.
No resource-completion or GPU-visibility attribution is added: admitted queue
entries do not prove displayed shadows. Use the retained engine/intersection
reports alongside workload and vehicle captures for remaining omissions.

Worker-owned notice states are 1 lead-in, 2 sampling, 3 draining, 4 saved, 5 save
failure. The capture serial and notice introduced in SE4 remain in current
[SE6 status](saved-settings.md). The original capture watcher observed only explicit requests at most once
per wall-clock second; later settings hydration owns its separate polling path. Notifications follow worker state,
not a guessed countdown; scheduling can delay them. Session changes cancel the
watch, repeated states do not repeat notices, and unload clears it.

Worker report output still waits for every sampled native-call ticket and ETW
cleanup. Saved is published only after output has no observed write errors and
FlushFileBuffers succeeds; failure has a distinct notice. Slow/in-flight native
work delays readiness rather than resetting memory used by an active sample.
No new render-thread file I/O or diagnostic lock across native work is added.

Startup moves the prior main log to ShadowEnginePatch.previous.log before
creating the new main log. Only one previous session is retained. A failed move
other than missing source opens the main log in append mode instead of erasing
it; SESSION_BEGIN records cleanLog=0 and rotationError. Repeated relaunches can
replace the one backup; this is not unlimited archival or crash-proof logging.

Actual-source tests exercise rotation, locked-backup append fallback, successful
report flush and locked-log failure. The desktop Lua fixture covers state/dedup,
busy/save-failure/session change, no idle/startup polling and retained controls.
It does not certify the game's modified Lua VM; live testing remains required.

# Native-call tickets and copied turnover

The bounded captures time
the original native manager, original renderer submission and candidate-list
restoration separately. Timings are CPU wall intervals including possible waits;
they are not GPU completion or frame time. Manager/renderer intervals may nest
and must not be added. Only sampled calls execute these QPC measurements.

Each sampled operation owns a numeric slot ticket reserved under the capture
lock. No lock is held across native execution. An in-flight counter prevents
worker reporting or subsequent capture reset until all tickets return. State
is patch-owned/process-lifetime; no native pointer is retained by the ticket.
An outstanding call delays the report, not native execution. Completion writes
its exclusive slot before releasing the drain count.

Queue samples copy full type 1/3 handles and known vehicle-owner tokens. Worker
compares adjacent valid samples as sets, ignoring order. It reports observed
additions/removals, not all transitions between samples, cache misses, resource
rebuilds or visibility. Unreadable/missing handle/ambiguous samples invalidate a
pair. Unknown vehicle provenance is not world classification; known-owner
turnover is explicitly partial. No rendering resource is retained or changed.

New DOWNSTREAM and TURNOVER records accompany the existing preparation summary.
 Synthetic tests cover in-flight drain,
no-lock timing, idempotent ticket release, reset exclusion, full-generation set
differences and invalid-pair rejection. Runtime observer cost remains a separate measured gate.

# Presentation timing

The .84 FPS1 diagnostic replaces the access-denied realtime session with an
own-process private sequential ETL session (mode0x20801). Microsoft documents
this private scope for ordinary users; private mode cannot use realtime
consumption. No privilege change, Present detour, stack walking or system-session
fallback is introduced. The worker starts it during lead-in, with QPC timestamps,
64 KiB buffers (requested2..8) and an8 MiB file limit. There is no kernel PID
filter; private in-process scope and an explicit consumer PID check provide scope.

Each request exclusively creates a uniquely named directory beside the owning
module and owns its fixed capture.etl child. The immutable path is separate from
ETW's in/out properties: a real Windows STOP cleared that properties filename.
Only after stopping its own session does the worker open the completed file and
start one ProcessTrace consumer. It drains that thread and closes its own handles
before deleting its file/directory and unloading the API modules. Start rejects
live session/thread/consumer ownership. Stop/close failure retains ownership and
prevents reuse; failed file deletion retains the owned directory and is retried
before another directory can be created. No existing directory is adopted and
no other session or file is cleaned. Process termination may leave a bounded
orphaned file; crash-proof file cleanup is not claimed.

TDH reads named properties, not guessed payload offsets. Only version0 x64
Present42/43 pairs with non-test flags and resultS_OK contribute start-to-start
intervals. A start inside the window may complete during the short stop tail;
an unmatched pending start makes the result invalid. This avoids accepting an
unknown last result or silently discarding a failed final Present. Statistics
are read only after the consumer thread exits.

Reported presentationFPS is application successful-Present cadence, **not
displayed FPS or GPU duration**. Setup/file/consume/cleanup errors, empty or full
files, event/buffer loss, failed/occluded presents, missing metadata, pending or
out-of-order pairs, overflow, multiple swapchains or fewer than two intervals
invalidate FPS/mean (-1). Logs retain validity, pending count and storage errors;
CPU workload reporting remains independent when presentation capture fails.
Renderer-call rate is never substituted. The1 ms histogram's final bucket is
open-ended (>=101 ms): p95OpenEnded=1 with upper bound0 explicitly replaces the
old misleading102 ms bound. Invalid p95 fields are0.

Actual-source fixtures cover pairing/coverage and setup, stop, consumer, close,
file and reuse failures, including STOP clearing the filename. A real ordinary
Windows token delivered12/12 custom-provider events and64 DXGI events for32
headless Present calls, with zero setup/consume/file/loss errors. All32 calls
were correctly classified occluded; this proves private DXGI delivery and
ordinary-user transport, not non-occluded game FPS or visual acceptance.
CPU callback time excludes provider/file cost. The bounded trace adds temporary
file I/O and its game-time measurement effect remains to be assessed.


# Movement and distance interpretation

Adjacent valid representative full-handle/owner samples use publication intervals
50–500 ms with both observations≤200 ms old. Difference of square-root distances
over publication time is linear distance rate: negative approaching, positive
receding. This differs from the earlier four-window squared-distance derivative
(50–2000 ms). Neither measures receiver visibility or every intervening transition.
No retained native pointer is used to calculate these rows.

Global parent`0x0099E5D0` calls entity-position reader`0x0082E610`, takes the
first object under`0x03B78508`, calls`0x006A5480`, subtracts returned+0C/+10/+14
from vehicle XYZ, squares/sums and forwards through native cadence to batch
`0x0093D730`. This was initially an unnamed native-reference lead. The later
Global player-position proof is in [incoming readiness](incoming-vehicle-readiness.md);
other profiles retain native-reference semantics. Update cadence and a fresh
join alone do not establish first-visible shadow timing.

# Historical measurements and failed evidence capture

All reported values below are CPU wall-time microseconds unless stated. Scenes
and candidate memory layouts evolved; comparisons do not isolate a causal
speedup. Native intervals may nest and must not be summed as frame/GPU time.
ETW attempts in these runs failed with access-denied 5, so no logged FPS exists.

| Build and limits | Preparation | Native queue | Mean faces | Other evidence |
| --- | --- | --- | --- | --- |
| .62: 1/0/10 |683.818/0.992/701.345 |Not sampled |15/26/26 |100+100 each; exact queue owners 1/9.75/9.35; observer 78–91 ms/10 s excludes unmeasured cost. Skipped includes already-filled slots, not missing scheduled samples. |
| .63: 1/0/10 |393.091/0.345/577.505 |Not sampled |15.07/26/26 |Owners 2.07/9.43/9.04; suppression 41.56/0/76.72; candidates 90.98/132.69/136.93; degraded 0/0/2, zero fail-open; playerAnchor1. Up to 3 readability queries per candidate (411 at 137) was a concrete source cost. |
| .64: 10/4/0 twice |87.624/91.821/0.350; 73.233/76.782/0.331 |Not sampled |26/20.49/26; 26.01/20.88/26 |Owners 9.52/4.25/9.78; 9.58/4.45/9.76. Copy 35.945–53.137, snapshot 8.672–9.968, classify 18.267–19.865, select 8.648–9.185; queries 46.02–67.64/hits 239.83–286.86. No sampled fail-open/degraded/ambiguous/unreadable. |
| .65: 0/4/10 |0.477/86.520/88.450 |748.220/621.751/721.026 |26/21.94/26.01 |Manager 2.444/1.659/1.805; restore 0.036/0.423/0.375.99 adjacent pairs: handle adds 54/8/63, removals 53/8/63; owner adds/removals 28/4/21. Observer 138.876/133.187/138.021 ms/10 s. No sampled failure or large demonstrated turnover storm. |
| .67: 0/4/10 |0.596/76.278/76.370 |679.824/591.032/686.820 |26/21.86/26 |50+50 each; no fail-open, one degraded 10 sample.89,058 results balanced, zero lifecycle/clamp failures. At 4 all protected lamps admitted, but 18.45-unit owner excluded/readmitted; 7/8 snapshots use 5/6 slots. |
| .68: 0/4 |0.506/78.378 |598.552/488.048 |26/21.48 |Ownership+classification 22.310 versus .67's 31.920, copy 45.368 versus 34.422.12 detailed 4 samples admit all protected lamps; 8 detailed 10 omit 1–4 despite fresh 0–16 ms joins, native 26 total/4 cached.4 uses≤1 extra.89,079 results balanced. |
| .69: 0/4/10 |0.500/65.914/55.522 |596.770/472.104/586.038 |26/20/26 |At 4 copy 33.106 and queries 20.98 versus .68's 45.368/43.20. No sampled fail-open/degraded, 18 cumulative gap-epoch degraded calls. Four queue owners/no sampled turnover at 4.106,452 results balanced. |
| .75 corrected 0/4096/4096 |H1 categories separate |Nonadditive |50+50 samples |World 320 valid/642 calls, mean 29.796250/median 28.8/p 95 41.9. Inactive admission/tail about 0.069/0.097; frozen detail phase 3/epoch 1.6,483 H3 starts/seals, no scope failures. First 4/2048/Original window excluded from active-world benefit. |
| .77 accepted quality/settings |No causal FPS result |Not isolated |23 entries/26 faces |Saved revision 4 at 0/4096/4096; each quality pass skips 743,567 under-cap and inspects 41,674, optional-proof unavailable 0.50+50 samples, 212.22 candidates/48 candidate owners/11.10 queue owners; no sampled suppression/failure/degradation/unreadable. Peak 29, no drops.154,478 nonnull+30,817 null =185,295 consumed, releases balanced. |

The .66 test data was lost from the current main log after a launcher relaunch:
only a 4,228-byte fresh startup survived, with no workload/vehicle records and no
session backup. The tester reported completing captures except the engine report;
the surviving file proves neither a crash nor failed original capture execution.
This motivated the five-second workflow, true worker-state notifications and
one previous-session log backup. A separate reported limit 0 disappearance remains
unattributed: 0 bypasses selection, not every native admission/resource policy.

Uncontrolled overlay reports (.59: 0/1/4/10≈136/152/136/120FPS; .60 quality 4:
10≈130, 4≈140–142, 1≈150, 0≈145; .63: 0≈140–145 versus 10≈120 s) are observations,
not log measurements. They do not isolate CPU/GPU cost. Lower submitted faces
at 4 and unchanged 26 at 0/10 explain why filtering more owners need not improve FPS.

The .62 delayed-near-car report showed native admission in samples 0/1 and outgoing
exclusion in 2/3, with 0–16 ms publication; it did not capture first-visible onset.
The .65 design had forecast extras before outgoing/current-near demand; .66
changed extras to actual-near/outgoing/spare-forecast without proving every
visual case. A parked-car visible shadow disappearing during passing traffic
and high-speed 40+ car pop-in remain population/receiver continuity questions.
No saved capture demonstrates a GPU-ready fence or a universally slow buffer.
