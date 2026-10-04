---
type: Engineering Convention
title: Nexus Tools Extension Authoring
description: Reusable ownership, registration, feedback, packaging, and validation rules for
  independent in-game Nexus Tools menus.
tags:
- nexus-tools
- lua
- menu
- commands
- interoperability
status: draft
sources:
- resource: ../evidence/catalog.json#E-shadow-a4ee-addons-menu-20261004
  title: A4EE native initialization rejection before Addons menu registration
- id: lua-frame-finding
  resource: ../projects/shadow-engine/architecture/lua-stack-compatibility.md
  title: WD1 Lua Packed Frame Size and Garbage Collection
- id: lua-frame-repair
  resource: ../projects/shadow-engine/compatibility/lua-frame-repair.md
  title: Internal Lua Frame Repair Candidate
- id: current-shadow-menu
  resource: ../evidence/catalog.json#E-b6e7111dd577
  title: Current independent categories, staged controls and acknowledged requests
- id: menu-controller
  resource: ../evidence/catalog.json#E-a760a8854c3b
  title: Shadow Engine Addons menu owner
- id: command-core
  resource: ../evidence/catalog.json#E-a955e484d12d
  title: Shadow Engine Addons command utilities
- id: lua-bundler
  resource: ../evidence/catalog.json#E-509f73fe535f
  title: Shadow Engine Addons Lua module bundler
- id: v1030-result
  resource: ../evidence/catalog.json#E-25f57e8e704f
  title: v1.0.30 menu coexistence and notification field result
- id: v1025-build
  resource: ../evidence/catalog.json#E-1313879dd200
  title: Rejected v1.0.25 live-control experiment
---

# Ownership model

This is workspace-derived guidance, not official NexusTools documentation or a
guarantee of compatibility. Verify API signatures against the installed host's
documentation/bindings. The Lua safety section below applies independently of
which mod registers a menu; it does not establish fault ownership for another mod.

Give menu registration one owner. That module alone calls
`SH_Menu_RegisterMenu`, creates categories, registers commands, assigns layout
callbacks, and returns the resulting menu handle. Feature metadata, native
loading, diagnostics, and command utilities remain separate modules. This
prevents an unrelated feature module from accidentally recreating or replacing
another mod's menu state.[^menu-controller]

Use a collision-resistant prefix for every command ID, such as
`SCA_8F31C6D2_`. Never reuse another mod's IDs or generic names such as
`Environment`, `Weather`, or `Enabled`. Centralize ID construction so every
registration and state read uses the same spelling.[^command-core]

# Safe registration pattern

1. Register one uniquely named menu and retain its handle.
2. Register categories against that handle only.
3. Register each Boolean once with a unique ID, label, description, menu
   handle, default value, and callback.
4. Render it with `root:CommandWidget(commandId)` inside the owning category's
   layout callback.
5. Read Boolean state through `SH_Commands_GetStateBool` inside a protected
   call. The command callback observes the already-updated value.
6. Guard the entrypoint against duplicate loading when the environment can
   evaluate the same script more than once.

Do not make registration order a cross-mod dependency. Independent menus must
coexist regardless of whether Trainer, Living City, or the extension loads
first. The v1.0.30 field test showed Shadow Engine Addons, Trainer, and Living City
present together while the Addons callback produced its notification.[^v1030-result]

# Immediate feedback

Distinguish staged, queued, applied and failed states. A notification that a
request was queued is not proof that its backend applied it. Use action buttons
for captures, toggles for Boolean state and sliders for bounded values. Group
controls into clearly named categories/sections; in the current Shadow Engine
implementation layouts belong to categories, not the top-level menu handle.
Keep registration out of drawing callbacks and do not send repeated mutations
while a slider is being drawn or dragged. Preserve menu/command/callback owners
until their documented teardown boundary.[^current-shadow-menu]

Every user action should acknowledge itself through
`SH_Notifications_PushNotification` when available, while logging the command
ID, resulting state, and scope. Layout text may be reconstructed only when the
page is reopened, so the notification is the authoritative immediate feedback.
The extension must fail softly if the notification function is absent.

State truthfully what changed. A UI test must say that lighting is unchanged;
it must not resemble a functioning feature toggle. The successful v1.0.30
control changes only explanatory text and emits a visible notification.[^v1030-result]

# Runtime capability boundary

Expose a live feature control only when it has a proven reversible runtime
backend. Archive-backed `.lib`, `.dat`, and `.fat` changes are static for the
running session unless a validated database reload or mutation API is found.
A menu Boolean cannot by itself alter already-loaded database objects.

The rejected v1.0.25 experiment installed hooks but observed zero matching live
objects, so its controls were inert. It also coincided with missing Trainer
categories and must not be copied as a valid live-control design.[^v1025-build]
Until a real reversible boundary exists, show archive features as status and
keep diagnostic/UI-only controls explicitly separate.

# Modular source, single runtime entrypoint

Develop responsibilities as ordinary Lua modules. When Nexus Tools expects one
autostart file, bundle the modules into `package.preload` entries and append a
small entrypoint. The generated file is an artifact; edit and review the source
modules instead.[^lua-bundler]

For optional native code, let one bridge module own `package.loadlib`, exported
function discovery, error handling, and capability reporting. Menu code calls
that stable bridge interface and does not load DLLs directly.

