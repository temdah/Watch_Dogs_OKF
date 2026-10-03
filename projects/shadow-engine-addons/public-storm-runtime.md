---
type: Runtime Architecture
title: Separating a storm hook host from optional observers
tags:
- shadow-engine-addons
- lightning
- thunder
- public
- ownership
status: stable
sources:
- id: promotion
  resource: ../../evidence/catalog.json#E-29487a51e173
  title: reported acceptance, release scope, package comparisons and offline tests
- id: preflight
  resource: ../../evidence/catalog.json#E-972fa106ab4e
  title: Knowledge lookup, historical envelope and acceptance boundaries
- id: host
  resource: ../../evidence/catalog.json#E-0da6815d7a1f
  title: Production-only native sky host
- id: core
  resource: ../../evidence/catalog.json#E-c8d4e97556fd
  title: Shared scheduler and sky publication
- id: allowlist
  resource: ../../evidence/catalog.json#E-49da5047739d
  title: Exact public native compilation units
- id: loading
  resource: storm-audio-loading.md
  title: Retail Storm Audio Dependency Loading
---

# Native boundaries and build identity

The inspected Watch Dogs 1 Global image is AMD64, timestamp `5CD045B4`, image
size `6595000`, captured SHA256
`D8004145FB17BD6A9073466EBB9BFC19589AAD7D08D8EC3FD45733A5D8AD0855`.
The following is a mod implementation over these mapped native boundaries:

| Boundary | Role |
| --- | --- |
| `A53860`, 19 displaced bytes | Sky orchestrator; forwards the original trampoline, Environment, delta and blend. |
| `A2F7E0` / `A24DE0` | Native update runs first; a private Storm A scheduler follows using owned output. |
| `A15180` | Contribution before sky publication; selected Moon record/state remain intact. |
| `275DC0`, Environment+8 | Retail resource-add path for strike `1B2CB` and thunder `1B2CA`; the native container owns references and release. |

# Host and observer ownership

One shared storm implementation served a minimal host and a diagnostic host.
The latter injected copied observer callbacks; the former supplied no observers.
Observers borrowed serialized state and did not own pulse allocations or change
playback policy. Only one host owned the sky detour. The initializer ran outside
DllMain, with the ASI pinned and published trampolines retained for in-flight calls.

Image/core/sky signatures were checked before writes. Installation prepared both
hooks and rolled back owned writes on allocation/protection failure. This is not
thread-suspended atomic patching, nor proof of compatibility with another hook at
the same site. Unsupported images remained inactive.

# Experiment and checks

The diagnostic implementation received a reported Global result with audible
thunder, flashes and preserved moon shadows in version 2.1.27. Extracting the same
mechanism into a smaller host had separate offline evidence, not a fresh game
acceptance report. Native fixtures compared observed/unobserved scheduling,
original arguments and order, delayed sound, first-entry acquisition, weather/
pause/scene guards, Moon sentinels and rollback. Explicit source/include and PE
checks verified that excluded diagnostics were absent rather than merely hidden.

The reusable result is separation of hook ownership, mechanism and observation.
See [storm scheduling](basic-lightning.md) and
[native sound-resource loading](storm-audio-loading.md) for the recovered engine
behavior. This host experiment establishes no sun alignment or custom-bolt rendering.
