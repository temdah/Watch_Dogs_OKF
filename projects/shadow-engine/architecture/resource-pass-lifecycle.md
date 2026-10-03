---
type: Engine Lifecycle Contract
title: Shadow Resource and Pass Lifecycle
description: Safe construction, storage, registration, finalization, and routing rules for expanded
  maps and render passes.
tags:
- shadow-engine
- resources
- passes
- constructor
- lifecycle
status: draft
sources:
- id: expansion
  resource: ../../../evidence/catalog.json#E-f45567a3ad24
  title: Engine expansion implementation
- id: bootstrap
  resource: ../../../evidence/catalog.json#E-1576d48ce50e
  title: Early and deferred orchestration
- id: historical-bootstrap
  resource: ../../../evidence/catalog.json#E-5a3420664ba5
  title: Historical public early-bootstrap investigation
- id: historical-regressions
  resource: https://github.com/temdah/Shadow-Engine/blob/2082a3bec1bfc4213ae4572b0e14b4f20c17906b/docs/okf/experiments-and-regressions.md
  title: Historical public regression ledger
- id: archived-bootstrap
  resource: ../../../evidence/catalog.json#E-de50058a67f5
  title: Historical early-bootstrap investigation
- resource: ../../../evidence/catalog.json#E-d9694ed25b9c
  title: Engine expansion implementation
- resource: ../../../evidence/catalog.json#E-32761c3b66e0
  title: Early and deferred orchestration
- resource: ../../../evidence/catalog.json#E-c38ab69eeed1
  title: Preserved historical technical evidence
---

# Construction window

Extra shadow maps must be created by extending the native resource-constructor
loop while its engine-owned dependencies are valid. Native indices 0-15 keep
their manager storage. Indices 16 and later are redirected to patch-owned
handle and aligned 16-byte companion arrays because continuing through the
native manager tail would overlap unrelated fields.[^expansion]

Late calls to the resource builder are unsafe. Historical staged tests crashed
on the first late `ShadowMap16` construction even when invoked from a renderer
thread.[^historical-bootstrap] The accepted implementation installs the constructor hooks during the
early NexusTools callback and performs downstream routing only after the early
resource and pass invariants are proven.[^current-status][^bootstrap]

# Pass registration and finalization

Pass registration is also an object factory: it constructs a pass and inserts
it into the renderer's two-level table. Added passes must be registered inside
the native registration phase, immediately after native pass 16 and before
table finalization. Registering after finalization can return without making
the objects visible to the renderer.[^expansion][^current-status]

For each added local map `m`, register pass `p = m + 1`:

* `Shadow` key = `(p << 9) | 0x0C`;
* `ShadowAlpha` key = `(p << 9) | 0x10C`.

Before registration, validate the physical table, stored maximum key, every
assigned name, and the entire required range. After registration, require every
added slot to be non-null and mutually distinct. Failure blocks downstream
installation; the patch must not partially expose new demand.

# Activation proof

Allocation is not proof of capacity. A candidate must separately prove:

1. all external handles are non-zero and distinct from native and one another;
2. all paired pass slots are non-zero and distinct;
3. downstream routing was installed only after those checks;
4. added map, face, pass, and result indices are actually consumed;
5. teardown/release counters remain coherent.

[^expansion]: Engine expansion implementation
[^bootstrap]: Early and deferred orchestration
[^current-status]: Accepted resource and pass behavior
[^historical-bootstrap]: Historical public early-bootstrap investigation
[^historical-regressions]: Historical public regression ledger

# Historical distinction between pass insertion and resource construction

Historical WD1 experiments isolated two different operations. The v1.2.9 report observed 17 admitted records with B4=8 and a null renderer initializer fault at reported RVA `0x408A4F`. Investigation identified `ff5130`/`ff5150` as two-level table lookups, not allocators: the key's low byte selected the bucket and its remaining upper bits selected the entry. A later capture identified missing key `0x220C` as pass 17, with lookup/reset sites reported at RVAs `0x307405`/`0x307410`. These are addresses from the cited historical capture, not automatically valid mappings for every current runtime profile.

The pass-registration routine was also an object factory: it allocated `0x1B0` bytes, constructed a pass object and inserted it into the two-level registry. The v1.2.12 constructor-injection count was zero because the ASI loaded after that phase. A later isolated late insertion created both pass-17 objects and they remained live until demand reached absent pass 18. The subsequent complete pass-range repair exceeded 71,900 manager calls in v1.2.16. Thus historical live factory insertion could work; the production requirement to install during native registration should not be read as proof that every late pass-object insertion is impossible.

Resource construction had a different result. The v1.2.13 combined late resource/pass repair crashed in MSVCR100.dll before its initialization result. Executing on the renderer thread did not establish valid constructor-era dependencies. Successful pass insertion therefore does not justify late resource creation or a current late-load recovery path.
