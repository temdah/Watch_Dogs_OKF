---
type: Reverse Engineering Status
title: Watch Dogs 1 High-FPS Player Movement Investigation
description: Global character-controller stage mapping and the experimental primary-update 30
  Hz policy.
tags:
- shadow-engine
- movement
- character-controller
- havok
- high-fps
status: draft
sources:
- id: boundary-report
  resource: ../../../evidence/catalog.json#E-98ce8b7e86f8
  title: WD1 high-FPS player movement boundary recovery
- id: wd2-reference
  resource: ../../../evidence/catalog.json#E-9ea89cb32838
  title: Local Watch Dogs 2 high-FPS movement reference
- id: character-xrefs
  resource: ../../../evidence/catalog.json#E-032e69dcdbb8
  title: Global character-controller type-name cross-references
- id: vcall-inventory
  resource: ../../../evidence/catalog.json#E-a02b6d7f9f34
  title: Global virtual-call 0x98 inventory
- id: v2019-runtime-rejection
  resource: ../../../evidence/catalog.json#E-47b2c21d7943
  title: v2.0.19 Global missing-world and crash result
- id: recovered-job-stages
  resource: ../../../evidence/catalog.json#E-941549486b04
  title: Global character-job stages and crash-RVA decompilation
- id: v2020-runtime-rejection
  resource: ../../../evidence/catalog.json#E-8fb4f4bfbc5d
  title: v2.0.20 Global fall and crash result
- id: v2021-runtime-rejection
  resource: ../../../evidence/catalog.json#E-a8047560d90b
  title: v2.0.21 Global inside-body fall and crash result
- id: lower-boundary-recovery
  resource: ../../../evidence/catalog.json#E-968d1376e40a
  title: Global lower movement timestep boundary
- id: lower-cfg-recovery
  resource: ../../../evidence/catalog.json#E-b0a2000dd7e1
  title: Global lower movement reachable-CFG and callee classification
- id: implementation
  resource: ../../../evidence/catalog.json#E-28a61a7ba052
  title: Experimental player movement policy
- id: validator
  resource: ../../../evidence/catalog.json#E-5f5144475e97
  title: Global movement scheduler validator
---

# Watch Dogs 1 High-FPS Player Movement Investigation

## Problem and scope

the tester reports that identical circular running input produces a tight circle at
30 FPS and a much larger circle at high frame rates. The effect already exists
at 60 FPS, making 30 Hz the requested reference cadence. This is a separate
engine subsystem from Aiden's SecondaryMotion coat solver.

## Knowledge lookup result

Private/public OKF, current source, SystemSurvey evidence, archive provenance,
the mapped Global runtime, and the local WD2 reference were searched for
character-step, controller, locomotion, strafe, circle, Havok, player transform,
and delta-time boundaries. The WD2 exact signatures have zero WD1 matches and
do not prove a portable address or prototype.

## Global function map

The `CCharacterControllerJob` record identifies Global RVA `0x0272EAC0` as a
whole-controller job. It reads a stable controller pointer at job `+0x130` and
a float delta at `+0x138`, then forwards that delta to all three native stages:

- `0x027292F0`: primary controller update and movement/timer consumption;
- `0x02729490`: collision/contact processing; and
- `0x026CC230`: final controller state/output and timer processing.

The input job record owns its delta for the duration of the synchronous call.
The controller pointer is the per-instance clock identity. These are static Global roles; the rejected interventions below independently
confirmed hook activation without validating their policy.

## v 2.0.19 rejected policy

v 2.0.19 retains cloth v 2.0.18 and adds a separate hook at `0x0272EAC0`. It
accumulates submitted time per controller and executes the complete original
job at fixed 30 Hz, preserving coherence across the three stages. Intervening
high-FPS jobs are skipped. The job delta is temporarily replaced with
`0.033333335`, then restored after every native call.

Safety limits are a 256-slot bounded clock table, oldest-slot replacement,
`0.066666670` maximum accepted input contribution, at most two substeps per
submission, exact Global prologue validation, a separate rollback transaction,
and native fail-open behavior for invalid job/controller/delta memory. The
initial scope includes every controller using this job; no player-only
classifier is claimed.

Runtime rejects this complete-job scheduler. The first attempt loaded without
the world or minimap; the second briefly loaded with Aiden falling through the
world and then crashed. The preserved log proves the hook installed, and
Windows records `0xC0000005` at Global RVA `0x01648C2D`. The faulting function
is not a direct character-job callee, so the exact crash instruction is not
claimed as a movement call-chain proof.[^v2019-runtime-rejection]

