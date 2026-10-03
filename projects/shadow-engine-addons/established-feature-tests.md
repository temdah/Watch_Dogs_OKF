---
type: Validation Contract
title: Semantic validation of lighting references and compiled assets
tags:
- shadow-engine-addons
- tests
- compatibility
- lighting
- regression
status: stable
sources:
- id: public-storm-promotion
  resource: public-storm-runtime.md
  title: Separating a storm hook host from optional observers
- id: audit
  resource: ../../evidence/catalog.json#E-03ce0fd18c43
  title: Nine-feature audit, historical control and mutation tests
- id: baseline
  resource: ../../evidence/catalog.json#E-c2d43d2bb848
  title: Frozen semantic fields, placements and independent world hashes
- id: mechanism
  resource: ../../evidence/catalog.json#E-c322d8e79fa5
  title: Record/reference/placement comparison
- id: gate
  resource: ../../evidence/catalog.json#E-efdc4561192c
  title: Actual packaged database and entity inspection
- id: tests
  resource: ../../evidence/catalog.json#E-19b873504dae
  title: Twenty-five retained-feature regression tests
---

# Serialized reference chain

Watch Dogs database `hidKey` is little-endian BinHex. FCBastard entity
`#XXXXXXXX` references are numeric keys. Entity VehicleDynamicLightPreset
references resolve to dynamic-light prefabs; vehicle lamp presets resolve to
light effects. Matching display names does not establish a working reference.
Duplicate keys or names make identity ambiguous and were rejected by the checks.

An independent baseline captured 371 records across four libraries and 2,722
lighting owners with reference-bearing nodes and driver/culling flags. Its 8,029
previously resolved entity references had to resolve to the same semantic target.
Unresolved native/external references stayed explicit tokens. They were not
invented as resolved records. Atlas data and optional world bytes were checked
separately.

# Experiments and observed regression

The baseline included 255 rear-equipped vehicles, 510 paired emitters, 25 police
variants and 16 emergency emitters across eight owners. Comparison found seven
mismatched preset keys affecting 526 attachments in the older public payload,
while the other protected records and world hashes matched. File presence and
plausible custom names had failed to catch broken reference chains.

The subsequent correction repaired those seven IDs. The resulting preset LIB
matched the previously working internal reference, and real Standard/World
archives passed the same semantic expectations without changing rear-light shape.
See [reference integrity](vehicle-light-reference-integrity.md).

# Independent validation method

The comparator exported actual LIB/FCB data from the produced archive and checked
fields, targets, emitter counts, positions, ranges, shadow/specular/activation
flags, emergency slots and searchlight references. Negative fixtures deliberately
deleted or duplicated emitters, broke links, removed fleet members, corrupted
archives and leaked assets between variants. World tests compared verified retail
bytes against only the explicitly allowed caster-bit changes.

Expectations came from the independent reference, never from the candidate under
test. Regenerating a baseline from a failing candidate would conceal the very
regression being measured. A deliberately changed feature needs a separately
explained expectation and a negative test for unintended drift.

# Limits

Semantic equality proves inspected data relationships. It does not establish
native admission, resource residency, external mod merging, final rendering or
performance. The distinction is especially important for shadow-enabled lights:
an authored caster flag is only an input to the engine's later selection stages.
