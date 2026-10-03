---
type: Diagnostic Contract
title: Headlight Shadow Resource Diagnostics
description: Bounded F10 correlation of native light candidates, requested shadow dimensions
  and shared-texture metadata.
tags:
- shadow-engine
- headlights
- resolution
- diagnostics
- ownership
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-077cac7a56c4
  title: Global87 whole-pass population binary
- resource: ../../../evidence/catalog.json#E-3724261dfc5f
  title: Global85 unmarked population tail, native boundaries and coverage/cost limits
- id: private-resource-transition43-runtime
  resource: ../../../evidence/catalog.json#E-06c95a21c55d
  title: Stationary4096 to512 to4096 Global transition result
- id: private-resource-transition43
  resource: ../../../evidence/catalog.json#E-e70c6531fe6e
  title: Capture-only resource transition candidate and validation
- id: private-provenance
  resource: vehicle-light-provenance.md
  title: Vehicle Light Component to Renderer Provenance
- id: private-runtime-evidence
  resource: ../../../evidence/catalog.json#E-69106f5168e9
  title: Seven Global F10 resource captures with state labels pending
- id: private-candidate-evidence
  resource: ../../../evidence/catalog.json#E-3e271e3703b6
  title: Candidate preflight, source freeze, validation and package
- id: private-native-renderer
  resource: ../../../evidence/catalog.json#E-08039110f66c
  title: Native renderer field and resource consumers
- id: private-native-builder
  resource: ../../../evidence/catalog.json#E-1001d162f65a
  title: Native candidate and dimension queue writers
- id: private-native-lookup
  resource: ../../../evidence/catalog.json#E-7d04e2d55f27
  title: Native shared-texture metadata assignment
- id: native-request-constructor
  resource: ../../../evidence/catalog.json#E-e78b15adf148
  title: Global shared-resource request pool and wrapper construction
- id: private-implementation
  resource: ../../../evidence/catalog.json#E-ad4735a0faf6
  title: Bounded candidate and renderer capture implementation
- id: private-proof
  resource: ../../../evidence/catalog.json#E-40884ac2c42b
  title: Independent regional field-consumer proof
- id: private-harness
  resource: ../../../evidence/catalog.json#E-f4a82f305d4e
  title: Actual-source synthetic safety tests
- id: private-classification
  resource: vehicle-light-classification.md
  title: Vehicle-Light Classification Boundary
- id: public-resource-transition
  resource: ../../../evidence/catalog.json#E-7df9454cca5a
  title: Capture-only before-resource copying and copied-value transition report
---

# Purpose and scope

v2.0.42 adds native-width/height copies before vehicle quality, followed by
submitted dimensions before the original renderer and resource metadata after
return. STAGE_SHADOW_LOD_RECORD joins existing serial/sample/entry identities;
policySampled distinguishes actual post-policy copies, resourceValid gates
metadata and requestResourceMismatch is a CPU comparison, not visual corruption.
distanceKnown=0 explicitly excludes guessed world coordinates/meters. Existing
request columns retain their post-policy meaning. Input values are those of the
currently modded engine before this policy, not proof of unmodified retail LOD.
The four-window bounded capture/token is reused; no new hook or persistent
tracking. Capture begins before quality, both locks are nonwaiting, and no
new file I/O occurs in renderer callbacks. Offline split-phase/order tests pass;
the .42/.43 runtime findings below and in [distance-quality research](distance-shadow-quality.md) remain limited to CPU evidence.

# Resource transition diagnostic (v2.0.43)

The manual four-window sample also copies candidate+58 backing and backing+40
resource before the native renderer. Existing renderer+2D2 instruction proof
covers both pointer loads; fresh independent validation passes on four mapped
profiles. A4EE remains unvalidated. Module 18 owns the capture ticket/storage;
the focused resolution diagnostic module owns the synchronous read and pure
copied-value report. It adds no hooks, engine writes, native calls or persistent
registry. Inactive captures and dropped queue entries do not perform this read.

STAGE_SHADOW_RESOURCE_TRANSITION joins serial/sample/entry and distinguishes
unavailable data, no backing, no resource, same address and different address.
Before dimensions can be compared with the submitted request, alongside 42's
request/output comparison. A same address is not allocation-generation proof;
neither comparison establishes GPU completion or safe automatic resizing.
Pre-native pointers are never followed after native return or by the worker.
Null/unreadable cases affect only the snapshot. The .43 diagnostic changed no world policy, vehicle quality/limiter, lifecycle or tools contract.
Offline safety gates pass. Global stationary runtime used 4096->512->4096. Both
exact vehicle-owned lights match requested/output CPU dimensions across every
window and retain respective output addresses across both transitions. Their
backing resources are null before every native call, so the renderer obtains
the shared resource during each call. This validates both tested CPU transition
directions for the current vehicle cap, not persistent GPU allocation identity.

