---
type: Reverse Engineering Mapping
title: Compiled World-Light Shadows and Decoded Locations
description: Exact shadow-flag, instance serializer, light-type and world-resource ownership
  mappings for the two reference archives.
tags:
- shadow-engine-addons
- world-lights
- cbatch
- shadows
- static-analysis
status: stable
sources:
- id: sharp-marker-1
  resource: ../../evidence/catalog.json#E-06a468805f03
  title: Shot-segment-resolved sharp-shadow marker and leading decoded placement
- id: world-shadow-v214
  resource: ../../evidence/catalog.json#E-c47192e28e88
  title: Retail-rebuilt enable-all payload and anomaly-marker implementation
- id: anomaly-marker-policy
  resource: ../../evidence/catalog.json#E-e6ba6fe9ef53
  title: reported-selected enable-all policy and spatial anomaly-marker design
- id: underground-selection
  resource: ../../evidence/catalog.json#E-d36504676e10
  title: reported-selected marked area and conservative definition exclusion policy
- id: runtime-setter-lead
  resource: ../../evidence/catalog.json#E-7207816130b3
  title: Community runtime setter opcodes, profile mismatch and evidence limits
- id: author-loader-suggestion
  resource: ../../evidence/catalog.json#E-b03fca6910dd
  title: Author-attributed DLL-only cbatch-loader suggestion and evidence limits
- id: underground-warning
  resource: ../../evidence/catalog.json#E-6a45902accc5
  title: reported-relayed community warning about Loop and Mad Mile underground lights
- id: untouched
  resource: ../../evidence/catalog.json#E-023ce687e992
  title: Base-world lights omitted by both reference archives
- id: decoded
  resource: ../../evidence/catalog.json#E-d8ef19db32ee
  title: Complete changed-light instance decoding and owning world locations
- id: decoder
  resource: ../../evidence/catalog.json#E-df9f699f89af
  title: Read-only native-format light instance decoder
- id: wlu-decoder
  resource: ../../evidence/catalog.json#E-39415b4944e5
  title: Bounded read-only WLU entity attribute decoder
- id: locations
  resource: ../../evidence/catalog.json#E-eee6652c0361
  title: Superseded file-token-only location follow-up
- id: audit
  resource: ../../evidence/catalog.json#E-c35f4e516e08
  title: Complete private world-shadow archive audit
- id: static-evidence
  resource: ../../evidence/catalog.json#E-aa168ba97a1e
  title: Captured-image load and reflection evidence
- id: inventory
  resource: ../../evidence/catalog.json#E-8f313f2d7474
  title: Every changed field and resource location
---

# Compared payloads and selection scope

Public World v2.2.0 enables the 12,788 audited definition flags in 1,883 batches.
Internal World v2.1.30 separately leaves 80 Pequino secondary definitions off
across 426 matched placements; see [targeted policy](secondary-streetlamp-shadows.md).
The corridor exclusions below are a superseded conservative policy, distinct from the later enable-all and targeted-exclusion experiments.
Loader/setter proposals remain unverified research.

# Confirmed role and scope

The two inspected community archives `batchmeshentity_v.09.rar` and `nensgfj.rar` only switch existing
compiled world-light definitions' `bCastShadow` from `0` to `1`. Comparison
against the installed windy_city base archive covers all 2,098 supplied files:
1,883 changed, 215 identical, 12,788 changed bytes. Every other byte and every
file size is unchanged. Patch/patch1 FATs contain none of these target paths.
There are no overlapping filenames between the archives.[^audit]

Large archive: 2,067 files, 1,859 changed, 12,731 flags enabled. Small archive:
31 files, 24 changed, 57 flags enabled. These are batch-definition counts,
not unique live-light or rendered-shadow counts. No light sources are added.
No source, build, package, install, or runtime modification was made.

# Static function and data mapping

