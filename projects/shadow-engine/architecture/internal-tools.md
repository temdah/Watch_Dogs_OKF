---
type: Internal Diagnostic Contract
title: Lua-to-native bridges and shared-control ownership experiments
tags:
- shadow-engine
- diagnostics
- menu
- runtime-control
- cleanup
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-c681b34977c2
  title: Corrected .75 runtime, H3/H5 acceptance, H8 closure and settings-continuity request
- resource: ../../../evidence/catalog.json#E-650f8fa72d27
  title: Passed .74 offline gates; no standalone runtime test claimed
- resource: ../../../evidence/catalog.json#E-ab6fdb75eac9
  title: Positive .73 gameplay and H4 with confirmed H3 diagnostic blocker
- resource: detail-window-observation.md
  title: Explicit Detailed Observation Windows
- resource: periodic-summary-transport.md
  title: Worker-Owned Periodic Summary Output
- resource: ../../../evidence/catalog.json#E-e7bd6b8dce8a
  title: reported-positive72 runtime baseline and measurement scope
- resource: ../../../evidence/catalog.json#E-06078fbd86b8
  title: 69 three-window measurements, lifecycle and duplicate notification finding
- resource: https://www.kaverti.com/en/TroploNexusTools/Lua/Script
  title: NexusTools Script lifecycle callback contract
- resource: https://www.kaverti.com/en/TroploNexusTools/Lua/SH_Menu
  title: NexusTools Layout Rerender contract
- id: private-full-crash-capture
  resource: ../../../evidence/catalog.json#E-e463e89671b2
  title: Matching dump evidence and recorded full-memory capture
- id: private-fixed-menu-v251
  resource: ../../../evidence/catalog.json#E-3ff7c45f6952
  title: v2.0.50 crash rejection and fixed-slider correction
- id: private-fixed-baseline-v250
  resource: ../../../evidence/catalog.json#E-d04bec212810
  title: Fixed-only vehicle/world controls
- id: private-world-transport-v248
  resource: ../../../evidence/catalog.json#E-6d378fb10e97
  title: Explicit world-settings transport correction
- id: private-world-tier-v247
  resource: ../../../evidence/catalog.json#E-239a5e38a4a6
  title: Independent world-light controls and policy
- id: private-cleanup-v244
  resource: ../../../evidence/catalog.json#E-54d97d70abb6
  title: Internal and Release profile validation
- id: private-startup-crash-v242
  resource: ../../../evidence/catalog.json#E-22aef7dc072d
  title: Confirmed crash event and attribution limits
- id: private-resolution-v241
  resource: ../../../evidence/catalog.json#E-3ee5002942df
  title: Selectable resolution validation and comparison scope
- id: private-suite-v240
  resource: ../../../evidence/catalog.json#E-564783b1f228
  title: Slider and traffic ownership migration preflight
- id: private-working-r2
  resource: ../../../evidence/catalog.json#E-adc3508b9dfe
  title: Live r2 controls and corrected launch classification
- id: private-r2-rejection
  resource: ../../../evidence/catalog.json#E-433c59a3d55e
  title: Rejected r2 and no-op Lua isolation
- id: private-tools-r2
  resource: ../../../evidence/catalog.json#E-aea695e146ba
  title: Startup-isolated Lua companion revision
- id: private-autostart-isolation
  resource: ../../../evidence/catalog.json#E-d3806eddb282
  title: Same-ASI launch control and companion-only package
- id: private-launch-rejection
  resource: ../../../evidence/catalog.json#E-82ad24c8a657
  title: reported launch rejection and read-only log diagnosis
- id: private-contract
  resource: ../../../evidence/catalog.json#E-78c26e1ddcf4
  title: Sanitized ownership and protocol contract
- id: private-preflight
  resource: ../../../evidence/catalog.json#E-d435e6eff393
  title: Lookup and rejected-carrier review
- id: private-previous-runtime
  resource: ../../../evidence/catalog.json#E-24a531ddd73f
  title: Preserved v2.0.38 Global log
