# Research by subject

Begin with [engine fundamentals](../projects/shadow-engine/research/engine-fundamentals.md).
[Open technical questions](../projects/shadow-engine/research/engine-opportunity-map.md)
identify gaps in the evidence, not an implementation queue.

## Build identity and native patching

- [Delayed Shadow Initialization](../projects/shadow-engine/architecture/startup-supervision.md)
- [Native patch architecture: ownership and binary-equivalence experiments](../projects/shadow-engine/architecture/runtime-architecture.md)
- [NexusTools Early Initialization](../projects/shadow-engine/compatibility/nexustools-init.md)
- [Patch Transaction Model](../projects/shadow-engine/architecture/patch-transactions.md)
- [Reproducible Watch Dogs archive construction and runtime isolation](../projects/shadow-engine-addons/build-profiles.md)
- [Runtime Profile Architecture](../projects/shadow-engine/architecture/runtime-profiles.md)
- [Shadow Resource and Pass Lifecycle](../projects/shadow-engine/architecture/resource-pass-lifecycle.md)

## Shadow admission, resources and quality

- [Case study: leaked acquisitions in expanded shadow results](../projects/shadow-engine/releases/v2.0.15.md)
- [Distance Shadow Quality Controls](../projects/shadow-engine/architecture/distance-shadow-quality.md)
- [External Slice Results](../projects/shadow-engine/architecture/external-slice-results.md)
- [Headlight Shadow Resource Diagnostics](../projects/shadow-engine/architecture/headlight-resource-diagnostics.md)
- [Incoming Vehicle Shadow Readiness](../projects/shadow-engine/architecture/incoming-vehicle-readiness.md)
- [Shadow Capacity Layout](../projects/shadow-engine/architecture/engine-capacity-layout.md)
- [Shadow Engine Pipeline](../projects/shadow-engine/architecture/shadow-pipeline.md)
- [Shadow Population Boundary Observation](../projects/shadow-engine/architecture/population-observation.md)
- [Shadow Pressure Boundaries](../projects/shadow-engine/architecture/shadow-pressure.md)
- [Vehicle Shadow Quality Boundary](../projects/shadow-engine/architecture/vehicle-shadow-quality.md)
- [Vehicle Shadow Selection Diagnostic](../projects/shadow-engine/architecture/vehicle-shadow-selection.md)
- [Watch Dogs 2 Shadow Architecture Reference](../projects/shadow-engine/compatibility/wd2-reference.md)
- [WD1 Shadow Eligibility and Work Boundary](../projects/shadow-engine/architecture/wd1-shadow-eligibility.md)
- [WD2 Headlight Owner Selection and Publication](../projects/shadow-engine/architecture/wd2-headlight-selection.md)
- [WD2 Local Shadow Admission and Fade Consumption](../projects/shadow-engine/architecture/wd2-local-shadow-pipeline.md)
- [WD2 Shadow Reference and WD1 Port Boundaries](../projects/shadow-engine/architecture/wd2-shadow-reference.md)
- [World Quality Validation Overhead](../projects/shadow-engine/architecture/world-quality-validation.md)

## Vehicle identity and light ownership

- [Current Driver Vehicle Identity](../projects/shadow-engine/architecture/driver-vehicle-identity.md)
- [Tracked Vehicle Retirement Diagnostics](../projects/shadow-engine/architecture/vehicle-retirement-diagnostics.md)
- [Vehicle Light Component to Renderer Provenance](../projects/shadow-engine/architecture/vehicle-light-provenance.md)
- [Vehicle Light Owner and Skeleton Lifetime](../projects/shadow-engine/architecture/vehicle-owner-lifetime.md)
- [Vehicle Specular Light Reference Integrity](../projects/shadow-engine-addons/vehicle-light-reference-integrity.md)
- [Vehicle-Light Classification Boundary](../projects/shadow-engine/architecture/vehicle-light-classification.md)

## World data, graphics and streaming

- [Additional Non-Batched Game Light Sources](../projects/shadow-engine-addons/additional-light-sources.md)
- [Authoring XBG lightning assets: formats, resource joins and spawn failures](../projects/shadow-engine-addons/custom-lightning-asset.md)
- [Compiled World-Light Shadows and Decoded Locations](../projects/shadow-engine-addons/world-light-shadow-batches.md)
- [Entity transforms, graphics activation and loading categories](../projects/shadow-engine-addons/graphics-activation-and-streaming.md)
- [Muzzle-Flash Dynamic Shadows](../projects/shadow-engine-addons/muzzle-flash-shadows.md)
- [Pequino Secondary Streetlamp Shadow Exclusions](../projects/shadow-engine-addons/secondary-streetlamp-shadows.md)
- [Perspective Local-Light PCSS](../projects/shadow-engine-addons/local-light-pcss.md)
- [TFoWC2 PCSS Delivery and Coverage Limits](../projects/shadow-engine-addons/tfowc2-shadow-filtering.md)
- [World Batch Loader Timing Probe](../projects/shadow-engine-addons/world-loader-probe.md)
- [World Entity Lights and Mission Activation](../projects/shadow-engine-addons/world-entity-script-lights.md)

