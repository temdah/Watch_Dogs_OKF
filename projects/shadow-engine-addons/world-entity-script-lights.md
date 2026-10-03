---
type: Engine Mapping
title: World Entity Lights and Mission Activation
description: Authored world-light owners, explicit shadow flags, and Domino activation contracts
  outside cbatch-only edits.
tags:
- shadow-engine-addons
- world-lights
- entity
- domino
- shadows
- research
status: draft
sources:
- id: audit
  resource: ../../evidence/catalog.json#E-7a9ff33d62a6
  title: Actual-game entity and script mapping, scope and reproduction
- id: components
  resource: ../../evidence/catalog.json#E-7db41850bfac
  title: Owner references, explicit light fields and authored coordinates
- id: targets
  resource: ../../evidence/catalog.json#E-5c0a759abc78
  title: Script lines, target IDs, actions and exact WLU entity matches
- id: validation
  resource: ../../evidence/catalog.json#E-df34ac470d7d
  title: Input hashes, owner references, shadow values and library parity checks
---

# Scope and evidence

Read-only installed common/patch/patch1/Windy City data inspection, 2026-08-31.
No live-process profile/RVA, installation, game launch, addon implementation or
build. Evidence is authored binary data and offline Lua decompilation, not
renderer admission or visual acceptance. These findings extend the separate
[world batch](world-light-shadow-batches.md) and
[additional prefab](additional-light-sources.md) maps.[^audit]

# Entity component ownership

`CDynamicLightComponent` carries authored shape, enable, intensity, radius,
shadow flag and Affects settings under an Entity owner. Inputs include prefab
references/overrides and electricity/time-of-day fields; final native consumers
and inheritance resolution are not established here. WLU owner IDs and positions
identify serialized records, not guaranteed loaded lights.

FCB back-references share complete component nodes between different owners.
Deduplicate by source + owner + component, not just component offset. The scan
maps 1,018 WLU owner/component references (742 distinct entity IDs) using 263
stored dynamic-light nodes. **78 distinct owners explicitly have shadows off**,
14 owner references on, 926 locally absent. Absent is not false.[^components]

Concrete explicit-off findings: six exact ParentId-linked BeanSculpture omni
owners in near554; Owl Motel neon near862; stadium spotlight and disabled soda
spot; eight HMA/one SAS Aberration Lounge light owners; 21 hubunlock indicators;
four A02M10 indicators; four initially disabled AftermatFire owners near1094;
other mission/sector/poker lights with exact IDs and coordinates in the audit.
Forty-seven of the 78 are authored enabled, positive and geometry-affecting with
non-black color. Exclusions: 17 zero intensity, four GI-only, one black-color
projector and nine initially disabled. This screening is not feasibility proof.
Bean parent links are exact; parent transform composition remains unverified.
Fire-named entity lights do not establish particle-fire caster support.[^audit]

Both fully decoded entity libraries contain 7,194 prototype entries. Runtime
has 1,841 light-bearing prototypes (1,816 stored component nodes): 1,235 explicit
off, 358 on, 248 absent. These can also feed existing batches and are not an
additional live-light count. Lighting data agrees between editor/runtime pairs
apart from editor-only text. GUID-to-library-UID inheritance remains unresolved;
do not use name matches to supply missing flags.[^validation]

# Script activation contract

Confirmed decompiled call boundary, without native binding/RVA or live testing:

| Script consumer | Input and output/operation | Ownership limit |
|---|---|---|
| `LightController` | Entity ID and enabled value into `SetEnableLight`; Toggle reads `GetEnableLight` then writes the opposite | Existing-entity activation, not a mapped shadow setter |
| `SpotlightController` | `SetSpotlightBehavior(1/0, Vehicle, SpotlightTarget, 0)`; missing target becomes invalid entity ID | Vehicle spotlight behavior/targeting, not arbitrary world-lamp caster flags |
| `OverrideEnvironmentLighting` | Manager `SetLightingOverride` / `RemoveLightingOverride`, setting and transition duration | Environment lighting domain; no per-light shadow control established |

Of 45 numeric target IDs in the bounded non-debug script scan, 17 match WLU IDs:
15 stadium board/banner lamps in A01M01 (local shadow fields absent), the A01M06
red `OmniLight_ALARM` (ID 2081528631378735176, shadows already enabled, script
Toggle), and A04M06 New's QuinnPlace blue gyro light in the Merlot interior
(ID 2083508947859278301, inherited settings unresolved). HQ power-up field
targets and other unmatched targets remain leads. Script and entity counts
overlap; they are not additive source families.[^targets]

# Coverage and safety

All 487 light-containing Lua files among 7,523 extracted scripts decompiled
through EOF. the preserved evidence location duplicates and gym/test scripts are not evidence of
shipping runtime execution. 212 of 2,356 WLU inputs stop in unsupported later
data; only completed light nodes are used and file errors retained. This is a
bounded mapping, not a full-game census. Owner/hash/value/parity checks are in
the validation record.[^validation]

Any future runtime caster implementation requires native component access,
inheritance, entity lifetime/streaming and shadow-admission mapping. Preserve
mission activation, blackout/electricity and time-of-day ownership; do not force
lights on or infer safe shadow mutation from an activation API. No change to
current release behavior or package is implied.

[^audit]: Research report with per-location evidence, limits and reproducibility
[^components]: Binary-derived light owner settings and identities
[^targets]: Decompiled mission lines joined by exact numeric entity ID
[^validation]: Offline verification only; no human or runtime acceptance