Runtime identity for the following RVAs is the preserved
preserved evidence, SHA-256
`D8004145FB17BD6A9073466EBB9BFC19589AAD7D08D8EC3FD45733A5D8AD0855`.
Do not generalize these addresses to another profile without validation.

| RVA or field | Role and input/output boundary |
|---|---|
| `0x00759410` | Type-identity accessor for `CDynamicLightBatchProcessor`; type hash `0xC58A3AB9`. |
| `0x0073E4E0` | Processor load method; passes processor-owned definition at `+0x30` and read stream into `0x007C7F70`. |
| `0x007C7F70` | Reads leading definition data, then delegates shared light settings to `0x0259C960`. |
| `0x0259C960` | Stream-to-shared-light-definition loader; enum then two bytes, then aligned shadow distances. |
| `0x0259C9AC` | Stores the second byte into shared-definition `+5`. |
| `0x02599FEB` / `0x02599FF6` | Reflection registration names `bCastShadow` and supplies shared-definition offset `+5`. |
| cbatch processor-tag `+0x21` | Exact file location of that Boolean for all 12,788 observed edits; not a universal serializer rule. |
| `0x02599920` onward | Named light-type enum registration: 1=Omni, 2=Directional, 3=Spot, 4=Capsule. Changed records contain 1/3/4 only. |
| `0x0073E4E0`, instance `+8/+0x14/+0x20` | Deserializes processor-owned per-instance position, forward and up; serialized array tag `0xFB4B8BEB`, repeated count, variable curve keys, then vectors/extra fields. |
| `0x02598230`, `0x0259F870`, `0x00759F90` | Variable curve-key readers used by shared settings and batch instances; instance key-array tag `0x92B61304`. |
| `0x0076D830` / `0x007678D0` | Optional index-array loading; compiled-stream branch reserves backing storage without inline index payload consumption here. |
| `0x0079E0B0`, writes `0x0079E3EB..0x0079E415` | Transform updater writes the same instance position/orientation fields, corroborating vector roles. Arbitrary runtime parent/movement handling remains outside this audit. |

Evidence level is complete byte comparison plus named static engine load/
reflection mapping. Input is the serialized definition; output belongs to the
native light definition populated by its batch loader. It is a caster-enable
setting consumed through the engine's normal lighting path; downstream final
admission and rendering were not audited here. No runtime mutation was used.
`bCastShadowCurrentGen` was checked as an adjacent lead and is not this field.
[^static-evidence]

# Decoded world placements

All 12,788 changed definitions decode without errors into **49,592 stored light
instances**: 39,467 Omni, 7,457 Spot, 2,668 Capsule. Large archive contributes
49,452; small archive 140. Each record has XYZ/orientation and a definition/file
offset trace. This is not a unique simultaneous live-light or shadow count.
Streaming, mission and interior variants can differ or not coexist.[^decoded]

Every affected compound resource (1,883) has an exact `ExportPath` association
to a decoded WLU batch entity, covering 1,022 owning world resources. 47,018
instances belong to regular near/far resources; 2,574 belong to 114 named
location/mission resources. Confirmed named owners include Financial Circle,
Southside Campus and West Island cafes; downtown and other gun shops; Nikki's
house interior; auction house; stadium; Dot ConneXion; Aberration Lounge;
restaurants, pharmacies, hideouts and mission interiors. Full rows and a
searchable coordinate map are linked from the decode report.[^decoded]

The decoded positions already represent world placement in this corpus. Do
not add the WLU batch center translation again. The cafe position agrees with
independent authored door coordinates; all batch parent angles are identity.
An identity filename suffix is **not** evidence of local coordinates. Even the
single placeholder `-1,-1,+1,+1` resource holds 44 positioned mission lights,
with an identity parent at zero. Filename bounds are supporting provenance,
not replacement coordinates. No local-origin exclusion is justified here.

