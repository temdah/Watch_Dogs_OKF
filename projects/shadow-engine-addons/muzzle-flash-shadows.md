---
type: Feasibility Research
title: Muzzle-Flash Dynamic Shadows
description: Confirmed authored muzzle-light data and unresolved native shadow-caster feasibility.
tags:
- shadow-engine-addons
- muzzle-flash
- particles
- dynamic-shadows
- research
status: draft
sources:
- id: investigation
  resource: ../../evidence/catalog.json#E-6b7639f08734
  title: Muzzle-shadow feasibility report and limitations
- id: authored-data
  resource: ../../evidence/catalog.json#E-76447e4b8cc2
  title: Base particle-library findings and input identities
- id: native-evidence
  resource: ../../evidence/catalog.json#E-2e96ad2de634
  title: Captured native configuration registration and particle-parameter readers
---

# Confirmed authored behavior

The installed base `windy_city_deploadnewparticles.rml` contains 1,111 particle
systems and 5,953 emitters. Of 20 named weapon muzzle systems, 17 contain an
active forward-light emitter (`MaterialType=4`) with environment/particle
illumination and quadratic falloff enabled. The three named handgun/rifle/SMG
SpecOps variants have no MaterialType-4 emitter. The authored light lifetimes
are 50 ms for rifles/SMGs, 55 ms for handguns, 150 ms for shotguns, and 200 ms
for sniper rifles/grenade launchers. Replica/alternate variants are counted
separately; these values are not runtime measurements.[^authored-data]

The effect contains both visible particle visuals and short-lived illumination.
The feature under investigation is shadows from that illumination, not making
the visible flash sprite itself an occluder. No runtime result is available.

No `bCastShadow` emitter attribute exists in the inspected library. Its only
shadow-named emitter attribute is `PixelShadowSampling`, which is zero for the
17 muzzle light emitters and is not established as a caster-enable setting.
Do not transplant the world-batch `+5` definition mapping into particle data.

Retained 1911/416 entity exports expose separate player/non-player particle
references and front/face light settings. Their front radii are zero; 1911 face
radius and 416 face intensity are also zero. Those exports are candidate
evidence, not independently authenticated stock. The exact exported weapon
particle IDs have not been linked to the base named effect families. Terrain
muzzle illumination settings do not prove a shadow-caster control.

# Confirmed static mappings

Scope: captured image
preserved evidence, SHA-256
`D8004145FB17BD6A9073466EBB9BFC19589AAD7D08D8EC3FD45733A5D8AD0855`.
These are image-specific configuration mappings, not live hooks or regional
compatibility claims.[^native-evidence]

| Location | Role and input/output |
|---|---|
| `0x00D98CE2`–registration sequence | Names `ImpactLightConfiguration` and registers weapon configuration offset `+0x250`. |
| `0x00D98D39` / `0x00D98D47` | Names `FrontLightConfiguration` and registers weapon configuration offset `+0x218`. |
| `0x00D98D55` / `0x00D98D63` | Names `FaceLightConfiguration` and registers weapon configuration offset `+0x1C0`. |
| `0x006748F2` through `0x0067492B` | Reads authored `PartLightAffectsParticles` Boolean; writes the current parser destination's byte `+0xA6`. |
| `0x00674934` through `0x0067496D` | Reads authored `PartLightAffectsEnvironment` Boolean; writes parser destination byte `+0xA7`. |

The particle reader accepts textual Boolean data and populates native resource
parameters. Parser output ownership is native; the lifetime of a rendered
particle light and its final shadow-admission consumer are not mapped here.
The weapon registration exposes configuration fields, not evidence that those
members identify live muzzle lights. No writes or runtime observations were
performed. Broad string-dictionary names `CMuzzleFlashManager` and
`CMuzzleFlashEffectProcessor` were absent from this captured image and remain
unmapped leads; UI `fFlashTime` was rejected as muzzle evidence.

# Feasibility remains open

Native support is plausible but unproven. Candidate strategies are upgrading
an exactly identified emitted light through a shadow-capable path, or creating
a synchronized ordinary shadow-capable light with correct muzzle attachment
and lifetime. Neither is selected or implemented. The second requires handling
duplicate illumination; both require player/NPC, suppressed-variant, automatic
fire, engine lifecycle and workload checks. No pure-Lua caster operation is
established by the local references.

Next boundary: read-only creation/submission/retirement correlation for one
known muzzle light and proof of the shadow-policy consumer. Preserve the
authored flash timing; do not extend it to mask late shadow work. Keep Shadow
Engine capacity and vehicle-light behavior unchanged. Runtime and visual behavior remain unvalidated. This feature is research, not a
promised working one-byte fix.[^investigation]

[^investigation]: Muzzle-shadow feasibility report and limitations
[^authored-data]: Base particle-library findings and input identities
[^native-evidence]: Captured native configuration registration and particle-parameter readers
