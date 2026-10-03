---
type: Architecture Reference
title: Shadow Engine Pipeline
description: End-to-end ownership map from light candidates through manager residency, renderer
  dispatch, result consumption, and release.
tags:
- shadow-engine
- pipeline
- admission
- rendering
- lifecycle
status: draft
sources:
- id: manager-module
  resource: ../../../evidence/catalog.json#E-6658abb69696
  title: Manager admission and owner-vector module
- id: renderer-module
  resource: ../../../evidence/catalog.json#E-9a4ab6c06cd6
  title: Renderer queue and face-admission module
- id: expansion-module
  resource: ../../../evidence/catalog.json#E-f45567a3ad24
  title: Map, pass, queue, and scheduler expansion module
- id: result-module
  resource: ../../../evidence/catalog.json#E-6c0b42188e37
  title: External slice-result lifecycle module
- resource: ../../../evidence/catalog.json#E-77e04602a192
  title: Manager admission and owner-vector module
- resource: ../../../evidence/catalog.json#E-8ba8bf022b48
  title: Renderer queue and face-admission module
- resource: ../../../evidence/catalog.json#E-d9694ed25b9c
  title: Map, pass, queue, and scheduler expansion module
- resource: ../../../evidence/catalog.json#E-2b606cbf5e75
  title: External slice-result lifecycle module
---

# Processing stages

```text
world and vehicle lights
  -> candidate construction and classification
  -> manager admission and priority
  -> fully dynamic or cached-owner residency
  -> render-queue records and cumulative face allocation
  -> local-map handle and Shadow/ShadowAlpha pass lookup
  -> SliceExecute dispatch and result store
  -> stock post-call consumer
  -> external-result consumer and native-wrapper release
```

Each arrow crosses a distinct capacity or lifetime boundary. Increasing one
number cannot prove that later allocations, writers, readers, indexing, and
release paths can consume the added work.[^manager-module][^expansion-module]

# Policy boundaries

`B4` controls the manager's fully dynamic lane; with caching enabled, ordinary
dynamic positions are approximately `B4 - 1`. `A8` bounds cached owners. Those
owners rotate through a shared low-resolution refresh lane and are not extra
high-resolution maps. The renderer then counts cumulative faces, so one queue
record may consume more than one local map.[^manager-module][^renderer-module]

Vehicle headlights and world spotlights converge before the generic renderer
path. Renderer type 3 is therefore not a safe vehicle identity. Current finite selection filters only exact recent generation-safe vehicle
groups before admission; world, unknown and ambiguous candidates retain native
passthrough. See [vehicle selection](vehicle-shadow-selection.md).

# Failure localization

When rendering regresses, compare the first stage that differs from a known
good run:

1. profile selection and complete preflight;
2. native and external resource handles;
3. pass-table population;
4. manager candidates, admissions, `B4`, `A8`, and cached bindings;
5. queue records and cumulative faces;
6. native and external `SliceExecute` stores;
7. external consumption, release, stale-lineage, and late-write counters.

A populated queue with zero result stores localizes failure before or at job
dispatch. Balanced accepted stores and releases with visual loss points back
toward admission/residency or sampling rather than result lifetime.[^result-module]

[^manager-module]: Manager admission and owner-vector module
[^renderer-module]: Renderer queue and face-admission module
[^expansion-module]: Map, pass, queue, and scheduler expansion module
[^result-module]: External slice-result lifecycle module
