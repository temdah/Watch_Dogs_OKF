---
okf_version: '0.2'
---
# Watch Dogs engine and modding knowledge

Research for modders: how the engine works, how its data and interfaces behave,
what changes were tried, what failed, and what remains unknown. Most findings
concern Watch Dogs 1; Watch Dogs 2 comparisons are explicitly scoped.

Start with [engine fundamentals](projects/shadow-engine/research/engine-fundamentals.md),
then browse the [subject guide](topics/index.md):

- [Build identity and native patching](topics/index.md#build-identity-and-native-patching)
- [Shadow admission, resources and quality](topics/index.md#shadow-admission-resources-and-quality)
- [Vehicle identity and light ownership](topics/index.md#vehicle-identity-and-light-ownership)
- [World data, graphics and streaming](topics/index.md#world-data-graphics-and-streaming)
- [Weather, sky and audio](topics/index.md#weather-sky-and-audio)
- [Cloth, animation and movement](topics/index.md#cloth-animation-and-movement)
- [Lua and mod interfaces](topics/index.md#lua-and-mod-interfaces)
- [Measurement, failures and validation](topics/index.md#measurement-failures-and-validation)

Native engine mappings, mod-owned implementations, static inference, offline
checks and human runtime observations are different kinds of evidence. Each
concept should state its build/profile, source and limits; an address is not a
portable API. Failed controls are retained because they help avoid repeating
unsafe or ineffective approaches.

[Function maps](projects/index.md) and [shared compatibility findings](compatibility/index.md)
provide another route into the research.
Existing project-named paths record where findings originated; these are research
articles, not mod release manuals. See [evidence availability](evidence/index.md)
and [recent knowledge changes](log.md). Raw game binaries and private captures
are not distributed with this documentation.
