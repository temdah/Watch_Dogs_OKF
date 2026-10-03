---
type: Reverse Engineering Reference
title: Watch Dogs 2 Shadow Architecture Reference
description: Successor-engine responsibilities that inform WD1 hypotheses without supplying
  portable offsets or layouts.
tags:
- shadow-engine
- wd2
- reverse-engineering
- backport
status: draft
sources:
- resource: ../architecture/vehicle-light-provenance.md
  title: Vehicle Light Component to Renderer Provenance
- resource: ../architecture/incoming-vehicle-readiness.md
  title: Incoming Vehicle Shadow Readiness
- id: wd1-source
  resource: ../../../evidence/catalog.json#E-f45567a3ad24
  title: WD1 engine expansion implementation
- resource: ../../../evidence/catalog.json#E-d9694ed25b9c
  title: WD1 engine expansion implementation
---

# Use

Successor-engine research separates vehicle-owner selection, shadow-only lamp
eligibility, general renderer admission, static-map refresh and shadow-strength
rendering. These responsibilities guide WD1 investigation; none is a drop-in
implementation or a claim that a future port has been runtime validated.

The recovered CPU selector is not evidence of a timed N+2 handover. A native
distance-fade value reaching lighting parameters does not prove temporal
replacement fading, dithering, incoming GPU readiness or independent siren
resource pools. Special-class sorting after admission is not vehicle ranking.
The exact successor mappings are retained in the focused [WD2 technical
reference](../architecture/wd2-shadow-reference.md), with static evidence and
non-portability limits. Proprietary binaries and raw captures are not included.

# Boundary

Addresses, object layouts, constants, and call contracts are not portable
between the games. A WD2 observation is architectural evidence only until a
matching WD1 allocation, writer, reader, index, and lifetime path is recovered
independently.

Before moving the WD1 limiter earlier, prove a shadow-only consumer and native
publication ownership without suppressing illumination or unrelated lights.
Maintain generation-safe identity, current-scene invalidation and uncertainty
passthrough. Evaluate total work removed, not only a cheaper hook after shifting
the same work elsewhere. Rendered-shadow caching and atlas changes are outside
the current plan. Existing runtime behavior remains unchanged by this research.