Evidence: exact native serializer/reflection mapping, hash-verified input,
strict array-tag/count/alignment/bounds checks, nonoverlapping parsed intervals,
finite vectors and normalized forward/up. The WLU reader preserves fully
parsed target entity nodes even where later unrelated data is unsupported
(212 of 2,354 files partially parsed). No failed node supplies an association.
2,195 placements cross-check against the original FCBastard reader with zero
identity/transform mismatches. Byte offsets, parse status and input hashes are
retained. This is static data ownership, not runtime rendering proof.[^decoder]
[^wlu-decoder]

# Ownership and safety

## Additional world lights omitted by the references

A 2026-08-31 read-only scan of 3,408 filename-resolved base compound cbatches
found **158 further disabled definitions / 496 stored instances in 29 omitted
files**: 398 Omni, 69 Spot, 29 Capsule. All have positive authored intensity/
radius and exact WLU owners. Confirmed owners include Rustville gun shop (59),
Pequino Village pharmacy (42) and pawn shop (35), Ravioli pharmacy (49), City Hall
clothing shop (23), Woodpark restaurant (9), an additional stadium HMA batch
(26), mission/interior records and regular world sectors. Per-light XYZ and
traces are preserved. No disabled definition was left untouched inside any
supplied file. Another 4,041 definitions / 12,443 instances were already
shadow-enabled in the base data, not new candidates.[^untouched]

All original changed offsets and supplied-file base hashes match. The same
reader accepts either Boolean through an explicit optional mode; its original
default still requires 1. Repeated processor hashes in trailing type-count
metadata are excluded only after position/descriptor/count validation: 2,111
entries agree with every light-containing file's decoded definition count.
Descriptors `c052120000000000` and `9051120000000000` are observed structural
signatures in this corpus, not new native RVAs or universal schema guarantees.
No unresolved payload decode errors remain. Patch/patch1 contain none of the
3,408 target paths. Unknown filenames, other archives/DLC worlds and non-batch
light systems are outside this scan. The additional false flags are editable
data-level candidates, not demonstrated runtime shadows or a completed implementation contract. Vehicle/particle lights remain separate subsystem boundaries.

## Later runtime setter lead

The supplied evidence included a community screenshot of a function labelled `setcastshadow`.
The visible wrapper increments RCX by0x20, calls a resolver, then writes DL to
returned-object `+0xD`. That opcode-level wrapper behavior is real; the label,
object type and field meaning are not independently established. The screenshot
provides only ASLR absolute addresses and "Ubisoft version", not a module base,
hash or profile. Its exact masked bytes do not occur in the saved Global mapped
image; raw regional-file negatives are inconclusive for protected code.[^runtime-setter-lead]

This lead matters as a possible later DLL application mechanism using the
static safe-selection manifests. It does not supersede batch selection or
solve underground exclusions. A global detour forcing argument2 to1 would be
blanket enablement and is prohibited: caller scope, deliberately disabled lights,
shared definitions and Loop/Mad Mile underground behavior are unresolved. Map
exact identity, callers, resolver, returned `+0xD`, live batch correlation and
fade readers first. The claim that fade is near this byte is unverified.

## Observer integration and unresolved timing

The subsequent
[integrated v2.1.2 world-loader observer](world-loader-probe.md) tests the Global virtual loader
boundary without changing any shadow or fading settings. Runtime timing and
selection remain unverified; this experiment does not establish blanket caster enablement or renderer publication.

An author-attributed suggestion proposed to modify the cbatch loader
for a DLL-only implementation, enabling false caster flags and setting a fade
distance. This aligns with the already mapped static load boundary but supplies
no hook implementation, runtime timing or supported-profile verification. Treat
it as a promising research route, not established runtime feasibility. Keep
selection batch-specific; a global shared-loader override could exceed reference
coverage and violate underground exclusions. Distance tuning would be a separate
change from the reference files, which changed only flags; no fade value or
underground fix is validated. Independent authorship remains required.[^author-loader-suggestion]

