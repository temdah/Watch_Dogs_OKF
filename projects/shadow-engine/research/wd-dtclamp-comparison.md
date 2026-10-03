---
type: Reverse Engineering Review
title: WD_DTCLAMP versus the coat fixed-step experiment
description: Pinned external source review, Global hook mismatch, and limits of accumulator
  clamping versus secondary-motion scheduling.
tags:
- shadow-engine
- cloth
- timestep
- havok
- external-review
status: draft
sources:
- id: external-source
  resource: https://github.com/Open-Source-Modding/WD_DTCLAMP/blob/b09e900e160f8a90f5f3837e507344030760ab8e/dtclamp.c
  title: WD_DTCLAMP pinned source reviewed without execution
- id: cloth-policy
  resource: cloth-high-fps-investigation.md
  title: Watch Dogs 1 High-FPS Coat Physics Investigation
- id: cloth-source
  resource: ../../../evidence/catalog.json#E-a3a09f241a70
  title: Current experimental cloth scheduler and nested solver gate
- id: global-image
  resource: ../../../evidence/catalog.json#E-b1f432b717f7
  title: Preserved Global mapped runtime image, private evidence
- id: havok-provenance
  resource: ../../../evidence/catalog.json#E-c55e439c44be
  title: Historical Havok names and unresolved live coat connection
---

# Scope and knowledge preflight

The comparison pins external commit`b09e900e160f8a90f5f3837e507344030760ab8e`
and the separate cloth source. Existing Havok job/type names are provenance,
not proof of live coat ownership. External code was neither built nor executed.

# Intended external mechanism

The author labels RVA `0x026E2C50` in `Disrupt_b64.dll` as a
WorldStepHavok job accumulator addition. Source requires exactly
`F3 0F 58 51 20`, or `addss xmm2,[rcx+0x20]`. Intended arithmetic is:

```text
xmm2 = min(xmm2, 0.03333333333)
xmm2 = xmm2 + float_at(rcx + 0x20)
xmm2 = min(xmm2, 0.03333333333)
```

This is an upper clamp, not a 30 Hz scheduler. It has no wall clock, phase
accumulator, call-frequency gate, source classifier, force filter, output
replay or animation-rate cap. Finite values whose sum stays below the ceiling
remain unchanged. If the value represents accumulated elapsed time, clipping
it discards excess accumulated time; the source does not establish downstream
substeps or consumers. The world-job role is author-claimed, not independently
mapped here, and a connection to coat or steering remains unproven.
[^external-source]

# Separate cloth mechanism

The separate cloth worktree retains accepted v 2.0.23/v 2.0.18 behavior; v 2.0.26
adds only output-owner tracing. Global adapter `0x00C16ED0` always executes.
A QPC phase clock keyed by the stable source record selects fixed 16.666668 ms
major solves at at most 60 Hz, without burst catch-up. Its synchronous solver
gate at `0x00C16BD0` runs original integration on a major; between majors it
calls publisher `0x00C168E0` using actual solver arguments 1 and 3, without
integration. Scope uses live coat-resource plus type-0/130-node classification;
this is not a global Havok policy or a proven exclusive resource-to-solver link.
[^cloth-policy]

Acceleration filtering (alpha 0.125) advances only on major steps through a
private source-value copy. Context timestep changes are serialized and exactly
restored. Animation remains native; replay is not proven to hold the previous
solved pose coherently. Hands-in-pockets phasing remains unresolved. Different
animation and cloth rates are a plausible synchronization concern, not a
confirmed diagnosis or evidence that animation itself must be capped.
[^cloth-source]

# Static blockers in the reviewed external source

1. **Global target mismatch.** A read-only seek to RVA `0x026E2C50` in the
  mapped Global image yields `48 8B 07 8B D3`, not the required five bytes.
  Its own guard would reject this image. Image timestamp is `0x5CD045B4`,
  SizeOfImage and file length are `0x06595000`; SHA256 is
  `5F4259790890B52F3B05825572E93D3DB3932D3E470EA4BE8DB5DCB4E9E5ED6D`.
  No claim is made about other profiles or the semantic role of this mismatched
  location.[^global-image]
2. **Trampoline layout errors.** Counting the declared bytes gives second
  MINSS end `0x15`, indirect JMP start `0x15`/end `0x1B`, float `0x1B`, pointer
  `0x1F`, total `0x27`. Constants/comments instead use `0x14`, `0x1A`, `0x1E`
  and size `0x26`. The JMP displacement write at `+0x16` overwrites its ModRM
  byte (the actual displacement starts `+0x17`). Second MINSS also calculates
  RIP from the wrong end offset. The indirect JMP displacement targets the
  game return address rather than the inline slot containing that address.
3. **Unvalidated reachability.** `VirtualAlloc(NULL,...)` does not guarantee a
  trampoline within signed 32-bit displacement range; both entry E9 and
  RIP-relative loads cast displacements without validating range.
  These are static source defects, not observed crashes in a tested ASI.
  The external source was neither built nor executed.[^external-source]

# Conclusion and operating boundary

This repository supplies a different, upstream accumulator-clamping hypothesis,
not evidence that our coat fix should be replaced. Its inspected source is not
a verified working Global alternative. Correct runtime mapping and detour
construction, then live input/consumer evidence, would be prerequisites to
evaluating that hypothesis. No runtime experiment validates this external hypothesis.

[^external-source]: Pinned external source, lines 1-9, 32-59, 64-114.
[^cloth-policy]: Private cloth investigation, accepted v 2.0.23 and v 2.0.26 boundary.
[^cloth-source]: Cloth module, scheduler and adapter/solver hooks.
[^global-image]: Private mapped image read and SHA256 on 2026-08-31.
[^havok-provenance]: Prior HCL pivot distinguishes type/job names from live coat ownership.
