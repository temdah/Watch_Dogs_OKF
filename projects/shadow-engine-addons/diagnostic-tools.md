---
type: Diagnostic Operating Contract
title: NexusTools menu coexistence and diagnostic attribution experiments
tags:
- shadow-engine-addons
- diagnostics
- nexustools
- lightning
- hdri
status: draft
sources:
- id: public-v210
  resource: ../../evidence/catalog.json#E-301ee65332e5
  title: Production reporter payload and verification boundary
- id: v221-tabs
  resource: ../../evidence/catalog.json#E-399acb0b492d
  title: Compact category and functional tab layout
- id: v220-ui
  resource: ../../evidence/catalog.json#E-fb80be60719c
  title: Concise four-page diagnostic UI and non-storm boundary
- id: v219-nonstorm
  resource: ../../evidence/catalog.json#E-dff9dfb77b79
  title: Non-storm diagnostic inventory and single-category UI
- id: v218-diagnostics
  resource: ../../evidence/catalog.json#E-1f5d41e630d6
  title: Four-section diagnostic menu and runtime boundary
- id: v217-menu-coexistence
  resource: ../../evidence/catalog.json#E-7474e7c94231
  title: Static-menu step with all diagnostics excluded
- id: v216-coexistence
  resource: ../../evidence/catalog.json#E-05a22d9b04f4
  title: Diagnostic payload retained but not autostarted
- id: v213-rejection
  resource: ../../evidence/catalog.json#E-f0e57293f8cd
  title: Rejected OnUpdate activation and current diagnostic boundary
- id: v213-v214-baseline
  resource: ../../evidence/catalog.json#E-701d45eee316
  title: Current v2.1.13 diagnostic inventory and activation boundary
- id: visual-only-v2112
  resource: ../../evidence/catalog.json#E-1b8d81c5411f
  title: Current visual-only storm candidate
- id: runtime-repair
  resource: ../../evidence/catalog.json#E-7d9efa87e5a8
  title: Sound-gate correction, latest-run logging and menu investigation limits
- id: traffic-removal-audit
  resource: ../../evidence/catalog.json#E-c2fd7e0a563f
  title: Current diagnostics and shipped v2.1.8 traffic-removal verification
- id: build-report
  resource: ../../evidence/catalog.json#E-69f4e9024e55
  title: v2.1.1 internal build report
- id: lifecycle-source
  resource: ../../evidence/catalog.json#E-4aa4ce23a7c8
  title: Diagnostic watcher lifecycle
- id: menu-source
  resource: ../../evidence/catalog.json#E-493fd5604c9a
  title: Diagnostic menu registration
- id: hdri-evidence
  resource: ../../evidence/catalog.json#E-ef87fe988bcd
  title: TFoWC2 HDRI selection and blend boundary
---

# Why controls alone did not identify the crash

The Addons experiments separated package presence, Lua autostart, static menu
registration and active native diagnostics. A dormant package preserved the
foreign Trainer menu and did not reproduce the reported crash. A later static
menu control worked, but restoring several native/Lua/UI changes together lost
the foreign menu again. That combined change could not isolate the cause.

A four-category layout later reproduced the missing Trainer Environment page
while retaining the earlier non-storm runtime. A single unique category with
supported tabs received a successful loading/menu/capture report. This supports
that tested arrangement; it does not prove a universal category-count limit or
that every earlier crash had the same cause.

Removing traffic control and reusing an existing OnUpdate watcher for Storm A
still reproduced a story-load Lua-table fault. The callback change was not a
causal proof. [The Lua attribution study](lua-frame-attribution.md) explains the
missing historical heap/frame evidence and the separately demonstrated target-VM
frame-size defect. Native lifecycle scheduling is documented in
[storm mechanics](basic-lightning.md).

# Ownership lesson

An extension owns its menu references, prefixed identifiers and watcher. Failure
cleanup must not erase another extension's registry entries or restore global
traffic state that it did not change. Package checks and Lua fixtures preserved
foreign sentinels, but live coexistence still required a runtime report. Finding
Trainer files on disk or seeing time commands register did not disprove a missing
menu observed in the game.

# One-shot world-light marker

A separate reporter armed one capture at the guarded Global projectile-trace
boundary and copied the next valid endpoint into a `WORLD_SHADOW_MARKER` record.
The Lua registration used one action without continuous polling or Script lifecycle
callbacks. Native tracing remained pass-through and failed closed on byte mismatch.
A trace endpoint is not automatically a surface hit or a unique light identity;
screenshots and world-resource mapping were independent evidence.

# Logs and deferred capture

The implementation truncated its own log once per process, then appended bounded
records. Menu reload did not truncate it. Failed initialization disabled logging
instead of appending into an older session. Version/PID markers distinguished a
new loader run from an older Addons log when the extension was disabled.

Atmosphere requests queued one bounded read at a subsequent sky callback.
`CAPTURE_COMPLETE` meant the request was processed, not that every record existed.
Bolt cancellation stopped future emissions; already emitted traces expired under
native lifetime. Neither a copied pointer nor a successful API return proved
safe cross-scene reuse. See [atmosphere mappings](atmosphere-probe.md),
[tracer experiments](manual-lightning-bolt.md), and
[extension authoring](../../compatibility/nexus-tools-extension-authoring.md).
