---
type: Native Compatibility
title: Regional native boundaries for storm, graphics and world-loader extensions
tags:
- compatibility
- native-abi
- shadow-engine-addons
status: stable
sources:
- resource: ../../evidence/catalog.json#E-addons-five-build-delivery-20261004
  title: Both compiled data units and final package/prototype regression evidence
- resource: ../../evidence/catalog.json#E-addons-five-build-native-20261004
  title: Five-image mapping, source controls and actual C gate tests
- resource: basic-lightning.md
  title: Native weather, scheduler and sky publication ownership
- resource: storm-audio-loading.md
  title: Environment collector ownership and retained resources
- resource: graphics-activation-and-streaming.md
  title: Completed graphics state and producer/published views
---

# Evidence boundary

These are static mappings for the five identified Disrupt images, independently
checked for Addons' own hooks and dependencies. Provider-mod compatibility does
not validate a receiving extension's addresses. The evidence retains each input
SHA256, PE timestamp/size/checksum/entrypoint and raw-versus-mapped interpretation.
Global, A4EE and Asia use mapped captures; VMPless and Complete use raw PEs.
No new manual gameplay, visual, audio or crash-free acceptance is claimed.

# Regional role map

Values below are RVAs, not absolute addresses. Calling convention is Windows x64;
float arguments keep their positional XMM registers. The frozen evidence contains
the remaining callsites, signatures, globals, vtables and field contracts.

| Semantic role | Global | A4EE/Shev | VMPless | Complete | Asia/Miru |
| --- | --- | --- | --- | --- | --- |
| Projectile tracer / borrowed native arguments | `00B59760` | `007232E0` | `0073D9F0` | `01B6E8A0` | `006CC7B0` |
| Sky update / three arguments and native publication context | `00A53860` | `0061B400` | `00631A00` | `01A6F000` | `006800B0` |
| Environment update / four arguments, native Moon first | `00A2F7E0` | `005F7380` | `0060D980` | `01A4AF80` | `0066CA80` |
| Sky publication / key and output pointers | `00A15180` | `005DCD20` | `005F3320` | `01A30920` | `00660970` |
| Lightning scheduler / private state and output | `00A24DE0` | `005EC980` | `00602F80` | `01A40580` | `00668CE0` |
| Curve evaluator / float x, knots, count | `00498530` | `002F9D30` | `00302C90` | `00450FC0` | `00294610` |
| Tagged resource copy / destination and source handles | `008B3CD0` | `0189B930` | `0026F660` | `0166A4D0` | `003CAFC0` |
| Environment dependency collector / borrowed collector | `009FC8E0` | `005C4480` | `005DAA80` | `01A18080` | `00652120` |
| Sound resource acquisition / event ID and collector | `00275DC0` | `00D30820` | `00D54C20` | `021BA790` | `00D13C70` |
| Loaded database-manager pointer | `03B59050` | `03B6A2C0` | `0489DAC0` | `03BC1EF0` | `03A39D18` |
| Completed lightning settings record vtable | `02F520C0` | `02ED3490` | `03D10B60` | `030C9D80` | `02DA85F0` |
| Completed environment resource-owner vtable | `02E59100` | `02EACDD0` | `03CE9F00` | `030A6D20` | `02D67980` |
| Six-argument native sound submission | `002BBFE0` | `00D72AE0` | `00D97850` | `021FC840` | `00D2C7E0` |
| Existing entity-reference map pointer | `03B5B1A8` | `03B6C1F8` | `0489F9F8` | `03BC3C78` | `03A3B628` |
| Completed graphics-component vtable | `02F17D30` | `02E8E0C0` | `03CCABC0` | `0308A730` | `02D2F0F0` |
| World batch loader / processor and stream | `0073E4E0` | `00249420` | `00250550` | `016BC3E0` | `00416E20` |
| World batch loader virtual slot | `02EFE900` | `02E74900` | `03CB1060` | `03072C60` | `02D642F0` |

# Structure and ownership proof

After masking only relative call/branch destinations and RIP displacements, the
entire traced code regions for sky update, environment update, scheduler, state
construction, lightning-record construction, container addition, graphics
construction/update/synchronization, geometry parsing/loading, LOD selection,
entity activation, audio submission and world batch loading match across all
five images. Data-field offsets, widths, registers, constants and non-address
instructions remain fixed. All four displaced hook prefixes contain complete
instructions and require no relative relocation.

Loaded-record lookup has differing protected-call sequences but the same14
non-stack memory-access operations and typed-resolver relationship. Tagged
resource copy retains the same first160-byte implementation, including tag masking,
retain/release and virtual ownership calls. Its adjacent routine is not part of
the resource-copy ABI. Asia uses a different sound-resource helper and inlines
the resource-owner setup; each is bound through its caller/constructor and exact
regional bytes. Existing fields and lifetimes are detailed in the linked owning
concepts, rather than inferred from a uniform RVA delta.

The storm service owns its private state/settings/output copies. Native Moon
selection remains untouched. Native environment collectors own resource retention
and release. Entity/graphics views and the sound singleton remain borrowed;
no observer retains pointers after its bounded copy. Producer and published
renderer views are distinct. Geometry readiness fields do not prove GPU residency.

# Failed identification shortcuts

A matching collector forward/add vtable pair is ambiguous: many native classes
share those methods. Constructor references resolve the actual container.
The first vtable installed by a constructor can be its base class. Existing
resource-request and weather tests rejected initial mappings to those temporary
tables; final stores identify the completed resource owner and lightning record.

PE exception metadata can split one native routine into several contiguous
unwind fragments. Fingerprinting only its first fragment can validate little more
than a prologue. Joining contiguous regions preserves the relevant implementation,
but may also include an adjacent routine; callsite/return analysis still matters.

# Automatic gates and manual calibration

Both public and internal compiled C data units were exercised against all five image files without
loading or executing game code. Independently corrupted code regions, vtable links
and four identity fields are rejected. Relocated-base simulations pass. Exact
regional bytes and cross-references are checked before runtime mutations; unknown
or ambiguous identities fail closed. Immutable public data contains only public
code checks, while internal diagnostic mechanisms remain outside public compilation.

Native boundary fingerprints distinguish calibration from repeated release tests.
Changed profiles, layouts or native ABI implementation require renewed human runtime
validation. An automated PASS does not supply that calibration. Historical Global
feature observations cannot establish acceptance of a new regional initializer.

Every shipped Lua file is recursively inspected with the bundled auxiliary float
Lua5.1 compiler: maximum31 registers,15 upvalues and15 fixed parameters. The examined
internal bundle has120 prototypes with maxima23/14/3, including nested closures.
Negative32-register/16-upvalue/16-parameter controls are rejected. This inspection
is separate from target-VM execution and the independent NexusTools string bridge.

The public bundle contains6 prototypes with maxima17 registers,3 upvalues and1
fixed parameter. Edition comparisons retain byte-identical shared assets/runtime
within each audience; compiled public exports exclude internal diagnostics.
