---
type: Implementation Plan
title: Distance Shadow Quality Controls
description: Linked distance boundaries and native LOD evidence gates before world-shadow quality
  changes.
tags:
- shadow-engine
- resolution
- distance
- lod
- configuration
status: draft
sources:
- id: private-fixed-baseline-v250
  resource: ../../../evidence/catalog.json#E-d04bec212810
  title: Fixed vehicle/world quality baseline
- id: private-world-resource-probe
  resource: ../../../evidence/catalog.json#E-1b18a9b7f03d
  title: Global no-change result and bounded resource probe
- id: private-world-tier-result
  resource: ../../../evidence/catalog.json#E-239a5e38a4a6
  title: Independent world-light distance-tier implementation and validation
- id: private-renderer-callers
  resource: ../../../evidence/catalog.json#E-9e605c0c7194
  title: Fresh Global renderer caller export
- id: private-render-shadow-caller
  resource: ../../../evidence/catalog.json#E-61de5cfd3462
  title: Fresh Global RenderShadow caller export
- id: private-manager
  resource: ../../../evidence/catalog.json#E-bc0e0b354e98
  title: Fresh Global shadow-manager export
- id: private-vehicle-tier-result
  resource: ../../../evidence/catalog.json#E-3fbd10671774
  title: Exact vehicle distance-tier implementation and validation
- id: private-native-size-getter
  resource: ../../../evidence/catalog.json#E-eaf1d1f00d36
  title: Preserved complete Global texture-dimension getter disassembly
- id: private-resource-transition43
  resource: ../../../evidence/catalog.json#E-e70c6531fe6e
  title: Before-resource diagnostic candidate and fresh field proof
- id: private-four-captures
  resource: ../../../evidence/catalog.json#E-e1ae96164874
  title: Four complete native-resolution captures and interpretation limits
- id: private-builder
  resource: ../../../evidence/catalog.json#E-1001d162f65a
  title: Preserved Global queue-builder decompilation
- id: private-renderer
  resource: ../../../evidence/catalog.json#E-08039110f66c
  title: Preserved Global renderer resource-consumer decompilation
- id: private-callback
  resource: ../../../evidence/catalog.json#E-eb759699435d
  title: Preserved renderer and manager profile callback
- id: private-observed
  resource: vehicle-light-provenance.md
  title: Vehicle Light Component to Renderer Provenance
- id: private-quality
  resource: vehicle-shadow-quality.md
  title: Vehicle Shadow Quality Boundary
- id: private-public-plan
  resource: ../../../evidence/catalog.json#E-65a5cc19aca5
  title: Sanitized implementation gates and user controls
- id: public-resource
  resource: headlight-resource-diagnostics.md
  title: Headlight Shadow Resource Diagnostics
- id: public-pressure
  resource: shadow-pressure.md
  title: Shadow Pressure Boundaries
- id: public-tools
  resource: internal-tools.md
  title: Lua-to-native bridges and shared-control ownership experiments
---

# Scope

Distance tiers were a removed experiment. Version .50 removed their consumers
after vehicle/world request changes lacked reliable visible effectiveness.
This concept records native resolution producers, backing-resource reuse and
the failed controls. The separate [vehicle quality](vehicle-shadow-quality.md)
concept owns fixed-cap evidence.

# Resolution producer and resource consumers

The following roles are static Global evidence. They are not a distance-only LOD table, portable regional offsets or GPU allocation proof.

| Function or field | Confirmed role and limits |
| --- | --- |
| Queue builder 0x0030A570 | Writes requested dimensions at entry+20A4/+20A8. Type 0 follows configuration+9E4 or +A70. Nonzero descriptor+40 sign bit selects configuration+9E8; bit 26 selects +9EC; otherwise an unbound path uses +9E0 (1024 fallback when zero), or a manager-bound path calls 0x0025DBF0. Flag meanings and writable-policy semantics remain unproven. |
| Texture dimension getter 0x0025DBF0 | RCX is a texture wrapper; wrapper+1A0 provides the native object; virtual+50 fills a stack-local descriptor; its first two 32-bit words go to RDX/R8. This reads existing dimensions, not distance/projected size. The queue builder is a consumer, not necessarily the resolution owner. |
| Renderer 0x00306E60 | Candidate+58 is backing state; backing+40 is resource. Shared-texture lookup 0x00430A80 occurs only for null resource; otherwise native reuses it. Request dimensions also feed rendering parameters. Resource invalidation/resize ownership is therefore a prerequisite for dynamic tiers. |
| Profile callback 0x00308A90 | Reads configuration+A54 and clamps manager+AC to 32..4096 alongside cached-owner count changes. Calling this a general distance LOD threshold is unsupported. |
| Builder view reference | Parameter 4 +1E0/+1E4/+1E8 supplies XYZ; its address becomes argument 6 of the only direct manager 0x002E9B60 call. The experimental manager hook copied it coherently and forwarded all seven arguments. |
| Local-light spatial fields | Nonzero spatial+08/+0C/+10 is the builder's point-transform position. +14/+18/+1C is normalized direction. Type 0 follows a separate directional/cascade path. |