On 2026-09-02 The supplied evidence included the intended underground map location, selected the
old reference changes as the candidate set and directed a static conservative
selection without the v2.1.3 runtime identification test. The decoded world
point cloud was registered to the map geometry and the full marked corridor was
given a boundary allowance. Any definition with an instance in that polygon
remains false; mixed inside/outside definitions also remain false. The resulting
complete partition excludes 2,535 definitions covering 11,613 corridor
placements (177 mixed definitions) and marks 10,253 definitions eligible. This
regional policy knowingly leaves some surface lights inside the marked area
unchanged so the underground risk area cannot be enabled by the selection. Do
not copy reference payloads—derive edits from the audited differences and retail
baseline. Z is not used to identify underground membership.[^underground-selection]

The subsequent enable-all policy superseded the initial regional exclusion. The
selected first candidate enables all 12,788 audited reference-changed
definitions. A private diagnostic lets him arm a suspicious-shadow marker and
fire at the believed light fixture; the existing hash-checked tracer endpoint
carrier can record exact start/end/direction under a dedicated marker state and
log prefix. An offline resolver then ranks the decoded placements near that
endpoint and returns full definition/instance provenance for a later exclusion
update. Ambiguous marks remain multi-candidate. Database exclusions still apply
to a complete shared definition, so “one light” cannot mean one placement until
a per-object runtime setter is proven. The broad static corridor manifests stay
available as fallback evidence but are not the selected initial allowlist.
[^anomaly-marker-policy]

The unified v2.1.4 internal candidate implements this policy. Its build extracts
only compound batches from the installed `windy_city` base, validates every
audited base hash/size/HCTB tag and original false field before publishing, and
changes exactly the 12,788 planned bytes across 1,883 resources. An independent
post-build comparison confirms every difference is `00→01` at a planned
`bCastShadow` offset. No reference archive is a build input. A separate marker
arm state on the existing Global tracer hook logs exact aimed endpoints; the
offline resolver returns ranked placement/definition/WLU candidates and shared-
definition counts. This is static payload proof plus offline diagnostic proof;
runtime rendering, performance and visual acceptance remain separate checks.
[^world-shadow-v214]

On 2026-08-31 The recorded evidence includes a community warning against enabling shadows in
underground areas of the Loop and Mad Mile. The screenshot describes unspecified
undesirable behavior; no exact light IDs, locations, runtime build or reproduction
were supplied. This is an unverified third-party report, not The reported visual test
or a confirmed engine defect. The initial precaution left the complete marked corridor unchanged using a
static manifest; this was superseded by the enable-all plus targeted-marker policy. Do not infer
underground status from Z alone or exclude entire districts. Shared definitions
may affect both allowed and excluded instances; all 177 mapped mixed definitions
remain unchanged. That manifest was completed before the subsequent database enablement.[^underground-warning]

Fixture and world-location attribution are required for selective changes. The earlier file-token-only report is superseded by complete
per-light positions and owning world-resource links. Physical lamp-mesh identity
is not established for every light: 350 definitions / 716 instance rows match
preserved prototype type/colour/intensity/radius, but these are **settings-only
candidates**, sometimes ambiguous. Newspaper/advertising fixtures, garden,
Bloom, hideout and stadium lights appear among those candidates. Never label
all spots streetlamps or all capsules neon solely from the enum. No UI district
boundaries or teleport-safe destinations are claimed. Decoding alone does not establish a safe runtime policy.
[^decoded]

These are `worlds/windy_city/generated/batchmeshentity/*_compound.cbatch`
resource edits, separate from Addons' vehicle databases/entity-library payload.
Brightness, placement, colour, radius, specular, shadow distances and unrelated
sector data are unchanged. The reference archives supply no code, shaders or
textures. No reference payload may be treated as independently authored Addons
source. Future work must derive its own selection/edits from an appropriate
baseline rather than incorporate these files by implication.