# Confirmed native CPU boundary

The queue builder stores its admitted candidate at entry +0x10. The renderer
reads candidate +8 as descriptor and +0x10 as spatial data; descriptor +8 is
renderer type and +0x40 contains flags. Spatial +0 is an indexed-indirection
root consumed by the renderer, not a proven vehicle owner.

Queue-entry +0x20A4/+0x20A8 are requested width/height, following face count at
+0x20A0. The renderer passes those dimensions as shared-texture request words
0/1, then stores the returned native resource at entry +0x20B0. Request words
0/1 are copied into resource metadata +0x40/+0x44. Resource allocation/reuse and
release remain owned by the native engine; the diagnostic never acquires or
releases a resource.[^public-proof]

| Profile | Renderer RVA | Shared-texture lookup RVA |
| --- | --- | --- |
| Global | 0x00306E60 | 0x00430A80 |
| VMPless | 0x008BF250 | 0x00976800 |
| Complete | 0x01D06C40 | 0x01DBCE90 |
| Asia | 0x00940510 | 0x009A5CF0 |

These are statically recovered and byte-checked field consumers on four
preserved images, not fresh live classification or GPU proof. A4EE is
unvalidated. Five complete renderer instruction spans exclude unrelated
regional stack offsets; two exact shared-texture instruction variants cover
the observed layouts. At F10 arm, the extension validates those spans and the
renderer call target against the existing observer's verified target identity.
Failure disables the extension only; legacy F10 remains available.[^public-proof]

# Native backing and request-wrapper reuse

The following additional roles are static Global evidence. The regional
field-consumer checks above do not independently validate the complete helpers
or establish GPU allocation and lifetime behavior.

Renderer 0x00306E60 obtains a0x670-byte native backing structure when candidate+58
is null. If backing+40 is null, it calls shared lookup with the queued dimensions
and native map key, then stores the returned CPU resource in backing+40 and
queue+20B0. Existing backing+40 bypasses lookup even though request dimensions
still feed render parameters. Request capping alone therefore does not prove a
persistent backing resource resized.[^native-backing]

Shared lookup 0x00430A80 searches native request objects by key at+88. Its
matching-object reuse path requires +74=0, increments two native counters,
rewrites request/metadata fields including dimensions at+40/+44 and returns the
same wrapper. A matching object with nonzero+74 reaches a diagnostic trap in
the recovered body. The unmatched path calls 0x00426AF0, which obtains another
pool item or allocates and constructs a0xB0-byte request object when no spare
item exists, initializes metadata/counters and advances the active count.
The engine owns these objects and their consumers; the observer only copies
values during the synchronous native call.[^native-request-reuse][^native-request-constructor]

These are CPU wrapper allocation/reuse rules. Counter meanings, the complete
+74 ownership protocol, downstream GPU allocation/replacement and retirement
remain unproved here. Same-address wrappers with new dimensions are not GPU
generation proof. The .43 observations are consistent with request-wrapper reuse
but do not establish persistent GPU resizing. No pointer pinning, forced release,
null-to-refresh write or direct native allocator call follows from this evidence.
Manager-owned cached textures and their update scheduling are a separate
[pressure boundary](shadow-pressure.md).

# Capture ownership and bounds

Module 18 owns one process-lifetime copied buffer and state machine: idle,
initializing, capturing, frozen, worker flushing. One nonwaiting ownership
token excludes concurrent sample writers, timeout, rearm and premature flush.
Manager and renderer tickets borrow native pointers only for their synchronous
call. Contending diagnostics skip that opportunity; no engine thread waits
for the token, a shadow job or a GPU fence. The worker dereferences only copies.

Each stream targets samples at 0/500/1000/1500 ms after arming; delayed
opportunities can compress the actual gaps. Manager copies at most 256 candidates; renderer copies at most the
configured 31 queue records. The two streams are independently sampled; equal
sample indices are not a promise of the same frame. Renderer identity and
resource metadata are paired within one native call. Skipped trailing queue
records expose dimensions only, without chasing their candidate/resource
pointers. An idle renderer observer returns before any memory query.

