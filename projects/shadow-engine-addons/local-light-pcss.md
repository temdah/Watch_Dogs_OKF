---
type: Shader Implementation
title: Perspective Local-Light PCSS
description: Internal Addons perspective-spot filtering, exact TFoWC2 inheritance and offline
  execution gates.
tags:
- shadow-engine-addons
- pcss
- shaders
- compatibility
status: deprecated
sources:
- id: implementation
  resource: ../../evidence/catalog.json#E-9016f25ffa29
  title: Audited SM5 perspective adapter and PCSS instruction generator
- id: build
  resource: ../../evidence/catalog.json#E-a8ac412d6e44
  title: Source identity validation, assembly and complete shader archive preservation
- id: manifest
  resource: ../../evidence/catalog.json#E-1569d736beb2
  title: Exact TFoWC2 1.1.0 archive hashes and 1096 modified object identities
- id: evidence
  resource: ../../evidence/catalog.json#E-232560cde549
  title: Full shader inventory, wrapper and native archive routing evidence
- id: gpu
  resource: ../../evidence/catalog.json#E-86784e421c2d
  title: Direct3D WARP shader creation and synthetic execution
- id: wrapper-reference
  resource: https://github.com/mlleemiles/Watch-Dogs-1-Shader-Compiler/blob/main/CompileShaders.py
  title: Community shader compiler preserves static headers before compiled DXBC
- id: nexus-author
  resource: https://www.nexusmods.com/watchdogs/mods/491
  title: NexusTools author documents one shader mod at a time
---

# Retired v2.1.29 experiment

Runtime feedback reports NexusTools multiple/inactive shader warnings and no discernible visual
improvement. The delivery was rejected; the experiment remains available for a possible future investigation. The implementation and exact input/output evidence are retained as archived provenance.
Active v2.1.30 profiles ship no shadersobj pack and let TFoWC2 retain shader ownership.
The following sections preserve the experiment and its offline evidence, not an
active implementation or permission to redistribute inherited shaders. See
[secondary streetlamp exclusions](secondary-streetlamp-shadows.md) for the retained lower-lamp caster changes.

# Ownership and coverage

The experiment implemented local PCSS for placed world spotlights and vehicle headlights. The adapter owns only ordinary
perspective spotlight shadow visibility: 548 single-comparison and 548 eight-
comparison variants from installed TFoWC2 1.1.0. These span deferred and material
paths. Light owner is not a shader discriminator: world Spot and headlight owners
use the perspective-light family. Exact runtime selection and visual outcome
still require runtime testing; this is not evidence for every fixture or renderer pass.

Full shadow-texture scan found 6,124 PSOs. Facetted filtering and non-perspective
paths remain unchanged. Four-comparison families include directional/cascaded
paths even when spot-projection metadata is used. A single-comparison orthographic
discard shader is also excluded. Four complex 16-comparison perspective shaders
are excluded. Unprojected local examples use paraboloid UVs and linear radial
depth: no ordinary perspective formula is applied there. Omni/capsule coverage
is not claimed. Existing native/facetted PCSS remains exactly as supplied.

# Filter inputs, math and output

SM5 input is the original homogeneous projected UV and comparison depth, with
the already-consumed `_LightSpotShadowProjections` matrix. Capture the center
before native filter offsets overwrite working registers. No new texture,
sampler, constant-buffer binding or engine field is introduced. Eight new temps
belong exclusively to the current pixel invocation; no native mutable state.

For ordinary perspective depth `d=A+B/z`, derive A from the spatial projection
rows `dot(Z,W)/dot(W,W)`. Check nonzero W, parallel rows, positive `A-d`, receiver
range and a 13-texel map-edge margin. `q=1/(A-d)` is linear distance up to a common
positive scale. Eight raw Texture.Load samples accumulate blocker q and count;
the penumbra uses `qReceiver/mean(qBlocker)-1`. No blockers returns visibility 1.
Sixteen fixed spatial PCF offsets filter with radius clamped to 0.5–12 texels.
The effective source size is 12 projected texels, an initial artistic policy,
not a calibrated world-space bulb width. It has no frame-random noise.

Texture dimensions come from resinfo. Original depth bias, comparison sampler,
visibility remap, lighting/material/specular math and downstream consumers remain.
Invalid/edge pixels execute the original filter. The eight-comparison family
reuses one PCSS result through its original accumulation; native comparisons
remain as guarded fallbacks. All original instructions remain in order. Valid
PCSS costs eight raw loads and sixteen comparisons plus the first retained native
comparison; no measured game performance claim follows from offline execution.

# Object and archive contract

All 6,124 captured PSOs have a static prefix of `4+4*count` bytes followed by DXBC
to EOF. The semantic meaning of those IDs is not asserted. Preserve the prefix
exactly; its length does not depend on code length. The community compiler also
prepends unchanged `.header` data to newly compiled bytecode. Assembly preserves
RDEF and signatures exactly; remove optional STAT rather than copying stale
instruction counts. The final assembler generates DXBC sizes/checksum. WARP
CreatePixelShader validates all 1,096 outputs, including sample-frequency shaders.

Installed NexusTools IPE SHA256
`8120389BA4D144DC465E9FED2648B5690A6BBF0CDF5B052EF6EE3B738BE5DCFC`
has `shadersobj.dat/fat` name tests at RVAs 1A7E82/1A7E99. The matching branch at
1A8330 obtains one mod, constructs its archive path, checks it and opens it through
the original file operation at 1A8461. A debug string says it redirects shaders
to that mod. This confirms whole-archive redirection for this binary; function
names and ownership of the selector object remain unproved. Do not modify it.

Consequently internal Addons includes a complete `shadersobj` archive under its
existing mod identity. 38,274 other resources remain byte-identical to TFoWC2;
the installed TFoWC2 is never overwritten. This supersedes the earlier small-pack
proposal, which could discard inherited shaders. Full input hashes are pinned;
different TFoWC2 archives fail the builder rather than silently merge. Public
profiles forbid this experimental pack. This does not fix regional storm hooks.

# Verification and limits

Canonical builder runs the unchanged nine-feature frozen contract, internal
native/Lua tests, exact source/PSO wrapper/interface checks, full inherited-member
comparison, shader family rejection tests and WARP creation/execution before ZIP.
Synthetic 128px map: contact edge spans 2 pixels; separated and radius-clamped
distant edges span 22. Fully lit, fully shadowed, finite output, edge fallback and
invalid projection pass. These validate the emitted filter math on a D3D11 float
shadow SRV; they do not establish the game's actual SRV/projection values,
NexusTools runtime shader selection, visual acceptance or FPS.
