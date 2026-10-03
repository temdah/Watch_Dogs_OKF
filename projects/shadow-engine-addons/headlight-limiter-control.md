---
type: Runtime Control Contract
title: Vehicle Headlight Shadow Limiter NexusTools Control
description: Supported cross-mod ABI, Addons ownership, failure policy, and verification boundary
  for the vehicle-headlight limiter toggle.
tags:
- shadow-engine-addons
- shadow-engine
- nexustools
- headlights
- runtime-control
status: draft
sources:
- id: shadow-engine-api
  resource: ../shadow-engine/architecture/control-api.md
  title: 'Asynchronous native control ABI: request, receipt and application'
- id: addon-adapter
  resource: ../../evidence/catalog.json#E-44460ab19b0d
  title: Rejected v2.1.7 Addons native ABI adapter
- id: menu-control
  resource: ../../evidence/catalog.json#E-5decfc6be562
  title: Rejected capture-free Addons control owner
- id: offline-tests
  resource: ../../evidence/catalog.json#E-64f7481659ff
  title: Rejected v2.1.7 control ABI offline tests
- id: build-report
  resource: ../../evidence/catalog.json#E-9e301f19852c
  title: Capture-free v2.1.7 build and package evidence
- id: crash-result
  resource: ../../evidence/catalog.json#E-bf63e4cae5af
  title: v2.1.5 pre-game crash and registration-timing hypothesis
- id: v216-crash
  resource: ../../evidence/catalog.json#E-62c215f23f78
  title: v2.1.6 load-game crash and embedded Lua fault mapping
- id: v217-crash
  resource: ../../evidence/catalog.json#E-b599e530c2b3
  title: v2.1.7 repeated fault and rollback
---

# Historical rejected control carrier

This maps the v2.0.35 engine ABI and rejected Addons v2.1.5–2.1.7 UI carriers.
It is not the current numeric/saved limiter contract or a current Addons feature.
Fault-address agreement does not establish the Lua corruption mechanism; see
[Lua frame attribution](lua-frame-attribution.md). The technical ABI and failure
tests remain useful provenance.

# Ownership and ABI

Shadow Engine v2.0.35 owns the limiter state and exports a stable version-1
native interface: API version, getter, and setter. Addons owns only the
NexusTools presentation and an isolated adapter. It finds the already-loaded
`ShadowEnginePatch.asi` through `GetModuleHandleW` and named exports through
`GetProcAddress`; it does not inspect or patch Shadow Engine memory.[^shadow-engine-api]

The Shadow Engine default is enabled on every process launch. Zero disables
candidate suppression and nonzero enables it. Disabling leaves vehicle
publication, classification, and telemetry running and does not affect sirens,
world lights, lifecycle, quality, capacity, caches, or atlases.[^shadow-engine-api]

# Addons state and failure policy

The native adapter owns cached module/export identity and a failure latch. The
existing Addons Script performs a first getter read and rate-limited 120-update lazy
retries until registration succeeds. A changed module identity clears cached
discovery and the latch. Repeated unchanged discovery states do not repeat
logs.[^addon-adapter]

Lua registers **Vehicle Headlight Shadow Limiter** only after a successful
getter read and passes that confirmed value as the NexusTools initial state.
Every toggle invokes the setter and a native getter confirmation before showing
Enabled or Disabled. Module absence, a missing export, API version other than
1, invalid getter output, setter rejection, or confirmation mismatch displays
Unavailable. No shortcut or persistent Addons default exists.[^menu-control]

v2.1.7 replaces the rejected control object's retained callbacks. NexusTools
holds one function with zero Lua upvalues; it resolves a global dispatcher only
when invoked. Script-owned state contains only the active handler and scalar
view state, and unload removes the dispatcher. Registration remains outside
Layout. No retry button or closure capturing the control object, menu or `self`
is present. This targets the observed Lua lifetime boundary but does not prove
the exact prior fault without a dump.[^build-report]

Runtime rejects that correction. Windows recorded a fourth identical
`Disrupt+0x001C7CC2` access violation. Crash-session Addons logs were removed by
the immediate v2.1.4 restoration and no dump exists, so setter execution and
the exact invalid object remain unknown. The result rejects Layout timing,
captured `self`/menu/control tables, and the zero-upvalue dispatcher distinction
as sufficient causes. Active source is v2.1.4 and contains no limiter carrier;
do not build another Addons-side registration variant unchanged.[^v217-crash]

v2.1.5 incorrectly registered the Boolean from inside the NexusTools layout
callback. Runtime feedback rejected that build after two matching pre-game crashes;
v2.1.4 works. v2.1.6 registers during the normal pre-layout phase and keeps an
explicit late-module retry outside layout construction. An offline invariant
now rejects any command registration while a layout callback is active. The
registration misuse is the leading cause, not proven attribution for the
observed Disrupt fault.[^crash-result]

That hypothesis is rejected by v2.1.6 runtime. The runtime reached the main menu but crashed after Load Game at the identical RVA. Logs prove the getter returned
enabled, the setter never ran, and the world-loader observer processed zero
batches. The fault maps to Disrupt's embedded Lua hash-table node lookup, not a
shadow function. Without a dump, the exact invalid Lua object or earlier
corrupting event is unknown. The common v2.1.5/v2.1.6 Lua/native carrier is
retired; v2.1.4 remains the working fallback.[^v216-crash]

# Evidence boundary

The native harness covers missing module, all three missing-export cases, wrong
version, both reads, enable/disable, failed setter, and false-success getter
confirmation. Lua tests cover getter-derived registration, zero callback
upvalues, a confirmed change, late-module discovery, setter failure and unload
cleanup. Package verification proves the unified six-file NexusTools layout
and twelve bridge exports.[^offline-tests][^build-report]

These gates prove adapter policy and packaging. They do not prove NexusTools UI
behavior or Shadow Engine visual behavior in Watch Dogs; The runtime report
remains required.

[^shadow-engine-api]: Shadow Engine runtime control ABI and behavioral scope
[^addon-adapter]: Lazy discovery, bounded logs, state ownership, and fail-closed behavior
[^menu-control]: Getter-derived registration and post-set confirmation
[^offline-tests]: Native injected-platform failure and success matrix
[^build-report]: Unified package and retained-payload verification
[^crash-result]: The rollback control, Windows events, evidence limits, and v2.1.6 correction
[^v216-crash]: Exact active hashes, bounded logs, repeated fault, Ghidra role mapping, and rejection
[^v217-crash]: Fourth identical fault, rejected lifetime correction, evidence loss boundary, and v2.1.4 rollback