# Validation checklist

## WD1 Lua frame safety: not a menu-item limit

The captured Global Lua compiler accepts requirements below250 but stores the
frame maximum in five bits. A constructor requiring51 registers declared19;
the VM then exposed only19 slots to stack marking. The isolated native test
reproduces loss of GC visibility before table children are published. Item24
was the observed victim, NOT a24-item/category/widget limit. Total menu size,
source lines, number of locals and register demand are not interchangeable.
The faulty native instruction ranges also exist in a working configuration;
allocation/GC timing can expose a latent defect elsewhere.[^lua-frame-finding]

For new tools targeting the unpatched runtime:

* Prefer small cohesive functions and incremental construction of large data
  tables over large list literals of nested tables. Keep all entries/functions;
  split their construction, not the feature set. Publish each completed child
  into a strongly owned parent before constructing the next where practical.
* Reduce simultaneous temporaries, large argument lists and deeply nested
  expressions. A helper or incremental constructor is a mitigation candidate,
  not a guarantee: its own frame, caller and nested functions still matter.
* Inspect the final generated/autostart chunk and every nested prototype using
  the target compiler's semantics. On the mapped unpatched runtime, required
  frame size must fit31 and agree with declared size. Inspect implicit register
  ranges as well as explicit operands. A highest-NEWTABLE scan, a wrapped
  maxstack field, or success under desktop Lua cannot certify this invariant.
  A complete automatic packaged-bytecode gate is not supplied by this guide.
* Independently keep captured upvalues and fixed parameters at15 or fewer per
  prototype. Both counts occupy four-bit fields in prototype byte0A. A12-register
  function capturing16 variables is still invalid. Source/compiler evidence and
  producer/consumer roles are in the [packed metadata finding](../projects/shadow-engine/architecture/lua-stack-compatibility.md#independent-four-bit-upvalue-and-parameter-counts).
* Keep modules separate when bundling; do not flatten them into one enormous
  function. Verify the packaged artifact, not only the source modules.
* Do not disable GC, periodically force GC as a shipping workaround, swallow
  native access violations with pcall, or remove menu functions to call this fixed.
  Lua error protection does not repair native memory corruption.

Shadow Engine .57 tests a coherent17-site shared-runtime repair and retains .56
tools unchanged. It is Internal/Global-only, excluded from Release, and still
has startup-synchronization, metadata-ownership and lifecycle gates. Do not
make other mods silently depend on it or copy/install a second runtime patch.
A reusable host-level fix needs a single coordinated owner and explicit version
compatibility; NexusTools introducing the defect has NOT been established.
[^lua-frame-repair]

## Crash investigation and acceptance

Preserve logs and exact module/script versions before changing the candidate.
Separate ordinary Lua/API errors, menu ownership/ID collisions, blank-layout
errors and native crashes. For the latter, compare module identity and relative
fault location, then frame requirements, live object ownership and GC evidence;
the same table-lookup RVA alone does not prove the same cause. A menu change
that shifts allocations is not necessarily the corrupting operation.

Use existing crash evidence first. Do not repeat a full live-process capture by
default: the earlier working-control attempt coincided with a hang. Record
missing evidence rather than guessing. Controlled comparisons keep the save,
host, other mods and instrumentation identical, changing one owned variable.
Isolation experiments must preserve unrelated tools and their registration state.

Validate cold starts/save loads, all retained functions, page reopen/unload and
coexistence with other menus. Record success separately from long-run safety,
regional support and causal proof. .57 has one user-reported successful run
with confirmed activation and a completed menu capture; that does not attribute
Addons crashes or certify every API/tool combination.

## Menu delivery checks

Before handing off a menu build:

* prove there is exactly one menu-registration owner and one registration per
  command ID;
* search the packaged entrypoint for duplicate or foreign command IDs;
* open Trainer and other installed menus before and after using the extension;
* toggle each control repeatedly and confirm its notification and logged state;
* close and reopen the page to confirm reconstructed layout state;
* confirm UI-only controls do not invoke native or database mutation paths;
* confirm live controls fail open when their backend is unavailable;
* verify the bundled entrypoint is byte-identical to the packaged file; and
* treat runtime coexistence and action effects as separate test results.

[^menu-controller]: Shadow Engine Addons menu owner
[^command-core]: Shadow Engine Addons command utilities
[^lua-bundler]: Shadow Engine Addons Lua module bundler
[^v1030-result]: v1.0.30 menu coexistence and notification field result
[^v1025-build]: Rejected v1.0.25 live-control experiment
[^lua-frame-finding]: Captured frame contract and bounded proof, not every crash's cause.
[^lua-frame-repair]: Experimental compatibility scope and remaining release gates.
[^current-shadow-menu]: Current Shadow Engine-owned UI and request lifecycle.

# Regional initialization and missing menus

A missing extension menu need not indicate a registration collision. In the
A4EE Addons2.1.48 run, native storm initialization returned UNAVAILABLE and the
Lua entrypoint returned before registering its menu. Its native runtime gate
requires Global PE timestamp5CD045B4/image size6595000; A4EE fails that identity.
Restoring menu availability and porting native capabilities are separate work:
keep independently usable controls available, clearly disable unsupported native
actions, and prove regional function/layout contracts before enabling them.
Merely allowing another timestamp does not make Global addresses portable.
