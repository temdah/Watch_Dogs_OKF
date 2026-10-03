---
type: Startup Ownership Contract
title: Delayed Shadow Initialization
description: B1 startup supervision after committed early hooks, with unchanged construction
  and deferred mutation gates.
tags:
- shadow-engine
- startup
- lifecycle
- timeout
- compatibility
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-a594dd95fdf2
  title: Actual worker with virtual time and controlled operations
- resource: ../../../evidence/catalog.json#E-fdebcf63c883
  title: Startup worker and lifecycle supervision
- resource: ../../../evidence/catalog.json#E-1576d48ce50e
  title: One-shot early and deferred transactions
- resource: ../../../evidence/catalog.json#E-f45567a3ad24
  title: Native constructor-owned resource/pass creation and proof
- resource: resource-pass-lifecycle.md
  title: Shadow Resource and Pass Lifecycle
- resource: ../compatibility/nexustools-init.md
  title: NexusTools Early Initialization
- resource: ../compatibility/lua-frame-repair.md
  title: Internal Lua Frame Repair Candidate
- resource: ../../../evidence/catalog.json#E-fea5edb7f171
  title: Sanitized startup ownership and correction contract
- resource: ../../../evidence/catalog.json#E-6cb406222247
  title: Supplied Complete Edition .71 startup sequence
- resource: ../../../evidence/catalog.json#E-8122cb8852a8
  title: Same-PID inactive downstream and quality status
- resource: ../../../evidence/catalog.json#E-08c49de0cb6b
  title: User authorization, source preservation and knowledge lookup
- resource: ../../../evidence/catalog.json#E-360aab196a1f
  title: Global83 continued live verification and full activation
- resource: ../../../evidence/catalog.json#E-6dc601f4ed20
  title: Second Global83 continued live-verification sequence
---

# Confirmed failure and responsibility

Through .76, module 80's sole startup worker exits after 60 s even when the early
transaction committed successfully. Module 70's deferred installer is reachable
only through this worker. Native constructors can run later and create the extra
resources/passes correctly, leaving downstream routing and rendering uninstalled.
This is a startup ownership defect, not evidence that delayed construction itself
is invalid. The supplied .71 Complete Edition runtime exhibits this ordering;
the shared source has the same failure independently of profile number.

Resource/pass creation must remain inside the original native constructor and
registration phase. The correction does not invoke builders late, replay early
patches, move native construction, alter admission/capacity or infer that saved
settings imply rendering is active. The Global-only Lua repair limitation is
separate; an unsupported marker does not establish a Lua crash or explain this
worker timeout. The logs do not identify what delayed construction or prove a
crash or leak.

# B1 correction boundary

The .77 corrective stage retains bounded discovery of a safe early installation
window. Once early hooks commit, their startup supervisor remains responsible
for deferred completion beyond 60 s. One module-pinned worker observes at bounded
cadence; no engine hot-path callback, extra constructor invocation or secondary
installer owner is introduced. A waiting marker distinguishes delayed progress
from completed or terminal startup.

Positive resource/pass invariants and the existing 1 s stabilization still precede
the same deferred installer. Losing the proof during stabilization restarts its
interval. Unsigned tick differences and an explicit armed state handle tick 0
and wrap. Module 70 retains fresh signature/prepared-plan validation, its atomic
one-shot claim and transactional rollback. A failed early/deferred installation
or negative constructor proof is terminal and is never silently retried.

Successful deferred installation is distinct from complete live verification.
The existing manager/profile, capacity and owner-reserve observations still
govern STAGE_M_COMPLETE. Owner reserve may recover in its existing owner; the
supervisor does not reset it, create another owner or reinstall hooks. No runtime
mapping, signature or native patch bytes change for the supervisor correction.

Early commitment cannot safely be undone by deleting resources after native
construction. On a real terminal failure, report retained early state honestly;
do not claim full rollback or successful activation. This fix removes abandonment
solely due to elapsed time, not every possible partial-initialization failure.

Offline checks must exercise the actual worker with virtual time and controlled
early/deferred operations: constructors well after 60 s, slow live verification,
no safe early window, failed proof/signature/deferred transaction, single attempt,
stabilization loss, tick wrap and independent module lifetime. Runtime acceptance
requires both normal startup and the affected delayed-startup case. Offline
profile/corpus checks do not reproduce the reported load timing.

The .77 fixture passes 188 checks with Internal diagnostics and 188 with diagnostics
compiled out. It includes constructors after 180/185 s, final profile proof after 240 s,
proof loss, tick wrap/zero, terminal states and independent worker pin failure.
These results verify the supervisor mechanism, not an in-game compatibility claim.

# Observed failure ordering

The .71 Complete Edition case committed early hooks, reported
`STAGE_M_TIMEOUT` while construction/downstream states were zero, then created
14 nonzero mutually distinct extra handles and 28 distinct added pass slots
inside the 64-slot table. Same-session SE4 quality/downstream/profile stayed zero.
This establishes abandoned deferred startup, not failed resource construction.
A separate .76 Global menu failure had quality readiness 1/downstream 2/profile 2
and no submitted settings, so it was a UI synchronization problem. Modules 60/70
were byte-identical across the supervisor correction. Normal Global startup was
later accepted; reproduction of the affected delayed-startup case remains a
separate unclosed compatibility observation.

Two September12 Global .83 sessions record `STAGE_M_STARTUP_WAITING` at60000ms,
with resource/pass/pass-table/downstream state2 and live profile state0, followed
by both completion markers. This is runtime evidence of continued live
verification after60 seconds. Constructors and downstream installation had
already completed at the wait marker; it does not reproduce the historical
Complete Edition case whose constructors ran after worker abandonment.