The installed base archive was not authenticated against retail media. Static
enablement does not prove visual output, acceptable cost, safe interaction with
other sector mods, or compatibility with any engine candidate. Extra casters
may add workload; visual and workload results require runtime evidence. The records'
stored shadow distances remain unchanged, including many `1000/0` pairs;
these are not measured effective in-game ranges.[^audit]

On 2026-09-02 Runtime feedback reported a newly enabled world-light shadow with an overly
sharp edge and confirmed that the marker shot destroyed the physical lamp. The
complete log shows that Addons recorded the tracer's 148.231-metre visual end,
not the lamp collision point. The original endpoint-only resolver therefore
failed. Shot-segment ranking finds Omni instance 5 at
`1809.1345,868.6995,73.2674`, only 0.4401 metres from the ray and 1.4402 metres
from its start. It is the leading spatial attribution: near-sector resource
`wlu_data_near862.xml.data.fcb`, compound processor tag `0x5BE0`, shared by ten
placements, intensity/radius `6/6`, with authored maximum/fade distances
`1000/0`. This is strong static correlation plus the destroyed-fixture report,
not a captured runtime light pointer.[^sharp-marker-1]

The offline resolver now ranks against `start`-to-`endpoint` when the complete
log supplies both vectors and retains endpoint-only fallback for legacy records.
Offline coverage proves both modes and shared-definition counting. Future marker
analysis must preserve and use the complete log rather than the short status
line. Every candidate also carries an exact map query derived from its batch
resource, processor tag and instance. The coordinate viewer accepts that query,
centres and rings the resolved light, and opens its full record. This completes
the diagnostic logger-to-map handoff without depending on a Shadow Engine
runtime identity diagnostic. The diagnostic correction no longer presents
the tracer endpoint as the marked lamp coordinate; its status requests the
complete log while retaining full start/end/direction data in bounded logging.
[^sharp-marker-1]

The same named reflection map confirms per-light fields
`fCastShadowMaxDistance` (`+0x44`), `fCastShadowFadeDistance` (`+0x48`) and
`bHighResShadowFiltering` (`+7`) in the shared definition. Their existence does
not prove the final runtime distance or that the high-resolution flag controls
penumbra softness. An earlier isolated Addons field test still showed hard local
shadow edges, so softness remains an unresolved shader/filtering question rather
than a justified database edit.[^sharp-marker-1]

Full file paths, zero-based offsets, hashes and original/new values are in the
private change inventory (preserved evidence).

[^audit]: Complete private world-shadow archive audit
[^static-evidence]: Captured-image load and reflection evidence
[^locations]: Location follow-up; no fixture-level world map established
[^decoded]: Complete instance decoding, world ownership inventory and limits
[^decoder]: Native-format instance decoder and preserved disassembly provenance
[^wlu-decoder]: WLU entity parser with fully validated target nodes and partial-file status
[^untouched]: Additional false-shadow world definitions, positions, counts and verification limits
[^underground-warning]: Preserved community screenshot, evidence limits and proposed selection precaution
[^author-loader-suggestion]: Author-attributed native-loader proposal; no runtime or implementation proof

[^runtime-setter-lead]: Preserved screenshots, visible opcode semantics and local profile comparison

[^underground-selection]: Marked area, decoded definition locality and conservative mixed-definition rule
[^anomaly-marker-policy]: Enable-all selection, marker workflow and definition-granularity limit
[^world-shadow-v214]: Unified build, exact retail mutation proof, marker/resolver tests and runtime limits
[^sharp-marker-1]: Shot-segment marker resolution, leading placement metadata and quality-field limits

The internal30 experiment in [secondary streetlamp shadow exclusions](secondary-streetlamp-shadows.md)
retains lower-lamp illumination while leaving 80 selected caster flags off across
426 matched placements. PCSS29 is retired after reported warnings and no
discernible visual improvement; its implementation remains archived.
