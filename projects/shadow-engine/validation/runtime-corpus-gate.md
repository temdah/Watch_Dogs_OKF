---
type: Validation Reference
title: Regional Runtime Corpus Gate
description: Offline verification of capacity-sensitive patch sites across all supported executable
  layouts.
tags:
- shadow-engine
- validation
- regional
- capacity
- automation
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-shadow-a4ee-capture-20261004
  title: Mapped A4EE image and complete five-profile offline proof
- id: validator
  resource: ../../../evidence/catalog.json#E-ebc961aaf6ec
  title: Runtime corpus validator
- id: profiles
  resource: ../../../evidence/catalog.json#E-4d85852a0d8b
  title: Runtime profiles and address resolution
- id: corpus
  resource: ../../../evidence/catalog.json#E-cb00e25d0849
  title: Private five-runtime corpus manifest
- id: a4ee-attestation
  resource: ../../../evidence/catalog.json#E-ee4d3390a611
  title: Frozen v1.2.3 A4EE successful runtime attestation
- resource: ../../../evidence/catalog.json#E-ec0b5999a154
  title: Runtime corpus validator
- resource: ../../../evidence/catalog.json#E-1f29073db08d
  title: Runtime profiles and address resolution
---

# Purpose

Capacity changes must be checked against the executable layouts they will
mutate, not only against C source. The corpus validator verifies all five exact
PE identities and independently resolves the capacity-sensitive RVAs for each
profile.[^validator]

# Coverage and historical gate versions

Global/04DF and Asia/Miru use preserved mapped images; VMPless and Complete
Edition have usable code bytes in their raw files. The historical v 2.0.5 gate
performed 63 byte-exact checks per usable profile (15 signatures, 46 relocations,
construction and pre-finalizer/decoded-call proof).

For those four profiles, the v 2.0.12 gate
with `--intersection-diagnostic` performs 71 byte-exact checks per profile:
16 signatures, 46 relocation sites,
the map-construction loop, and the frame-graph pre-finalizer sequence plus its
decoded native call target. The validator
also checks the three lookup calls, three matching builder field stores and
their shared target/prologue (seven checks). This observer coverage is explicit;
without the flag the current baseline has 64 checks. The validator
verifies the old immediate at every relocation,
derives the new value from the owning `0x24C0`, `0x24C4`, or `0x24C8` region,
and simulates every write in a disposable memory copy.

The packed Shev/A4EE disk file alone cannot supply code at the manager hook RVA
`0x0086D700`: that virtual range has no raw file bytes. Its historical successful
runtime attestation predates later boundaries and cannot replace an image proof.

A read-only A4EE capture on 2026-10-04 closes this missing-image gap. The loaded
module was identified by its scoped executable/module path and PE identity:
timestamp `0x5CD13864`, checksum `0x01E4FD51`, entry RVA `0x05824EE5`, image size
`0x06595000`. The disk DLL SHA256 is
`a4eead7a645ab4340a67622da4bfc91789e8cecfd53f605499a0e4b09b3ee60a`;
the mapped image SHA256 is
`171c6a2efc00b2404b5ff4a032dcfda42c162468a7767ef76989bb2cc894e7f8`.

All 106,516,480 bytes were readable, with zero missing pages. Shadow Engine was
disabled during capture, and the collector requested only process-query and
memory-read access. It did not suspend, inject or patch the process. The image
passes 71 core byte checks, 46 simulated relocation writes and quality-consumer
proof at renderer `0x0089E4F0` / lookup `0x009550D0` (five queue spans, resource
variant 0). Registering its hash as a mapped input makes all five profiles pass
the same current offline gate. The image remains private and is reused for
future candidates targeting this game version.

This closes the core compatibility evidence gap, not optional-feature mapping
or visual acceptance. Vehicle identity/finite-selection paths remain disabled
for A4EE until separately mapped; Global-only features remain Global-only.

# Boundary

This gate catches wrong RVAs, wrong old bytes, incorrect regional mapping, and
incorrect capacity-layout formulas such as the rejected v 1.2.2 uniform-stride
change. It does not execute the game, prove that a detour runs, or judge visual
output. Manual validation remains proportionate to the changed compatibility
surface.

[^validator]: Runtime corpus validator

The earlier pre-hotfix baseline performed 62 checks: 15 signatures, 46 relocation
sites and construction. Its packed A4EE acceptance used a frozen runtime attestation
(profile, cluster deltas, 46 relocations, completion). That attestation did not
cover subsequently added sites and cannot close their manual-required gate.
