---
type: Loader Compatibility Contract
title: NexusTools Early Initialization
description: Loader callback contract required to patch Shadow Engine before dependent initialization.
tags:
- shadow-engine
- nexustools
- loader
- bootstrap
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-nexus113-compatibility-20261003
  title: Host identities, startup rejection and actual-module offline checks
- id: entry-module
  resource: ../../../evidence/catalog.json#E-fdebcf63c883
  title: Runtime entry and exported callbacks
- id: archived-contract
  resource: ../../../evidence/catalog.json#E-23bae041084b
  title: Pre-migration detailed NexusTools investigation
- resource: ../../../evidence/catalog.json#E-d7dd373e7ad2
  title: Runtime entry and exported callbacks
- resource: ../../../evidence/catalog.json#E-5a3420664ba5
  title: Preserved historical technical evidence
- resource: ../../../evidence/catalog.json#E-ba15b5d80461
  title: Preserved historical technical evidence
---

# Contract

Shadow Engine exports the NexusTools early callbacks implemented by the runtime
entry module. The early callback must run before dependent engine construction;
post-engine fallback is diagnostic, not equivalent activation.[^entry-module]

# Failure behavior

Missing or late activation must not be reported as an engine crash without
separate evidence. The patch records its lifecycle markers and performs no
partial profile installation when preflight is incomplete.

[^entry-module]: Runtime entry and exported callbacks

A missing, renamed or late callback can leave the ASI loaded but inactive. The
callback is synchronous; completing construction hooks before dependent engine
startup is part of its contract. Late constructor execution after early hooks
commit is handled separately by [startup supervision](../architecture/startup-supervision.md).

# Historical pre-RunGame loader experiment

The v0.1.1 timing experiment inspected a particular NexusTools loader chain, not a generic ASI loader contract. Its dinput8 proxy contained a hard-coded UTF-16 `TroploAsiInjectionHelper.asi` target. The helper exported `HookedGetProcAddress`, `HookedRunGame`, `HookedRunGameEx`, `HookedEntryPoint` and `InitializationThread`. Its GetProcAddress wrapper recognized decorated and undecorated `RunGame`/`RunGameEx` names and substituted wrappers that initialized `TroploNexusTools.ipe`, waited for Nexus readiness, then called the real Disrupt entry point.

The first appended process session ended before readiness. The second completed with no engine mutation: Disrupt was already mapped at bootstrap entry, interception was active at 2167.538 ms, `OriginalRunGame` was published at 2167.958 ms, and Nexus readiness occurred at 5709.278 ms. The observed interval from pointer publication to readiness was 3541.32 ms. This proved a pre-native-startup installation opportunity in that captured chain; it did not establish constructor-hook reachability, a minimum timing window in other sessions, or compatibility with other loaders.

The historical chain prototype interposed the helper's exported RunGame wrappers while retaining the original helper and Nexus binary. Its purpose was to arm constructor hooks before engine startup without calling engine resource builders from DllMain or a loader-notification callback. This prototype and its proposed replacement proxy are historical designs; the current early-callback contract above does not require installing that old loader chain.

# Historical proxy identity and successful early expansion

A later captured prototype retained a 46,592-byte proxy and changed its embedded UTF-16 helper filename at file offset `0x5D28`, from `TroploAsiInjectionHelper.asi` to `ShadowEnginePatch.asi`; 26 bytes differed. The patch then loaded the untouched helper. The reference original SHA256 was `D827076530406E467C593D23A6B84AC22883B853A579EA816BC10FCE1CDAA4EC`; the modified reference was `10110E4BD7A960C66B6CF55664BF9919126B096154FDCFC0D9322BEA565ED178`. Neither binary is redistributed here.

That early-window experiment reported construction of maps 16–23 and their paired passes 17–24, followed by several minutes of normal operation. It established the captured early-construction path, not complete lifecycle or regional safety. A generic ASI scan by that old proxy remained unproved. These historical modified-loader details are not current installation instructions.

# Host update case study: 1.1.12 to 1.1.13

The .87 log rejected `hostOrStartupWindow`, then `earlyInstallationFailed` with
zero installed hooks. An optional Global Lua repair pinned the old NexusTools
image size and guard addresses; its rejection aborted the shadow installation.
The game shadow executable profile had already matched.

Read-only PE inspection identified these builds; neither image was executed:

| Host build | Timestamp / image size | CustomLuaManager initializer | Instance guard | LEA/call site |
| --- | --- | --- | --- | --- |
| 1.1.12-6924c27 | `6A82F9AC` / `EBB000` | `A0E00` | `C62AE0` | `1B6B31` |
| 1.1.13-ad643fa | `6AB6AD4E` / `ED6000` | `B4350` | `C7C0C0` | `1ADF91` |

The old file SHA256 is `8120389BA4D144DC465E9FED2648B5690A6BBF0CDF5B052EF6EE3B738BE5DCFC`;
the new file SHA256 is `03875BACFAD447397305B9D5F19BCB07DC4473B99F7D1354604B4A2BB1DFE727`.
Embedded build strings identify the versions. The initializer checks/sets the
instance's first byte before logging `Initializing CustomLuaManager...`. The
caller's RIP-relative LEA supplies that static instance. Code and data moved by
different deltas; translating every RVA by one offset is invalid.

# Optional repair and independent shadow checks

The .88 candidate explicitly maps both hosts. It checks x64 PE identity, the
27-byte initializer prologue, the following 12 guard bytes and the caller's
12-byte LEA/call before reading the mapped guard. Helper interception, original
RunGame and not-ready state remain required. NexusTools itself is never patched.

All 17 game Lua sites must match before selecting the optional repair. The
complete set and startup window are rechecked immediately before writes, which
remain in the early transaction. A write failure rolls that transaction back;
a partially installed format is never accepted.

An unknown host, unavailable/late guard or changed Lua sites leaves the optional
repair inactive. Shadows continue through their own game identity, instruction,
constructor-timing and transaction checks. Inactive Lua repair is not proof the
unpatched defect is harmless. Required shadow checks can still reject startup;
this does not guarantee compatibility with all future loaders.

SE10 tools and the log warn on fallback, with a session-scoped notification and
persistent Shadows-page text. They identify 1.1.12 as the last runtime-tested
baseline and recommend that complete version if issues occur. The explicitly
mapped 1.1.13 candidate uses the normal repair path.

# Validation boundary

The actual module passed 1,788 offline checks against both original PE fixtures
mapped as data: 17-site activation, failure at every write and rollback, every
changed game site, unknown identity, changed caller/guard, missing helper exports,
and loss of the startup window between selection and commit. Native settings,
startup and transaction tests and desktop Lua warning/control checks passed.
Internal and Release builds reproduce; Release still excludes the Lua experiment.

The .88 candidate has no in-game acceptance yet. Mapping 1.1.13 does not prove
safe synchronous Lua format transition, all host APIs/scripts, or future builds.
The remaining lifecycle limits belong to [the frame investigation](../architecture/lua-stack-compatibility.md).