Static recovery establishes the mechanism error. Each submitted job performs
native job bookkeeping, primary movement, collision/contact, and final
state/output work. v 2.0.19 skipped all of it on intervening submissions and
could call the entire job twice for catch-up. A complete job therefore owns
one required native completion per submitted job; it is a coherent delta
carrier but not a suppressible scheduler boundary.[^recovered-job-stages]

## v 2.0.20 rejected shared-delta policy

v 2.0.20 invokes the original job exactly once for every valid submission. Its
per-controller accumulator supplies `0.033333335` seconds on a 30 Hz major
step and zero on intervening refresh calls, then restores the incoming delta.
The primary movement stage statically guards its movement body behind positive
delta, while collision/contact and final state/output still execute. Missed
whole periods are discarded rather than duplicating a submitted job.

Runtime rejects this policy too. the tester again saw Aiden beneath the loaded world
with the world visible above him, followed by a crash. Windows recorded the
same `0xC0000005` fault at Global RVA `0x01648C2D` as v 2.0.19. Calling the job
once was insufficient because replacing its shared delta also passed zero to
collision/contact and finalization. The `0x0272EAC0` detour and all job `+0x138`
writes are retired.[^v2020-runtime-rejection]

## v 2.0.21 primary-only policy

v 2.0.21 hooks only primary update `0x027292F0`, with arguments `(controller,
float dt, job-local)`. Its per-controller accumulator supplies `0.033333335`
on a 30 Hz major step and zero on intervening primary calls. The native function
guards its movement body for non-positive delta. Caller/job memory is never
read or written, so collision `0x02729490` and finalization `0x026CC230` receive
the untouched native delta. Every primary call is invoked once, invalid input
fails open, and missed periods are discarded rather than burst.

Runtime rejects this boundary too. the tester loaded inside Aiden's body beneath the
world and then crashed. The log proves the primary hook installed. Even with
native delta retained for collision, zero-step primary state was incompatible
with its consumers. Windows attributed this crash to an unknown module/address,
so no exact engine call chain is claimed.[^v2021-runtime-rejection]

v 2.0.22 removes the movement module from the unity build entirely: no movement
state, hook binding, preflight, installation, F9 capture, or shutdown capture
ships. All character-controller stages and deltas are native. The circle-radius
defect remains unresolved; future work must recover lower turning/radius math
that can be corrected without cadence-gating a controller stage.

## Lower steering search

Static recovery proves primary update `0x027292F0` forwards its native float
timestep to `0x02727FF0`. A 499-instruction reachable-CFG recovery shows the
incoming value is preserved until the end of the lower update: it computes
`1/dt` at `0x027287D0`, stores current `dt` at controller `+0x188` at
`0x027287D7`, and stores reciprocal `dt` at `+0x18C` at `0x027287EE`. The
preceding work therefore does not directly use the current argument through
those fields; any same-update consumer would see their previously stored
values.[^lower-boundary-recovery][^lower-cfg-recovery]

Neighbor `0x027277A0` reads `+0x188` and bounds a timestep-scaled controller
value before iterating 0x40-byte states. This proves it is a timestep consumer,
not that it owns steering. Its apparent table reference at mapped VA
`0x7FFC4012BA08` is `.pdata` unwind metadata, not a gameplay vtable. No movement
hook is present in v 2.0.26.

The first recovered direct callees in `0x02727FF0` are Havok collision,
support/contact collection, and stale-contact maintenance. They use collision
extent and contact state but do not expose player yaw or turn-radius arithmetic.
This narrows the active search away from those helpers and toward upstream
desired-motion/orientation input or the unresolved consumer dispatch for
`+0x188/+0x18C`. The previous-frame storage ordering is a credible lead, not a
proven explanation of the large-circle defect. The latest coat-only runtime
test adds no movement values because movement telemetry was intentionally
absent.[^lower-cfg-recovery]

The .26 coat tracer includes no movement intervention or telemetry. A safe
movement correction still requires proven player yaw or desired-orientation
ownership; the previous-frame dt store is only a lead.

## Validation state

Mapped-image, source-policy, 30/60/120/280 Hz convergence, reproducible-build,
validation proved v 2.0.21 was wired as intended, but
runtime rejected it. v 2.0.22's rollback guard and reproducible build prove the
movement experiment is absent. Player-only classification and the lower
turning boundary remain unproven. Other profiles remain outside intermediate
testing until public-release mapping.

[^v2019-runtime-rejection]: v 2.0.19 Global missing-world and crash result
[^recovered-job-stages]: Global character-job stages and crash-RVA decompilation
[^v2020-runtime-rejection]: v 2.0.20 Global fall and crash result
[^v2021-runtime-rejection]: v 2.0.21 Global inside-body fall and crash result
[^lower-boundary-recovery]: Global lower movement timestep boundary
[^lower-cfg-recovery]: Global lower movement reachable-CFG and callee classification