The historical native vehicle-batch distance value was later established as camera-derived; [incoming readiness](incoming-vehicle-readiness.md) owns the corrected camera/player distinction. The distance experiment's earlier player-distance name is not reliable semantic proof.

Writers/initialization of configuration+9E0/+9E8/+9EC/+A54 and relevant candidate+58/backing+40 writer/releaser paths remain unresolved. Regional checks of existing manager/renderer hooks do not prove distance units or a live LOD interpretation.

# Controlled observations and failed experiments

- Version .41: limiter behavior was reported correct; 512 visibly coarser, 1024 different but usable, 2048/4096 similar. No FPS benefit was measured.
- Version .42: four states produced 16 renderer windows and 83 rows. Native input, policy request and returned CPU resource dimensions agreed: 51 rows at 4096, 16 at 512, 16 at 8192. A correlated type-1 handle 0x4D5 stayed 4096 close/far/returned-close and disappeared from submitted work when facing away. This supports view-dependent membership, not a culling rule or distance-resolution transition. The world light was not explicitly tagged; shared handles require spatial disambiguation. More return-close entries prevent treating scene totals as a controlled distance comparison. The distant shadow was reported barely distinguishable, not confirmed absent.
- Version .43: stationary 4096 -> 512 -> 4096 CPU request/resource agreement held for both exact headlights. Output wrapper addresses stayed stable and pre-native backing resources were always null, so native shared-resource acquisition occurred each call. This validates the tested CPU transitions, not GPU allocation identity or a world-distance input.
- Version .45: exact vehicle type-1/type-3 requests used ordered 4096/2048/1024 caps, originally staged at 10/20/40 world-distance endpoints, preserving native requests outside. The native batch scalar supplied distance; its later camera-derived correction applies. The configuration was atomic and unknown/shared/world identities stayed native. No resource lifecycle change was added.
- Version .46 was withdrawn before delivery because normalized direction was confused with position. Corrected .47 used the builder view reference and spatial position for remaining nonzero local lights, excluding exact and ambiguous vehicle identities and all type-zero cascades. It added no hook, cache, atlas, allocation, release, admission, capacity or lifecycle mechanism.
- Version .48 accepted world-setting commands and capped 46,876 entries over 15,245 calls before disable, but no visible streetlight-shadow transition was reported, including a 100 m 4096 band and enable/disable comparisons. The command carrier and CPU distance selection worked; request-field mutation alone was insufficient evidence of an effective world implementation.
- Version .49 added a finite Internal-only 256-mutated-entry comparison of pre-native backing/resource state, request dimensions, returned resource metadata and address reuse. It performed no invalidation, resize, allocation, release, wait or new hook. It was untested and removed in .50.

The old six-state .18 captures showed type-3 requests at 512 and target headlights at 4096; variation does not prove a 512 distance cutoff.

# Conditional distance design

Ordered end distances describe contiguous bands: 4096 below endpoint 1, 2048 through endpoint 2, 1024 through endpoint 3, then preserve native behavior. Changing endpoint 1 automatically changes the second band's start. Each tier caps min(native,tier), never silently upscales or disables shadows at the last boundary. Native outside a 1024 band may return to 4096, so this is not necessarily a monotonic performance policy.

Further work needs mapped resolution producers, safe upward/downward resource transitions and coherent request/resource/viewport parameters. It must distinguish dynamic local lights, cached owners and sun/cascades; an affected building is not evidence of a sun-shadow path. No resource may be nulled or forcibly released merely to induce regeneration.

Useful bounded evidence correlates pre-policy/post-policy dimensions, returned resource sizes, reuse identity, full light identity, native lane and proven spatial input. Unknown units stay unknown. Approach/retreat, fixed-distance camera rotation and pressure changes must compare retained identities, not aggregates. No continuous per-face logging, native waits or render-path file I/O is implied.

Any revived policy would need deterministic boundary tests, generation-safe bounded hysteresis, separate vehicle/world settings, native-outside behavior and preserved uncertainty/admission boundaries. Forced promotion of lower native requests and sun support each require separate quality/cost and ownership evidence. Public release separation and diagnostic exclusion remain independent requirements.
