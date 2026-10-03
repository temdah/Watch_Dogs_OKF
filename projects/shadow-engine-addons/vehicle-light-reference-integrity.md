---
type: Serialized Data Contract
title: Vehicle Specular Light Reference Integrity
description: Confirmed entity-to-preset identity mismatch and internal staging repair for rear
  and emergency lights.
tags:
- shadow-engine-addons
- vehicle-lights
- specular
- references
status: stable
sources:
- id: public-storm-promotion
  resource: public-storm-runtime.md
  title: Separating a storm hook host from optional observers
- id: regression-timeline
  resource: ../../evidence/catalog.json#E-bedf1db086b8
  title: Original August26 v2.0.1 resolves correctly; August30 identity rebuild breaks references
- id: audit
  resource: ../../evidence/catalog.json#E-77bd9ffcdf4c
  title: Source and effective entity references and exact candidate archive comparison
- id: investigation
  resource: ../../evidence/catalog.json#E-607303853326
  title: Rear reference regression and first-entry thunder candidate
- id: repair
  resource: ../../evidence/catalog.json#E-447f671530b4
  title: Internal-only identity repair with complete specular-chain checks
---

# Confirmed mismatch

Runtime feedback reports missing rear specular reflections on all vehicles in v2.1.26; last
working version is unknown. The source entity FCB SHA256
12B30DA98C310CEF9A21A1D13E79DFD1FD637BE78409B6E94FC58C341B2B6564 contains
510 rear attachments across 255 vehicle owners and 16 ambulance/firetruck
attachments. Their seven preset IDs are absent from the packaged vehicle preset
database. The similarly named database records have different IDs. Keeping the
same asset hash across storm builds preserved this mismatch; hashes alone did
not establish retained working references. Subsequent package comparison finds
the first broken package in that comparison: the August30 v2.0.1 identity rebuild.
Original August26 v2.0.1 has the same entity FCB but correctly matching preset
keys. The rebuilt preset LIB and entity FCB are byte-identical to26. Rollback
source differs from its original packaged LIB, so the exact source-edit time
is not established. See the indexed regression timeline.

This is confirmed serialized reference evidence, not a runtime claim that the
candidate is visually fixed. Current source and the saved NexusTools merged
entity output both reference the keys below. The captured merged output has
474 rear and 14 emergency references, differing from source during the existing
mod merge; no unrelated mod or merge policy is altered.

| Preset suffix under ShadowEngineAddons | Entity key (numeric) | Source count |
| --- | --- | --- |
| TailLight_Specular | 748D6974 | 478 |
| TailLight_Low_Specular | 7531229B | 24 |
| TailLight_Very_Low_Specular | 18A9870C | 8 |
| Ambulance_Front | A820A222 | 3 |
| Ambulance_Back | 05CA3602 | 3 |
| FireTruck_Left | E04B0949 | 5 |
| FireTruck_Right | F83949A4 | 5 |

# Ownership and repair

Entity DynamicLights entries consume Vehicledynamiclightpreset keys. Each preset
then references a Dynamiclightprefab through dynamiclightprefabPrefabDynamicLight.
The latter links already resolve to existing specular-enabled definitions.
Native database keys need not be derived from their names; rehashing every
custom record is unnecessary. Only the seven dangling preset identities are
changed (hidName and hidKey, serialized little-endian BinHex). Position, intensity,
range, slot assignment, attenuation and all prefab references remain identical.

The v2.1.27 experiment applied this repair; v2.2.0 stored the seven corrected identities in canonical source and
updates the source/archive allowlists. Existing public v2.1.0 ZIPs stay unchanged.
The public repaired LIB is byte-identical to v2.1.27. Light shape, brightness,
positions and every non-identity field remain unchanged. The v1.0.38/39 envelope is an independent shape-control baseline.
The canonical builder rejects changed source identities or entity hashes until
the attachment audit is revisited. Tests reject dangling entity/prefab links and
non-specular targets and compare every non-identity field. The actual packaged
LIB was extracted and exported again: its entire semantic XML matches the
expected repair. Exactly one of 1,890 assets differs from26.

Runtime acceptance separately covers visible rear reflections across vehicles,
including emergency lights, with TFoWC2 and the existing mod order.

The subsequent [nine-feature audit and mandatory gate](established-feature-tests.md)
verifies full record semantics, consumer references and fleet placements from
actual archives. Internal27 passes; both public210 editions fail on the same526
attachments. No additional parameter drift was found across371 protected records.

Both v2.2.0 package variants passed the same independent nine-feature gate.
The old public210 failure remains regression provenance, not evidence about every later package.
