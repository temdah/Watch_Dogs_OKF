---
type: Feasibility Research
title: Additional Non-Batched Game Light Sources
description: Actual game prefab shadow controls outside the reference world-light archives,
  with ownership and runtime limits.
tags:
- shadow-engine-addons
- light-prefabs
- boats
- interiors
- shadows
- research
status: draft
sources:
- id: entity-script-map
  resource: world-entity-script-lights.md
  title: World Entity Lights and Mission Activation
- id: game-sources
  resource: ../../evidence/catalog.json#E-5ae0f31b0d98
  title: Fresh actual-game source-family inspection
- id: inventory
  resource: ../../evidence/catalog.json#E-3fffd32954fc
  title: Prefab fields and comparison with current Addons source
- id: provenance
  resource: ../../evidence/catalog.json#E-69fb0ead873b
  title: Fresh binary and XML input hashes
---

# Confirmed data boundary

This scan covers actual game lighting systems beyond world-sector locations.
Fresh installed common/patch `generated/databases/generic/dynamiclightprefab.lib`
exports have 106/113 records. Patch has 76 explicit `bCastShadow=False`, 32 true,
five absent. These are prefab records with variants, not distinct live lights
or an enable-all recommendation. The references contain only cbatches and do
not edit this database. Named fields and input hashes are the evidence; no new
native RVA or live caller is mapped.[^game-sources][^provenance]

Positive-intensity/radius candidates with explicit false shadow fields in both
the patch data and current Addons source:

* Boat red/green/white navigation lights (`Boat.Nav_Light_*`).
* Taxi-boat cabin/rear (`Taxi_Boat.Cabin`, `Taxi_Boat.Back`).
* Vehicle ceiling/cabin and dashboard (`Vehicle.Vehicle_Ceiling_Light`,
  `Vehicle.Vehicle_Dashboard_Light`).
* Train monitors (`Ltrain.Ltrain_InteriorLight_Monitor_01`, `_02`).
* Red helicopter strobe (`Helicopter.Strobe_Light_Red`).
* Dynamic bollard (`X-Ingredients.Bollard_Standard_Dyn_Light_01`).
* Slot machine (`MiniGames.Slotmachine_Light_01`).

Ownership/output boundary: native-engine-consumed prefab settings specify light
shape, brightness, radius and an explicit shadow control. Entity attachment,
active variants and final shadow admission are not traced. These are editable
data candidates, not proven runtime shadows or a mapped scripting/injection
API. Short radii limit potential visible benefit.[^inventory]

# Exceptions and safety

The subsequent [world entity and mission map](world-entity-script-lights.md)
identifies 78 additional authored shadow-off entity IDs and 17 exact script/WLU
target joins. It covers a separate component/activation boundary; it does not
resolve attachment or live use for every prefab listed above.

Capsule train interiors (`Ltrain_InteriorLight_Dynamic01/02`), taxi-boat neon
left/right and white helicopter strobe lack an exported `bCastShadow` field.
Do not infer false or transplant the compiled world-byte mapping without
resolving defaults/schema/native consumers.

Current Addons already alters stock emergency/headlight records. Rear
reflection-only components deliberately remain non-casting; the main licence-
plate override has zero intensity. Not every stock false flag is a useful new
feature. These static candidates have no demonstrated runtime implementation.

[Muzzle lights](muzzle-flash-shadows.md) are a separate particle research path.
Neither muzzle nor fire/explosion caster support follows from these prefabs.
[World batches](world-light-shadow-batches.md) own the separate 496-instance
omission finding. This scan is not a full-game source enumeration or runtime
rendering/performance proof.

[^game-sources]: Actual common/patch source-family inspection and limits
[^inventory]: Named fields and current addon differences
[^provenance]: Fresh binary and XML input identities
