---
type: World Light Policy
title: Pequino Secondary Streetlamp Shadow Exclusions
description: Marker-derived exclusion of lower-lamp casing shadows while retaining illumination
  and upper lamps.
tags:
- shadow-engine-addons
- world-lights
- marker
- regression
status: draft
sources:
- id: evidence
  resource: ../../evidence/catalog.json#E-a742b12c714f
  title: User scope, marker resolution, family comparison and mutation boundary
- id: selection
  resource: ../../evidence/catalog.json#E-bdbf68e4cb28
  title: Exact 80 definitions and 426 placements
- id: mechanism
  resource: ../../evidence/catalog.json#E-4e55f2a14790
  title: Policy loading and independent frozen-contract normalization
- id: builder
  resource: ../../evidence/catalog.json#E-08a9cb84d70b
  title: Retail validation and exact caster-bit generation
- id: decoder
  resource: ../../evidence/catalog.json#E-df9f699f89af
  title: Mapped C58A3AB9 definition layout and instance reader
---

# Targeted policy and attribution

Runtime feedback rejects the lower casing's five-edge shadow on a marked two-lamp pole and
explicitly chooses shadow removal only. The lower lamp must continue lighting;
the upper lamp and its shadows remain. Marker 1 from internal29 resolves by shot
segment to an Omni at 1771.625,752.590576,73.695221, 0.36m from the shot. It is
instance 6/12 of processor 0x7738 in the c2_i0_xp1665_yp0641_xp1791_yp0767 batch,
owned by WLU near829. This is a strong spatial match, not a runtime-pointer capture.

The matched fields identify the Pequino secondary family across 80 definitions
and 426 placements in 73 audited world batches. Compare every decoded serialized
definition field except colour; all four colours match the 2700/3300/3700/4700K
secondary prototypes. Authored prototype colours require sRGB-to-linear conversion
to match batch colours. A same-colour/intensity/radius wall light is excluded by
the full-field comparison. No blanket radius/brightness-based disabling is allowed.
The raw evidence records the remaining attribution limit: no recovered explicit
instance-to-prototype ID link, and no all-game/DLC population claim.

# Mechanism, ownership and verification

The existing C58A3AB9 batch processor's serialized shadow byte is tag+0x21. All
selected retail flags are zero. The internal World builder leaves those 80 off
instead of enabling them; 12,708 other audited flags still change 0->1. Native
record fields, resources, light colour/intensity/radius and all surrounding bytes
are unchanged. Each definition owns shadow policy for all its listed instances.
This is a static Addons world-payload change, not a native hook or geometry edit.

The explicit manifest owns policy; the builder validates retail hashes, processor
tags and membership before mutation. The independent world verifier derives
actual byte differences from retail and checks all excluded flags remain zero.
The original frozen feature contract stays unchanged: the internal-only archive
gate requires approved exceptions off, normalizes only those bytes in memory,
then compares the entire file to the old frozen hash. Changed illumination,
upper emitters or any other byte still fail. Public builds do not apply exceptions.

The v2.1.30 experiment has offline payload evidence; game appearance was not
established in that evidence. The separate PCSS experiment was retired; this
comparison supplied no replacement shader
archive. Do not silently re-enable it to address softness or the casing artifact.
