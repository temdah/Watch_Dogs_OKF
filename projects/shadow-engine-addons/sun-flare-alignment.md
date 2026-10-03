---
type: Engine Subsystem
title: 'HDRI sun and native flare: selection mappings and unresolved projection'
tags:
- shadow-engine-addons
- sun
- flare
- hdri
- sky
status: draft
sources:
- id: public-storm-promotion
  resource: public-storm-runtime.md
  title: Separating a storm hook host from optional observers
- id: probe
  resource: atmosphere-probe.md
  title: Bounded Atmosphere Snapshot Probe
- id: selection
  resource: ../../evidence/catalog.json#E-ef87fe988bcd
  title: Preserved CPU selection and hotspot research
- id: recheck
  resource: ../../evidence/catalog.json#E-777907b11eb7
  title: Rechecked cloud-key wrapper and its setter side effect
- id: captures
  resource: ../../evidence/catalog.json#E-2a47e631c04f
  title: Existing fixed-camera sun sequence
---

# Problem and observed boundary

The visible hotspot in a TFoWC2 HDRI did not reliably align with the native flare.
Enabling a disc-free flare in nine environment states supplied a comparison;
it did not solve position. A bounded post-sky-update capture inspected selected
cloud records and steps without calling setters or writing directions.
The shader projection and final flare-direction consumer remain unresolved.

# Confirmed selection boundary

The preserved captured engine has SHA256
`D8004145FB17BD6A9073466EBB9BFC19589AAD7D08D8EC3FD45733A5D8AD0855`.
These are static mappings for that image only:

| RVA | Role |
|---|---|
| `0xA53860` | Cloud/sky orchestrator selects record/time steps and clear/storm blending, then publishes output. |
| `0xA23310` | Randomized recipe selector and elapsed/duration weight. |
| `0xA22F40`, `0xA132F0` | Append selected record/step/context and blend weight. |
| `0xA455A0` | Selected-resource/output evaluator. |
| `0x9F5820` | Active-cloud setter writes both active record pointers. |
| `0x1E1C800` | Key-based cloud override wrapper; validates type then calls the setter. **It mutates active selection and must not be used as a read-only query.** |

Database resources and emitted renderer arrays remain engine-owned. Record
`+0x20/+0x28` is the time-step array/count; steps are `0xA8` bytes, with hour
at `+0`, lower/upper shapes at `+8/+0x58`. Record crossfade fields are
`+0x30/+0x34`; sun-position bias is `+0x78`.

Clear/storm records are `C0FD4E08` / `94B68E0D` in serialized key bytes.
Time-step blending begins before each hour key, using the 150-second configured
transition window scaled by the game's time progression. Recipe transitions,
weather blending, and lower/upper texture composition are distinct operations.
The source report holds the complete resource schedule and hotspot centroids.

# What remains unproven

Hotspot pixel measurements are reusable, but their proposed 360-by-90-degree
ring interpretation is not a verified shader projection. Older notes also
describe the 4:1 textures as four horizontal faces. Dimensions alone settle
neither interpretation. Recover actual UV projection, orientation, lower/upper
composition, and the final flare-direction consumer before applying a correction.

Existing fixed-camera evidence shows varying error across sky families; a
single screen offset or guessed global rotation cannot be assumed sufficient.
Do not change a shared astronomical sun/moon vector just to reposition the
flare. Identify which consumers would move before choosing the write boundary.

No alignment correction was established. A useful validation corpus spans
sunrise, noon, sunset, texture/recipe transitions, weather blends, night visibility
and moon-shadow preservation; one fixed-camera match would be insufficient.