- id: private-result
  resource: ../../../evidence/catalog.json#E-9059a60438ff
  title: Candidate validation and remaining work
- id: private-rejected-carrier
  resource: ../../shadow-engine-addons/headlight-limiter-control.md
  title: Vehicle Headlight Shadow Limiter NexusTools Control
- id: public-vehicle-tier-result
  resource: ../../../evidence/catalog.json#E-3fbd10671774
  title: Distance-tier tools protocol and runtime policy
- id: public-packaging
  resource: ../../../evidence/catalog.json#E-fb5a52ebca8d
  title: Separate ASI and tools packaging
- id: public-policy
  resource: ../../../evidence/catalog.json#E-4d0df9a99489
  title: Atomic policy control owner
- id: public-transport
  resource: ../../../evidence/catalog.json#E-8e4b6b03d025
  title: Native-worker bounded request transport
- id: public-menu
  resource: ../../../evidence/catalog.json#E-b6e7111dd577
  title: Pure-Lua internal presentation
- id: public-tests
  resource: ../../../evidence/catalog.json#E-1d96748bfdb8
  title: Fake-filesystem menu contract test
- id: public-quality
  resource: vehicle-shadow-quality.md
  title: Vehicle Shadow Quality Boundary
---

# Bridge used in the experiments

The Shadow Engine experiments used ordinary NexusTools Lua commands and a
native-owned file mailbox. Lua owned menu objects and scalar request state;
native code owned validation, persistence and policy. A pinned worker polled
every 250 ms and wrote status only when it changed. Engine hooks performed no
mailbox I/O and background work never dereferenced stored engine pointers.

Requests used a fixed adjacent path, bounded input, temporary-file rename and
one in-flight sequence. PID/session checks, replay rejection and terminal errors
prevented stale requests from changing a later run. This local diagnostic input
was not an authentication boundary. [The ABI](control-api.md) and
[persistence experiment](saved-settings.md) describe the separate completion states.

# Rejected carriers and attribution mistakes

Early custom Lua/native carriers were replaced with the simpler bridge above.
Inconsistent launch results during companion/no-autostart/import controls did
not identify a manifest or Lua defect; the later successful control superseded
that attribution. A loader log ending without a fatal marker did not establish
why loading stopped.

Several later faults occurred at Global embedded-Lua lookup `0x001C7CC2` before
any quality request. Unique slider labels still faulted; disabling autostart
allowed the same save to load. A `menu:Layout` call also failed because the menu
owner was not a layout container; using `category:Layout` corrected that API
mistake but did not eliminate the separate native fault.

A delayed-registration watcher was blamed, then removed; the fault persisted.
One failing run had not reached any registration marker. This rejected simple
watcher/category/quality-policy explanations. The later captured heap identified
a table-tagged child aliasing the Lua concatenation buffer and a prototype frame
mismatch. See [Lua frame corruption](lua-stack-compatibility.md). A different
session's loader log cannot explain an earlier crash.

# Independent diagnostic lifetimes

Detailed event windows, performance measurements and population recording have
separate serials and completion states. A UI timer or a completed workload report
cannot certify another recorder's saved output. The whole-pass recorder sampled
for 60 seconds without requiring a human to mark a brief visual event. Optional
annotations did not identify the exact visible light. Native state remained the
completion authority; see [population observation](population-observation.md).

# Ambient traffic control

The observed Lua `ChangeVehiclesBudget(0)` / `RestoreBudgets` mechanism affects
ambient moving-traffic spawning. It does not remove existing, parked or scripted
vehicles. One owner remembered whether its suppression succeeded and restored
only its own change during cleanup. Two independent mods restoring a global
budget can undo each other's policy, so successful API calls alone are not
evidence of compatible ownership. This Lua budget control is separate from
native headlight selection and shadow-resource capacity.

# Limits

Desktop Lua fixtures, register-budget checks and native builds do not certify
the modified target VM. Configured quality does not establish backing-resource
replacement. Lower submitted face counts do not measure FPS. Preserve separate
native-call, resource, renderer and visual evidence when evaluating a bridge.