## Weather, sky and audio

- [Basic Storm Lightning and Moon-Shadow Separation](../projects/shadow-engine-addons/basic-lightning.md)
- [Bounded Atmosphere Snapshot Probe](../projects/shadow-engine-addons/atmosphere-probe.md)
- [HDRI sun and native flare: selection mappings and unresolved projection](../projects/shadow-engine-addons/sun-flare-alignment.md)
- [Internal Recorded Lightning Bolt](../projects/shadow-engine-addons/manual-lightning-bolt.md)
- [Retail Storm Audio Dependency Loading](../projects/shadow-engine-addons/storm-audio-loading.md)
- [Separating a storm hook host from optional observers](../projects/shadow-engine-addons/public-storm-runtime.md)
- [Storm Sound Command Execution and Resource Resolution](../projects/shadow-engine-addons/storm-sound-execution.md)
- [Storm Thunder Audio Submission](../projects/shadow-engine-addons/storm-thunder-audio.md)

## Cloth, animation and movement

- [Watch Dogs 1 High-FPS Coat Physics Investigation](../projects/shadow-engine/research/cloth-high-fps-investigation.md)
- [Watch Dogs 1 High-FPS Player Movement Investigation](../projects/shadow-engine/research/player-movement-high-fps-investigation.md)
- [WD_DTCLAMP versus the coat fixed-step experiment](../projects/shadow-engine/research/wd-dtclamp-comparison.md)

## Lua and mod interfaces

- [Addons Lua Frame Defect Attribution](../projects/shadow-engine-addons/lua-frame-attribution.md)
- [Asynchronous native control ABI: request, receipt and application](../projects/shadow-engine/architecture/control-api.md)
- [Internal Lua Frame Repair Candidate](../projects/shadow-engine/compatibility/lua-frame-repair.md)
- [Lua Frame Compatibility Fix Design](../projects/shadow-engine/architecture/lua-frame-fix-design.md)
- [Lua-to-native bridges and shared-control ownership experiments](../projects/shadow-engine/architecture/internal-tools.md)
- [Nexus Tools Extension Authoring](../compatibility/nexus-tools-extension-authoring.md)
- [NexusTools menu coexistence and diagnostic attribution experiments](../projects/shadow-engine-addons/diagnostic-tools.md)
- [Persisting mod policy without blocking native callbacks](../projects/shadow-engine/architecture/saved-settings.md)
- [Shadow Engine Menu Host Compatibility](../projects/shadow-engine/architecture/menu-host-compatibility.md)
- [Vehicle Headlight Shadow Limiter NexusTools Control](../projects/shadow-engine-addons/headlight-limiter-control.md)
- [WD1 Lua Packed Frame Size and Garbage Collection](../projects/shadow-engine/architecture/lua-stack-compatibility.md)

## Measurement, failures and validation

- [Binary equivalence as a control for native-patch refactoring](../projects/shadow-engine/validation/historical-refactor-results.md)
- [Black Shadow Flicker Attribution](../projects/shadow-engine/architecture/black-flicker-diagnostics.md)
- [Bounded Intersection Provenance](../projects/shadow-engine/architecture/intersection-diagnostics.md)
- [Bounded Shadow Workload and Presentation Capture](../projects/shadow-engine/architecture/workload-capture.md)
- [Completion Diagnostic History Lookup](../projects/shadow-engine/architecture/completion-diagnostic-overhead.md)
- [Explicit Detailed Observation Windows](../projects/shadow-engine/architecture/detail-window-observation.md)
- [Known Failure Boundaries](../projects/shadow-engine/validation/known-failure-boundaries.md)
- [Measuring native patch overhead without confusing it with frame cost](../projects/shadow-engine/architecture/mod-performance-audit.md)
- [Offline Refactor Gates](../projects/shadow-engine/validation/offline-gates.md)
- [Regional Runtime Corpus Gate](../projects/shadow-engine/validation/runtime-corpus-gate.md)
- [Regional Runtime Matrix](../projects/shadow-engine/validation/regional-runtime-matrix.md)
- [Renderer Queue Validation and Overhead](../projects/shadow-engine/architecture/renderer-queue-validation.md)
- [Semantic validation of lighting references and compiled assets](../projects/shadow-engine-addons/established-feature-tests.md)
- [Vehicle Cost and Movement Observation](../projects/shadow-engine/architecture/vehicle-performance-diagnostics.md)
- [Whole-Mod Overhead Measurement](../projects/shadow-engine/architecture/overhead-measurement.md)
- [Worker-Owned Periodic Summary Output](../projects/shadow-engine/architecture/periodic-summary-transport.md)
