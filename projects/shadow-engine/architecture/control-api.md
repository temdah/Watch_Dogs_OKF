---
type: Technical Reference
title: 'Asynchronous native control ABI: request, receipt and application'
status: draft
sources:
- id: background-query-review
  resource: ../../../evidence/catalog.json#E-19eafa0c5c81
  title: Occlusion-query mapping and bounded background-quality experiment
- resource: ../../../evidence/catalog.json#E-8e4b6b03d025
  title: Native request dispatch and SE9 status projection
- resource: ../../../evidence/catalog.json#E-4cf6a0b742b3
  title: Strict SE7/SE8/SE9 presentation parser
- resource: population-observation.md
  title: Shadow Population Boundary Observation
- resource: ../../../evidence/catalog.json#E-569c6b85c180
  title: Preserved historical technical evidence
---

# Interface scope

These are Shadow Engine exports, not native Disrupt APIs. They illustrate a
versioned interface between a Watch Dogs Lua extension and mod-owned native
policy. The recorded 2.0.87 implementation exposes API version 2:

```c
unsigned int ShadowEngine_GetControlApiVersion(void);
int ShadowEngine_GetVehicleHeadlightLimiterEnabled(void);
int ShadowEngine_SetVehicleHeadlightLimiterEnabled(int enabled);
```

Setter return 1 means a request was accepted by the worker. It does not mean the
configuration was saved, applied, admitted by the renderer, or visible. Return 0
means invalid, busy or unavailable. The getter reports the last applied state.
No file I/O runs inside the export. Version-1 callers expecting synchronous
application are incompatible with this contract.

# Session-bound scalar transport

The file request format `SES2 pid session sequence mask limit vehicleQuality
worldQuality` contains copied scalar intent. PID/session validation rejects a
previous process, and sequence checks reject replay. A recognizable invalid
request in the active session gets a terminal result and receipt so the caller
can leave its pending state. Wrong-session input cannot advance state.

The Lua side keeps one request in flight, coalesces later edits and retries the
same sequence. Native status separates receipt, result, saved revision and
applied revision. Results distinguish saved/queued, unchanged, invalid, busy,
save failure and unavailable. Acknowledgement is not persistence proof.

The Boolean API cannot express every newer policy. In the recorded protocol,
0 disables suppression, 1–9 select a finite traffic count, and 10 means Unlimited.
Enabling a remembered count of 10 through the Boolean setter rejects rather than
inventing a finite count. Explicit protocol/version checks prevent an old caller
from silently selecting a different policy.

# Capture completion is independent

SE9 status extends earlier layouts with the population recorder's duration,
sample period and elapsed time: 60,000 ms, 50 ms and the observed elapsed time.
Matching session, serial and saved state establish which report completed.
A countdown reaching zero, request receipt, or another recorder's completion
does not certify that output was saved. Partial data and write failure stay explicit.

Persistence is described in [saved settings](saved-settings.md); recorder
ownership and sampling limits are in [population observation](population-observation.md).
These interfaces are useful implementation examples, not evidence of GPU readiness.

# Host compatibility status

The .88 SE10 status retains all 32 SE9 fields and appends `hostCompatibility`:
0 pending, 1 explicitly mapped host, 3 unknown host, 4 host layout/startup window
unavailable, 5 optional game Lua sites unavailable. Value 2 is reserved. The
33-field parser validates protocol and range; updated tools also accept SE7,
SE8 and SE9. Old fixed-width readers must not misinterpret appended fields.

Compatibility is separate from shadow readiness. A warning does not claim
successful startup. It is deduplicated by process/session/state and stays visible
on the Shadows page. See [the host update case study](../compatibility/nexustools-init.md)
for mapped 1.1.13 support, fallback behavior and remaining runtime limits.

# Background quality transport

SE11 preserves all33 SE10 fields and appends the background index:0 Off,1 512,
2 1024. Its34-field parser validates the range; new tools still parse SE7–SE10
and withhold background edits on older engines. SES3 requests contain process,
session, sequence, change mask, limiter, vehicle quality, world quality and
background quality. Allowed user masks are combinations of1/2/4/32; privileged
raw policy masks remain unavailable to this transport. SES1/2 keep their existing
contracts and cannot claim mask32. Acknowledgment remains receipt, not a saved
or applied result. Revisions/results and value reconciliation cover the new
field just like the existing settings. No callback waits for file I/O.
