---
type: Runtime Logging Contract
title: Worker-Owned Periodic Summary Output
description: H4 moves ordinary Internal summary output away from engine callbacks with bounded
  copied residency publication.
tags:
- shadow-engine
- overhead
- logging
- worker
- ownership
status: stable
sources:
- resource: ../../../evidence/catalog.json#E-c681b34977c2
  title: Corrected .75 transport validation and H8 acceptance
- resource: ../../../evidence/catalog.json#E-ab6fdb75eac9
  title: H4 runtime acceptance, complete packet delivery and separate H3 correctness defect
- resource: ../../../evidence/catalog.json#E-e354c7ee5760
  title: Final .73 stage evidence and artifact identity
- resource: ../../../evidence/catalog.json#E-fb74a4594c47
  title: Full scalar mailbox, worker ownership and output-failure contract
- resource: ../../../evidence/catalog.json#E-e7bd6b8dce8a
  title: Baseline observed log costs and attribution limits
- resource: ../../../evidence/catalog.json#E-d54c0069d255
  title: Approved second delivery design and preserved source identity
- resource: ../../../evidence/catalog.json#E-38ba6940d5b4
  title: Fixed typed scalar packet and mailbox state
- resource: ../../../evidence/catalog.json#E-3a7cc3374147
  title: Nonwaiting publication, worker copy and failure accounting
- resource: ../../../evidence/catalog.json#E-e88c2f23e9a3
  title: Checked log write result and report flush
- resource: ../../../evidence/catalog.json#E-9a4ab6c06cd6
  title: Existing residency scan cadence and immediate first-use evidence
- resource: ../../../evidence/catalog.json#E-6c0b42188e37
  title: Continuous health counters and removed Internal tail output calls
- resource: ../../../evidence/catalog.json#E-8e4b6b03d025
  title: Existing 250 ms worker orchestration
- resource: detail-window-observation.md
  title: Explicit Detailed Observation Windows
- resource: ../../../evidence/catalog.json#E-b4b7bc8de6b5
  title: Actual-source copied lifetime, callback I/O and failure checks
---

# Copied periodic output

v2.0.73 moves normal Internal Stage-Y/Z periodic checks and output to the existing
250 ms tools worker. Those summaries read process-lifetime patch counters and
require no deferred native reads. Their nominal 30 s cadence remains; worker
scheduling can delay capture/output. A snapshot is not a globally atomic view
of all counters. Manual reports and urgent fault/first-use lines remain
synchronous. No extra worker, hook, rendering or safety behavior is introduced.

The renderer still owns its existing at-most 4 Hz residency scan and 30 s heartbeat
decision. Its queue-derived counts exist only during that callback, so it copies
them into a `PeriodicResidencySummary`, including queue identity as an integer,
capture tick, renderer serial, policy/safety and detail-coverage scalars. Module 14
owns the single fixed `ShadowEngineContext.periodic_summary` mailbox.

# Publication boundary

CAS states are empty, writing, ready and reading. The successful producer owns
the payload until publishing ready. An occupied slot preserves its pending
packet, drops the new attempt and counts it. Publication never waits, allocates,
formats or writes files. It never keeps a pointer for a later native read.

The worker claims ready, copies the packet to its stack and releases the mailbox
before formatting or I/O. A new producer can then publish while the worker is
writing its independent copy. Output includes captured/emitted ticks, delay,
accepted/drained counts, full drops and failed-packet accounting. A checked log
return detects failed open/write/short write. A failed packet is counted once
even if both its body and transport metadata fail. There is no automatic retry,
because a failed write may already have emitted a prefix. A later record can
expose the cumulative failure count; process exit can lose pending best-effort
periodic output. Explicit report durability retains its separate flush boundary.

The mailbox is not a global FIFO with manual or urgent lines. Copied older
records may appear after newer synchronous evidence; capture/emission metadata
is part of their interpretation. Admission fields describe cumulative recorded
windows and can be stale. The `STAGE_F_RESIDENCY` payload independently includes
`admissionCoverage` and `latestMayBeStale=1`, so losing its separate transport
metadata cannot turn a recorded-window value into apparently continuous
coverage. No recording is `notRecorded`; unavailable detail status is `unknown`,
regardless of epoch. Transport metadata repeats the coverage and adds timing,
drop and failure accounting. Resource safety counters remain continuous.

# Verification and scope limits

Actual-source fixtures free the original queue and poison source counters before
drain, verify no ordinary callback file I/O, exercise writing/ready/reading/full
refusal and publication during worker output, inject open/write/short-write/
metadata failures and verify no retry. First-use output stays immediate.

This removes ordinary periodic formatting/open/write/close from Internal engine
callbacks. It does not eliminate logging cost, promise scheduling latency, move
manual/urgent evidence, or prove that previous stutter was caused by logging.
Copied periodic transport was exercised in the corrected .75 Global test at 0/4096/4096. All 13
accepted residency packets were drained and written, with zero full drops or
write failures and recorded delivery delays of 0-250 ms. The user reports that
the game looked and ran good, with no new visual or stability issue reported.
The separate H3 .74 correction was exercised in the combined .75 run; no standalone .74 test is claimed.
Full-slot/write-failure behavior remains supported by offline checks. Neither
this result nor copied counter snapshots establish future latency bounds,
process-exit durability, all-profile acceptance or a causal FPS improvement.

Historically, H4 first received runtime acceptance in v2.0.73 within the user's
reported test scope. That session recorded 15 accepted and 15 drained packets,
zero full drops and write failures, and successful output for every packet. Delivery delay is
15-203 ms, with a 110 ms median; every residency payload independently carries
its admission coverage and staleness fields. Full-slot and failed-write paths
were not triggered here and remain offline verification. These observations do
not establish a maximum future delay or process-exit durability.

The .73 user report described no stability issue or quality/stability regression
and perceived better driving performance. That .73 report did not validate the separate producer-scope defect;
the .75 correction has the narrower evidence recorded above. Release's old fallback remains retained;
these Internal results do not promote a Release binary.

The .72 comparison captured two logging calls at approximately 348 us each in one window and none in another. This proves sampled call cost only, not sustained per-frame expense or the cause of past stutter. H4 moves that ordinary callback I/O cost to the existing worker; it does not remove it.
