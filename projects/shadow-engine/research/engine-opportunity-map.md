---
type: Engine Research Reference
title: Open questions in the mapped Watch Dogs systems
tags:
- shadow-engine
- research
- shadows
- physics
- engine
status: draft
sources:
- id: archived-survey
  resource: ../../../evidence/catalog.json#E-4552ffaa2c1c
  title: Pre-migration detailed engine-system survey
- id: cloth-research
  resource: ../../../evidence/catalog.json#E-84ea28e92dbc
  title: WD1 high-FPS cloth research
---

# What the evidence has not established

These are limits of the documented research, not a feature queue or permission
to install experimental hooks.

| Subject | Missing engine knowledge |
| --- | --- |
| [Shadow population](../architecture/wd1-shadow-eligibility.md) | The primary candidate-holder producer's ordering/group rule and a per-light visible-readiness signal. Sampled admission competition does not establish that native ordering is wrong. |
| [Cached shadows](../architecture/shadow-pressure.md) | Which observed refresh/age transitions cause a particular visible late shadow. Consistent sampled counters do not prove adequate refresh. |
| [Resolution transitions](../architecture/distance-shadow-quality.md) | Safe invalidation and upward/downward resource replacement; changing requested dimensions alone is insufficient. |
| [Cloth](cloth-high-fps-investigation.md) | Exact live output ownership and coherent held-pose publication across solver and presentation phases. |
| [Movement](player-movement-high-fps-investigation.md) | Lower turning/orientation math; character-job suppression disrupted unrelated collision and completion work. |
| [Custom graphics](../../shadow-engine-addons/custom-lightning-asset.md) | Resource loading, short-lived graphics activation, final visibility and the separately observed spawn-registry failure. |
| [Sun/flare direction](../../shadow-engine-addons/sun-flare-alignment.md) | Actual sky UV projection and the final flare-direction consumer. Texture aspect ratio does not establish either. |

An unproved field meaning stays unproved until its writer, readers and lifetime
support the interpretation. Preserve game/build scope when extending any mapping.