Both streams finish before normal flush. After 2.5 seconds, timeout requests a
partial flush once no sampler owns the token; it never interrupts a native
call. Busy F10 presses are ignored. A failed worker creation discards only the
diagnostic buffer. Existing F7/F8/F9 and separate Addons traffic tools remain.
[^public-implementation][^public-harness]

# Reading the output

Original STAGE_VEHICLE_CAPTURE records remain. New
STAGE_VEHICLE_RESOLUTION records expose requestedWidth/Height, resourceWidth/
Height, candidate/descriptor/spatial/spatialRoot identities, type/flags, face
count, submitted status and derived prefix mapStart. Valid bits: 1 queue fields,
2 candidate readable, 4 spatial root readable, 8 resource metadata readable.
Type -1 means unavailable/unrecognized descriptor type; zero scalar values
alone are not a validity claim. A malformed face count clears validity.
complete describes queue-record copy completeness, not GPU rendering success.

These dimensions are native CPU request/resource metadata. They do not prove
the underlying ID3D11Texture2D allocation, GPU cost, visual quality, or that
per-vehicle resolution can be changed safely. Cached/reused metadata may differ
from the current request; preserve such differences as observations. Pointer
or tuple equality remains insufficient for persistent vehicle ownership.
[^public-classification]

# Global .85 population resource observation

The retained unmarked population tail contains5890 complete queue-row
observations with matching requested and returned CPU dimensions. All258 cached
update rows retain their before/after CPU resource address and512x512 dimensions.
This supplies no observed CPU resource mismatch or demonstrated allocation stall
in the retained approximately2.073 seconds. It does not establish GPU readiness,
allocation generation or resource behavior at the unmarked visual onset event.

# Global .87 whole-pass CPU resources

All27344 queued rows across1200 sampled renderer calls have complete copied
request and returned CPU dimensions, with zero mismatches. They split into
23786 requests at4096x4096,2358 at512x512 and1200 at8192x8192. No policy dimension
change occurs in these sampled calls at the chosen4096 settings; the8192 special
work remains outside the ordinary vehicle/world cap contract.

The sampled queue ranges13..25 entries and16..28 faces, with no admission/face
clamps. All1158 rows with readable pre-existing resource dimensions retain their
before/after address token and512x512 dimensions. Other before rows have either
no backing or no resource pointer, while their after-native CPU result is valid;
that alone is not an allocation failure.

Only26 distinct returned address tokens occur, and14 are observed with both512
and4096 metadata at different times. Address reuse therefore cannot identify a
stable GPU allocation or readiness. Same-bucket/full-handle cache comparisons
also do not establish a causal manager-to-queue pair. The capture shows no CPU
request/result mismatch to repair; GPU completion and exact visible onset remain
outside this observation contract.

# Global runtime observation

The first Global v2.0.16 run produced seven complete F10 captures, 28 samples
per stream and 117 fully readable renderer records without request/resource
CPU dimension mismatches. A repeated headlight-like type-3 pair requests
4096x4096 with matching metadata. Spatial roots remain consistent across
alternating descriptor/spatial copies; this is per-light correlation, not
vehicle ownership or generation proof. Other type-1 lights also use 4096.

The final window contains unadmitted headlight-like candidates, not evidence
of stale result rejection or proven siren eviction. Exact seven-state labeling
remains unknown after reported misclicks. Lifecycle summaries balance with zero reported
failures. GPU dimensions, safe selective resolution mutation and broad visual/
performance acceptance remain unproven.


The .43 transition test includes 24 exact target rows, all matching requested/output dimensions. The .16 recurring pair appears in captures 2/3/4/6; its two lamps have distinct spatial roots. Capture 7 still lists the familiar pair as admitted=0 while sampled renderer calls contain no type 3. Its lifecycle totals are 2,553 external results: 2,140 non-null releases plus 413 nulls, with zero reported lifecycle/completion failures. Exact seven-state labels remain unknown, so no six-state sequence or siren eviction is inferred.

The later component/transform diagnostic adds separate observers and identifies the observed tuple as direction, not world position; see [vehicle provenance](vehicle-light-provenance.md). Those additions do not change the historical no-new-detour scope of the original resource capture.

[^public-implementation]: Bounded candidate and renderer capture implementation
[^public-proof]: Independent regional field-consumer proof
[^public-harness]: Actual-source synthetic safety tests
[^public-classification]: Vehicle classification evidence and limits
[^native-backing]: Global renderer 0x00306E60, candidate+58 and backing+40 resource paths.
[^native-request-reuse]: Global shared lookup 0x00430A80, matching-key reuse and metadata writes.
[^native-request-constructor]: Global helper 0x00426AF0, request-pool item and wrapper construction.
