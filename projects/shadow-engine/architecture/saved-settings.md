---
type: Settings Ownership Contract
title: Persisting mod policy without blocking native callbacks
tags:
- shadow-engine
- settings
- persistence
- diagnostics
- lifecycle
status: draft
sources:
- id: retired-policy-migration
  resource: ../../../evidence/catalog.json#E-shadow-baseline-20261004
  title: Retired experiment removal and settings migration fixtures
- id: background-query-review
  resource: ../../../evidence/catalog.json#E-19eafa0c5c81
  title: Occlusion-query mapping and bounded background-quality experiment
- resource: ../../../evidence/catalog.json#E-54ba79f66f80
  title: Global 80 Unlimited and quality setting changes
- resource: ../../../evidence/catalog.json#E-72f305a1f5ef
  title: Subsequent Global startup restores saved revision 17
- resource: startup-supervision.md
  title: Delayed Shadow Initialization
- resource: ../../../evidence/catalog.json#E-e0c193d30c44
  title: Explicit state, request and status interface
- resource: ../../../evidence/catalog.json#E-0244013502e9
  title: Validation, persistence, publication and worker lifetime
- resource: ../../../evidence/catalog.json#E-4d0df9a99489
  title: Policy decoding and control routing
- resource: ../../../evidence/catalog.json#E-8e4b6b03d025
  title: Session transport and terminal result reporting
- resource: ../../../evidence/catalog.json#E-fdebcf63c883
  title: Common initialization before policy consumers
- resource: ../../../evidence/catalog.json#E-4cf6a0b742b3
  title: Native-driven menu values and pending changes
- resource: ../../../evidence/catalog.json#E-b6e7111dd577
  title: Immediate hydration and one owned queued polling callback
- resource: ../../../evidence/catalog.json#E-7f26b934ad93
  title: Actual-source persistence and transport fault fixtures
- resource: ../../../evidence/catalog.json#E-1d96748bfdb8
  title: Menu lifetime and acknowledgement fixtures
- resource: control-api.md
  title: 'Asynchronous native control ABI: request, receipt and application'
- resource: ../compatibility/lua-frame-repair.md
  title: Internal Lua Frame Repair Candidate
---

# Ownership and startup

This case study describes Shadow Engine's native persistence worker. It owns
one pending scalar request, a short copy token, an event and bounded paths.
Settings load outside DllMain before policy consumers start. Engine callbacks
and Lua submit copied choices; neither native pointers nor Lua objects enter
the saved record. Only the worker waits for its token, which never spans file I/O.
Worker, pin or event failure rejects changes while preserving the loaded state.

# Validate, save, then publish

The `SESAVE2 revision policy world` record has an exact trailing LF. Parsing
checks overflow, token count, embedded NUL, signs, trailing bytes, known bits,
valid cap/count combinations and positive revision. Invalid input remains intact
until a valid replacement succeeds. Missing or unreadable records select the
defined fallback; a fallback is not reported as a successful load.

The worker merges only fields explicitly changed by the request, validates the
complete result, writes a bounded temporary sibling, checks write/flush/close,
and atomically replaces the destination. Only then does it publish policy and
increment revision. Failure retains the previous applied/saved values. A crash
after replacement but before publication loads the new record on the next start.
Revision saturation rejects instead of wrapping.

Two policy words are separately atomic; their publication is not one engine
transaction. Limiter changes reset mod-owned residency under its own token;
quality-only changes do not. Resource allocation, resizing and visibility remain
separate engine operations.

# Format migration experiment

An older SESAVE1 record used a remembered count of 10 for two meanings. SESAVE2
adds an explicit Unlimited marker. An active old 10 normalizes to Unlimited;
a disabled old record remembering 10 remains disabled. Loading does not rewrite
the file or increment revision, repeated startup has the same interpretation,
and an identical request remains a no-op. The next real edit writes the applicable current format.

The recorded Global 2.0.80 run saved two revisions and restored the latter on the
next startup. This proves those recorded choices and persistence, not every
legacy migration or finite-limit case. Actual-source fixtures separately exercised
format validation, migration, replay, worker failures and persistence failures.

# Lua synchronization lesson

The inspected host's `SH_Commands_SetStateInt` invokes the registered callback,
including unchanged values and deferred dispatch. Hydrating a widget can therefore
look like a new edit. A persistent observed-value guard distinguishes echoes;
newer unobserved edits survive an older save result. Native status is authoritative,
and session changes discard old presentation state. See
[host callback behavior](menu-host-compatibility.md) and the
[control ABI](control-api.md). Saved revisions do not prove a rendered change.

# Historical background setting version ownership

The .89 experiment assigns policy bits20..21 to Off/512/1024 and change mask32
to the background setting. SESAVE1/2 reject those bits, so malformed older
records cannot activate it. SESAVE3 accepts them and preserves the existing
limit/cap invariants. Older valid files load with background Off without rewrite.
An enabled background choice writes SESAVE3; explicitly switching Off writes
SESAVE2 again. This permits older-build settings compatibility after an explicit
Off save; an older parser presented with enabled SESAVE3 instead falls back.
Legacy partial edits preserve the background field because unrequested fields
remain owned by the saved record. Save failures preserve both active policy
and the previous file. Actual-source restart, format/range and failure fixtures
cover these rules; in-game persistence acceptance is separate.

# Removing a persisted experimental field

The .91 cleanup removes the background policy from the runtime, while retaining
a bounded SESAVE3 reader. It validates the retired two-bit field as0..2, then
discards only those bits before applying the ordinary policy/world invariants.
Reserved value3 and unrelated unknown bits still reject; SESAVE1/2 never gain
ownership of the retired field. Existing limit, quality, world choice and revision
survive loading. Startup performs no replacement or revision increment; the next
real edit writes SESAVE2. Retired change-mask32 and SES3 transport requests return
rejection without queueing a write. Actual-source tests cover both build profiles,
nondefault choices, reload, unchanged disk bytes and normal edits. This is an
offline migration result, not in-game persistence acceptance.[^retired-policy-migration]

[^retired-policy-migration]: Preserved pre-cleanup source and actual-source baseline fixtures; both native builds reproduce offline, with no game acceptance inferred.
