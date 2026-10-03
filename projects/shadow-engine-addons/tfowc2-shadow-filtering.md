---
type: Compatibility Research
title: TFoWC2 PCSS Delivery and Coverage Limits
description: Author-described facetted-shadow PCSS, installed shader delivery and unproved local-light
  coverage.
tags:
- shadow-engine-addons
- tfowc2
- pcss
- shaders
status: draft
sources:
- id: local-pcss-implementation
  resource: local-light-pcss.md
  title: Perspective Local-Light PCSS
- id: local-disassembly
  resource: ../../evidence/catalog.json#E-fbcf85d58b30
  title: Installed deferred shader disassembly and local PCSS feasibility
- id: author
  resource: https://www.nexusmods.com/watchdogs/mods/552
  title: TFoWC2 author description and 1.1.0 changelog, checked September 7
- id: symbols
  resource: ../../evidence/catalog.json#E-0b314a53bd39
  title: Prior compiled shadow shader symbol inventory
- id: failed-trace
  resource: ../../evidence/catalog.json#E-83996fbf2008
  title: Zero actual shader bindings; failed diagnostic, not PCSS classification
- id: historical-contract
  resource: ../../evidence/catalog.json#E-5fc94c34461d
  title: Archived shader evidence contract, provenance only
- id: pcss
  resource: https://developer.download.nvidia.com/shaderlibrary/docs/shadow_PCSS.pdf
  title: NVIDIA PCSS algorithm; general explanation, not TFoWC2 disassembly
---

# Evidence scope

The comparison covers installed TFoWC2 1.1.0 manifests and compiled shader
objects, linked author documentation and earlier unsuccessful shader-trace
evidence. The resulting Addons PCSS29 experiment is now retired; its static/GPU
findings remain available in [local PCSS](local-light-pcss.md).

The author explicitly describes custom contact-hardening shadows/PCSS adapted
to Watch Dogs' facetted shadow mapping, separate screen-space shadows, and Moon
shadow/specular support. The 1.1.0 changelog reports CHSS/PCSS performance changes.
The website currently lists 1.1.1; the inspected local manifest reports 1.1.0.
Do not label local binary findings as an audit of 1.1.1.

Installed 1.1.0 declares the shadersobj pack and no Lua autostart. Its
shadersobj.dat/fat/nfo supplies engine/shaders/obj/h*/pixel_*.pso and vertex_*.vso
resources. This establishes compiled shader delivery. Combined with the author
description, the PCSS implementation belongs to shadow sampling/filtering in
the replacement shader path. This check does not identify a particular PSO as
the PCSS implementation or establish its exact sample count/constants.

General PCSS searches shadow-map blockers, estimates penumbra width from
blocker/receiver separation and light size, then applies a variable-radius PCF
filter. This explains contact-hardening behavior; it is not a disassembly of
TFoWC2's customized implementation. It filters shadow visibility rather than
enabling light casters, increasing their budget or restoring their selection.

# Coverage boundary

## September 7 compiled-path follow-up

Actual installed 1.1.0 disassembly now distinguishes the filtering mechanisms in
1,249 deferred candidates selected from the prior symbol inventory. 102 use
facetted receive parameters and eight raw shadow-depth loads followed by sixteen
variable-radius PCF samples or a four-sample fallback. 830 non-facetted variants
use one/eight/four comparison instructions with no raw blocker search on the
reflected light shadow texture; 317 have no matching texture access. These are
static corpus counts, not runtime selections or per-pixel texel-fetch counts.

Confirmed example pixel_b08ddcac.pso uses t3, cb2[11] facetted parameters and
cb2[30] shadow-map parameters. A cb2[30].y >= 4096 branch performs blocker depth
sum/count, receiver/averageBlocker - 1 and bounded rotated filtering. Its precise
CPU parameter producer and user graphics setting are not mapped. Do not force
4096 on local lights or infer a menu toggle. pixel_d334af33.pso instead performs
ordinary four-row spotlight projection and homogeneous divide, then one comparison
sample of t1; facetted parameters are unused. Resource hashes and complete
disassemblies are in the linked report/inspection.json.

The subsequent full 6,124-PSO scan and functional implementation are recorded in
[local PCSS](local-light-pcss.md). It refines the initial candidate classification:
four-comparison and orthographic paths are excluded, while 1,096 ordinary
perspective variants now receive an Addons-owned filter. All other shaders remain
byte-identical. WARP execution validates filter math; runtime fixture attribution,
actual SRV values and game performance remain for runtime testing.

Prior shader inventories contain facetted/cascaded parameters and local/spot
parameters, sometimes in the same compiled object. Symbols and object-size
differences cannot establish which filtering branch executes for a given lamp.
The v1.0.26 PCSS-enabled trace returned zero bindings because the temporary
device/context hook did not observe active game rendering. It proves neither
PCSS use nor absence for headlights, police spotlights or placed local lights.

The author's confirmed target is facetted shadow mapping. Do not turn that into
an exclusive sun/moon claim or universal all-local-light coverage. The new internal
PCSS build is a functional perspective-light implementation; it makes no claim
that omni/capsule or complex reflection paths have also been adapted.
