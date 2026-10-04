---
type: Architecture Reference
title: WD1 Shadow Eligibility and Work Boundary
description: Global static admission predicates, the shadow work they prevent, and unresolved
  ownership gates for earlier filtering.
tags:
- shadow-engine
- wd1
- admission
- ownership
- performance
status: draft
sources:
- id: lighting-consumer
  resource: ../../../evidence/catalog.json#E-wd1-lightdata-20261004
  title: Global LightShadowFactor registration, candidate consumer and command publication
- id: background-query-review
  resource: ../../../evidence/catalog.json#E-19eafa0c5c81
  title: Occlusion-query mapping and bounded background-quality experiment
- id: producer-review
  resource: ../../../evidence/catalog.json#E-7cc7a309ee67
  title: Global candidate producer, distance and query writers, and paired .87 observations
- resource: ../../../evidence/catalog.json#E-ee70408dc3e7
  title: Historical frame-builder export; candidate-holder attribution superseded
- resource: ../../../evidence/catalog.json#E-077cac7a56c4
  title: Global87 whole-pass population binary
- resource: ../../../evidence/catalog.json#E-3724261dfc5f
  title: Global85 unmarked population tail, native boundaries and coverage/cost limits
- id: manager
  resource: ../../../evidence/catalog.json#E-bc0e0b354e98
  title: Global rebuilt manager identity and native admission body
- id: admission-instructions
  resource: ../../../evidence/catalog.json#E-151ce662055b
  title: Global native eligibility instructions through the ordinary budget comparison
- id: admission82
  resource: ../../../evidence/catalog.json#E-7672703021a6
  title: Global82 complete candidate samples and protected-owner admission omissions
- id: queue-builder
  resource: ../../../evidence/catalog.json#E-1001d162f65a
  title: Admission caller and shadow queue entry construction
- id: visibility
  resource: ../../../evidence/catalog.json#E-2e632041f9d9
  title: Candidate-list holder supplied to shadow preparation
- id: setup-consumer
  resource: ../../../evidence/catalog.json#E-52c2765db7c9
  title: Additional descriptor shadow-enable consumer at Global 002C1220
- id: metadata
  resource: ../../../evidence/catalog.json#E-508e27c534c8
  title: Native light property registration
- id: physical-setters
  resource: ../../../evidence/catalog.json#E-55510fc4cb3a
  title: Physical light enable setters
- id: resolver
  resource: ../../../evidence/catalog.json#E-2ad94f5f962a
  title: Mutating spatial resolution and copy publication
- id: manager-hook
  resource: ../../../evidence/catalog.json#E-6658abb69696
  title: Synchronous candidate filtering and restoration
- id: candidate-observer
  resource: ../../../evidence/catalog.json#E-ad4735a0faf6
  title: Current copied candidate fields and post-native binding observation
- id: population-profile
  resource: ../../../evidence/catalog.json#E-251cc00fccb7
  title: Optional Global field proof and pure copied-input eligibility evaluator
- id: review
  resource: ../../../evidence/catalog.json#E-6619b163f9ff
  title: Read-only knowledge preflight and bounded result
---

# Scope and evidence

These are static mappings for the preserved Global
`Disrupt_b64_runtime_rebuilt.dll`, image base `0x7FFC39BF0000`.
All addresses below are RVAs in that image. Other profiles require independent
mapping and byte validation. Static mappings establish no safe writable API.
The .82 observations below are sampled input/output evidence, not a native branch
trace. The synchronous manager-list boundary remains in place through .83;
selection does not override the native eligibility predicates.[^manager][^manager-hook]

# Admission and prevented work

Let `C` be a linked candidate, `L = *(C+8)` its light descriptor, and
`S = *(C+10)` its spatial pointer; offsets are hexadecimal.

* For finite inputs, `002E9B60` reads `L+0D != 0`, `L+34 >= native epsilon`, and
 `C+68 >= native epsilon` before additional type, configuration, coverage and
 budget tests. The epsilon at RVA `02E70B94` has binary32 bits `3A83126F`,
 approximately **0.001** (`0.0010000000474974513` exactly as binary32). Output
 bindings have stride `18`: candidate at `+0`, optional manager cache owner at
 `+8`, and update-selection byte at `+10`.[^manager][^population-profile]
* `003C6CE0` passes the list holder from render-record `+40` to `0030A570`.
 That caller supplies its list head/count to the manager at `0030AAE7`.
 [^visibility][^queue-builder]
* `0030A570` constructs shadow work only for admitted bindings that need an
 update. A cache owner with its valid flag set provides `C+58 = owner+90`;
 a binding not selected for update skips queue construction. The work path
 creates `24C0`-byte entries, writing candidate at entry `+10` and face count
 at `+20A0`, then preparing native shadow cameras/caster work.[^queue-builder]

These bodies prove an admission-to-work boundary, not its measured cost. The
existing limiter already filters the input list before this native work and
restores borrowed links immediately after the synchronous manager returns.
Moving identity preparation earlier does not by itself prevent additional
renderer submissions. The downstream queue/face producer is owned by the
[external result lifecycle](external-slice-results.md).

# Candidate-list publication boundary

**Correction:** the earlier attribution of `003DC780` virtual slot `+20` to
candidate production was invalid. Exact call/store bytes proved instructions,
not object identity. In the concrete renderer family constructed at `004076A0`,
vtable `02EAEDC0` slot `+20` points to `00434470`, which selects/creates depth
textures, names resources `DepthTextureSS`/`DepthTextureMSAA`, and returns
resource `+38`. Its destination `+40/+48` fields must not be conflated with the
candidate holder merely because the offsets match. A live receiver was not
captured; this is a static type-family mapping.[^producer-review]

The actual candidate-holder allocation is in `003CA2E0`: a `A0`-byte object
has head `+0 = 0`, tail `+8 = self`, count `+10 = 0`, and `+18 = 0`, then is
stored at `(*argument2)+40`. It is passed to `002DFF40` and to the dependent
extents-results job scheduled by `002D66D0`. The subsequent
`PrepareShadowVisibility` callback `003C6CE0` supplies that same record field
to `0030A570`. The latter's manager call consumes head/count. These are frame/job
borrowed records, not persistent mod-owned storage.[^producer-review]

# Candidate construction, order and distance factor

The pre-shadow call at `003CA725` sets argument5 to one. On this path,
`002DFF40` retains a single worker job (the alternate path obtains a worker
count) and schedules `0048D7E0`. That worker constructs 16-byte sort records:
signed descriptor `L+48`, squared positional distance, and the light pointer.
Type0 uses the special key `INT_MIN` and zero distance. Sort `0048FB10`, with
comparison paths in `0048DE60` and `0048E650`, orders ascending signed key,
then ascending finite distance. Equal-key stability is not established. This
is already priority-then-distance ordering, not arbitrary arrival order or a
complete-vehicle grouping policy.[^producer-review]

The worker calls `0048CE20` in that order. It allocates/copies a `90`-byte
candidate, publishes descriptor/spatial pointers, links it to the list, and
atomically increments its count. Candidate addresses are therefore unsuitable
as durable vehicle identity across frames. Descriptor registration's property
`selPriority` at relative `+40` is consistent with descriptor `+48`; its writer,
sharing and safe mutation contract remain unproved.[^producer-review][^metadata]

`0048CE20` also initializes `C+68` to `1.0` at `0048D491`. For enabled ordinary
shadow lights, excluding types0/2 and flags `0x84000000`, it applies an optional
category factor and a positional-distance factor. For finite descriptor `L+50`
fade width above native epsilon (approximately0.001, constant RVA `02E565E4`),
the latter is `clamp((L+4C - distance) / L+50, 0, 1)`; for fade width at or below
epsilon it becomes zero beyond `L+4C`. Positions are read from
the light and current view/job context. This maps a native distance-fade
producer; it does not prove units in meters, permission to change descriptor
data, temporal blending, or that a particular visible pop-in was distance-caused.
The manager subsequently checks this factor against its epsilon.[^producer-review]

# Lighting consumption of the distance factor

For the same Global rebuilt image (SHA256
`d8004145fb17bd6a9073466ebb9bfc19589aad7d08d8ec3fd45733a5d8ad0855`),
`003A2520` registers `LightData` and its `LightShadowFactor` field. The latter's
header is at block `+150`, payload at `+160`, with registered type `104`.
`LightShadowTexture` uses payload `+198`. These names come from native
registration, independently of the successor game's layout.[^lighting-consumer]

`0031A8C0` populates that block from a candidate, spatial data and descriptor.
It reads `C+58` at `0031AA2B`; a null backing skips the shadow texture/factor
branch. Otherwise the texture is the optional sixth argument, or `backing+40`,
stored at block `+198`. There is **no non-null texture or GPU-completion test**
at that assignment. A backing pointer alone must not become a new readiness
claim.[^lighting-consumer]

For type1 and other nonzero types including type3, the helper copies `C+68`
into block `+160` and computes `1 - C+68` into `+164`. The type1 sites are
`0031ADBF/0031ADC9` and `0031ADF1/0031ADF6`; the other-type sites are
`0031AED9/0031AEE3` and `0031AF0B/0031AF10`. Native dirty-bit handling precedes
these writes. Type0 has a separate descriptor-derived branch. This establishes
the WD1 CPU factor/complement consumer; it does not establish the shader's
complete blending equation, temporal fading or visible correctness.
[^lighting-consumer]

Lifetime matters: `0031B3B0` returns an existing candidate `+80` block when
present. Otherwise it allocates/copies a `560`-byte template, invokes the
population helper, and atomically publishes to argument3 `+80`. That argument
must not be assumed identical to argument1 without its caller's proof.
Separately, local-light job `00490AD0` allocates a fresh block, calls the helper
at `00490E3A`, and passes the result to `00490A00` at `00490F3B`. The latter
appends the block pointer to a native command record. The helper is not proof
that every later consumption refreshes an already-published block. Retaining
these borrowed pointers or rewriting published data from another callback
requires an additional ownership/lifetime contract.[^lighting-consumer]

Two consequences constrain range extension and onset masking:

- `C+68` combines category and distance factors. Once zero, its value does not
  reveal which factor disabled the shadow. Replacing zero at manager admission
  can undo a non-distance gate; changing only texture request size changes
  neither factor. A distance-only extension must preserve the independent
  category, enable, coverage and capacity rules, including any earlier culling.
- A temporal multiplier applied before admission can itself fall below the
  manager epsilon and prevent allocation. A lighting-side multiplier avoids
  that specific dependency, but needs stable identity, a defined onset clock,
  cached/fresh consumer coverage and native resource lifetime proof first.

These are static implementation constraints, not a new runtime patch. The
reproducer verifies 24 instruction sites from unwind-range boundaries, seven
direct calls to the population helper, native names/constants and the preserved
experimental ASI's delivery identity. Other profiles remain unmapped for this
new boundary.[^lighting-consumer] The subsequent
[bounded onset experiment](incoming-vehicle-readiness.md#lighting-side-onset-experiment)
uses the original population call's borrowing window, rather than keeping block
pointers for later writes. Its visual result and cached-refresh coverage remain
runtime questions.

[^lighting-consumer]: Hash-gated native Global disassembly and bounded instruction/call verification; no game execution or visual fade proof.

# Coverage-result publication

`002D66D0` schedules `CShadowRenderer::GetExtentsResults`, callback `002CC700`,
after the population dependency. That callback traverses holder head/count and
can write `C+78` at `002CCB76`. It requires positive configuration `+A6C`, normal
mode, a valid per-spatial query index, unsigned result-counter age below five,
a view-stability counter greater than five, and no detected view/config change.
The view test compares positional displacement and orientation against native
constants and updates saved context state. These counters are not proven
seconds or presented frames.[^producer-review]

Query scalar accessor `0034D530` calls `0034D3C0`, which consumes available
resource results and retains the last scalar and associated counter. Accessor
`00333840` reads that counter; `00344E30` acquires the resource written to `C+70`.
The factory/readback chain is now mapped separately below. The initial/template
value of `C+78` remains unproved. Coverage is not a directly writable world-distance
limit; no readback-stall timing or safe replacement scheduling rule follows.
[^producer-review]

## Occlusion query factory and nonblocking readback

`00344D90` acquires a query wrapper and falls back to `001EFE10(1)`. The latter
allocates a `20`-byte wrapper with vtable `02E63C90`, initializes its divisor byte
at `+14` to one, and passes descriptor `{1,0}` to device virtual slot `+C0`,
storing the result at wrapper `+8`. This is the D3D11 `CreateQuery` ABI with
`D3D11_QUERY_OCCLUSION`, not an event/fence query. Occlusion returns the number
of samples passing depth/stencil tests; it does not certify a shadow texture's
completion. The result's exact issue geometry/cadence remains unmapped.
[^background-query-review]

Wrapper virtual slot `+28` resolves to `001EA240`, a tail thunk to `001E2550`.
The `0034D3C0` caller passes wait=false. `001E2550` calls context virtual slot
`+E8` (`GetData`) with an eight-byte result and flag1 (`DONOTFLUSH`). On pending
`S_FALSE` it returns false without polling again on this path. Its separate
wait=true path can retry with flags zero, but that is not the mapped coverage
call. On success, it uses the low32 result bits and ceiling-divides by wrapper
`+14`'s current byte, then clears the pending byte at `+18`. The factory's
initial divisor does not prove it can never change. The higher accessor retains
the previous scalar/counter when a result is unavailable. Static nonblocking
control flow does not measure driver latency or total GPU cost.
[^background-query-review]

`0048CE20` copies a `90`-byte candidate template from argument10 `+70` at
`0048D163..0048D173`; this identifies how an initial `C+78` enters the object,
not its initial scalar value or a safe writer. Bounded immediate-store searches
at `+78/+108` produced unrelated stack/object matches and no proven initializer.
The native priority input's values/writers for visibly affected lamps also remain
unresolved. No coverage override, forced query wait or cache enlargement was
selected from these findings.[^background-query-review]

API semantics: [D3D11 query types](https://learn.microsoft.com/en-us/windows/win32/api/d3d11/ne-d3d11-d3d11_query)
and [GetData flags](https://learn.microsoft.com/en-us/windows/win32/api/d3d11/ne-d3d11-d3d11_async_getdata_flag).


# Ordinary admission predicates and budget

The saved manager body and instructions at `002E9CA0` through `002E9D33`
separate the base enable/factor checks from type, coverage and count decisions.
Configuration below is the object at `*(manager+18)`; field offsets remain
hexadecimal. These are consumer roles, not proofs of the fields' writers or
writable ownership.[^manager][^admission-instructions]

The comparison descriptions below assume finite normal inputs. Copied-input
reconstruction and actual post-native binding membership are separate evidence;
the floating-point and publication limits are detailed below.

| Input or boundary | Native decision after the base checks |
| --- | --- |
| Descriptor type `L+08` is 0 | Append a binding without consuming the ordinary count. |
| Type 2 | Append without consuming the ordinary count only when `L+40 & 0x84000000` is nonzero. |
| Type 4 | Skip admission. |
| Type 3 | Require configuration `+A48` nonzero before the ordinary path. Other nonspecial raw types enter that path directly, including unusual values outside0..4. |
| Configuration `+A6C`, reduced-mode byte `+F29`, candidate unsigned `C+78` | The coverage test passes when the configured threshold is nonpositive, reduced mode is set, or the scaled unsigned candidate value reaches the threshold. The native numerator at RVA `02E444EC` is binary32 `1.0` (`3F800000`). Context lookup and integer/float operations below determine its denominator. |
| Ordinary count | Attempt append only while the prior ordinary count is less than `B4 - (A8 != 0) + A8`. Ordinary count increments before the append helper; allocation failure can consume count without publishing a binding. Special types 0/2 do not consume this count. |

With normal fixed `B4=21` and `A8=4`, the ordinary ceiling is **24 light
records**. The first 20 ordinary bindings use the dynamic lane; later ordinary
bindings seek cached-owner associations. This is distinct from vehicle count,
queue entries and physical faces. The manager traverses the retained linked list
in its original order; the patch's chosen vehicle does not receive a separate
native exemption or promotion. Cache reconciliation and refresh nomination are
owned by [shadow pressure](shadow-pressure.md).[^manager][^manager-hook]

This fixed21/4 result is the normal-mode profile. Reduced mode substitutes
scheduler floor1/upper2 before the native first-candidate-dependent B4 adjustment,
even though the normal immediates are patched to21. Observe B4 and A8 before and
after the call; neither24 ordinary records nor20 dynamic positions is a universal
reduced-mode bound. The first retained candidate's type0/base-predicate status
also affects that adjustment.[^manager][^population-profile]

`C+78` participates in a normalized coverage comparison; its conditional query
writer and occlusion-query resource are mapped above; initial value and query
issue geometry/cadence remain incomplete. `C+68` includes a distance fade, not a writable distance threshold.
Admission omits the downstream queue/caster
work, but no measured CPU/GPU saving or safe earlier preparation mechanism
follows from these predicates alone.

# Coverage context and numerical reconstruction

The native coverage context is manager **argument5**, named `context` in the
hook. Let `table = *(argument5)` and let `index` be the dynamic uint32 at image
RVA `0361EE80`. The context object is `*(table + 8 + index*8)`; signed32 dimensions
are read at object `+10/+14`. Argument6/view position is a separate input. The
table's allocation/count and publication writer are not mapped, so observation
must validate pointer arithmetic and readable scalar spans without calling a
resolver or inferring a table-wide lifetime guarantee.[^admission-instructions]

The native `IMUL` keeps the **low32 bits** of width*height, interprets that result
as signed32, and selects signed `max(product,1)`. It converts this denominator
to binary32, divides binary32 `1.0` by it, converts zero-extended unsigned C+78
through the native signed64-to-binary32 instruction, then multiplies in binary32.
A widened mathematical area product or double-precision combined expression
can differ from this instruction sequence. The optional evaluator preserves
these separate rounded operations.[^admission-instructions][^population-profile]

Native branches also differ on unordered comparisons. With masked invalid
exceptions, `COMISS epsilon,factor; JA` does not reject an unordered factor;
`COMISS threshold,0; JBE` bypasses coverage on unordered threshold; and
`COMISS scaled,threshold; JC` rejects an unordered final comparison. COMISS may
raise an invalid exception if unmasked. Observation preserves the raw bits and
returns unknown for relevant nonfinite or subnormal values before doing floating
arithmetic; it does not reproduce native exception delivery. Numerical coverage
reconstruction additionally requires a copied round-to-nearest MXCSR setting.
The observer reads MXCSR without changing native floating-point control.
[^admission-instructions][^population-profile]

The optional Global profile independently proves the candidate/config/context,
cache and constant spans. It avoids the installed manager prologue and scheduler
immediate patches; a missing or mismatched proof disables observation only.
Other profiles need independently recovered proof, and these diagnostic data and
functions are excluded from Release. Source/image agreement and fixture checks
do not establish manual game acceptance.[^population-profile]

A reconstructed rejection means the copied values would take that predicate
under the supported numerical conditions. It is never a native branch trace:
native inputs may change between copying and consumption. `ordinaryEligible`
means pre-budget eligibility, while actual admission comes from a complete,
readable, uniquely matched binding vector. An unreadable or incomplete vector
must not turn into a false native omission.[^population-profile][^manager]

# .82 protected-owner omission narrowing

Four complete Global candidate snapshots at 500 ms spacing recorded finite1
with diagnostic extras0. The same complete, recent rank1 traffic owner was
protected but omitted from the native binding output in samples0-2. Its two
headlights were at original, zero-based candidate indices **5 and 7**, before
the limiter removed any other owners. A different traffic owner became rank1
and was admitted in sample3.[^admission82]

| Samples | Copied candidate counts | Admitted ordinary records | Special0/2 records | Cached bindings |
| --- | --- | --- | --- | --- |
| 0-2 | 75, 77, 81 | 19 in each | 2 in each | 0 in each |
| 3 | 81 | 21 | 2 | 1 |

The session reports the fixed21/4 profile. The omitted candidates occur early
in the list, later ordinary candidates are admitted, and the first three
ordinary totals remain below the mapped ceiling. Together with the source's
original-order filtering, this strongly points to **native eligibility before
binding publication** for these particular omissions. Late list-order budget
exhaustion, cached refresh selection and renderer face truncation do not explain
that sampled pattern. This is an inference from the mapped body and copied
before/after observations; concurrent input changes and native allocation
failure were not directly traced.[^admission82][^manager][^manager-hook]

The .82 observer copied type, descriptor flags, direction and full handle, but not
`L+0D`, `L+34`, `C+68`, `C+78` or the relevant threshold/context inputs. It
therefore cannot identify that sample's rejecting native predicate. Driver headlights
admitted in the same samples demonstrate that type3 was generally enabled;
they do not reveal the omitted owner's per-candidate factors. The later rank
change proves a separate selection replacement, without timing every visible
flash. These finite-limit samples do not establish the cause of fast-driving
pop-in at limit0.[^candidate-observer][^admission82]

# Global .85 admission under dense candidate pressure

The unmarked P-A tail contains256 complete manager observations with142..178
candidates per call. The disabled patch limiter keeps all candidates. Recomputed
binary32 gate results agree with all9539 emitted gate rows; expanding material
index deltas gives44505 candidate-call observations. Every call binds exactly
the first24 ordinary-eligible candidates in original order plus2 special ones.
The ordinary split is20 dynamic and4 cached, consistent with B4=21/A8=4.

Of33154 ordinary-eligible observations,6144 are admitted and27010 are omitted.
Among valid vehicle identities,21913 observations are eligible but omitted;
ten observed headlight transitions from eligible/unbound to eligible/bound follow
the list-order admission boundary. There is no mismatch against that boundary in
the retained256 calls. This supports ordinary admission competition in this
tail, distinct from the earlier .82 below-budget rejection pattern.

These are light/candidate observations, not distinct vehicle counts. Identity is
healthy in218 packets and deliberately unknown in38 with publication gaps or
overflow. The retained interval covers only the final approximately2.073 seconds
of an unmarked60-second recording; it does not identify the visible delayed
headlight or establish that admission pressure explains every slow-onset event.
No predicate override, priority change or capacity increase follows automatically.

# Global .87 whole-pass admission

All1200 complete sampled manager calls match the same rule: the first24
ordinary-eligible candidates in original kept-list order, or all such candidates
when fewer exist, plus2 special candidates. There are no expected-versus-native
binding mismatches. The ordinary budget is full in1105 calls and oversubscribed
in1103; no eligible omission occurs at or below24 eligible ordinary candidates.

The complete censuses contain165520 candidate occurrences, with47..297 per call.
Of76597 ordinary-eligible occurrences,28244 bind and48353 remain eligible/kept
but unbound (63.13%). Other copied results are56583 coverage rejections,26285
candidate-factor rejections and3655 excluded type4 candidates. These gates act
before admission and must not be mislabeled budget loss. The patch limiter is
disabled and retains every candidate in every sampled call.

Strict healthy, unique full-generation vehicle identity covers74827 occurrences:
57899 ordinary eligible,16928 rejected by coverage and38536 eligible/kept/unbound.
One identified light remains outside the admission frontier across238 consecutive
samples spanning11.8488s. Another remains outside across216 samples spanning
10.7497s, then crosses from ordinary rank26 to24 at the next sample and receives
a cached binding with immediate update. There are377 sampled transitions from
eligible/kept/unbound to admitted. These are sampled candidate occurrences and
observed spans, not proof of uninterrupted nonadmission between samples.

This extends the .85 admission-competition evidence across the driving pass.
Neither the binary nor its full identity supplies the screen position, distance,
upstream priority score or exact light seen drawing in slowly. The result selects
the admission boundary for further correction analysis; it does not prove that
native list order is wrong or authorize a replacement priority, gate override
or capacity increase.

# Paired type3 observations in the .87 pass

Grouping each sample by valid, unambiguous full-generation vehicle/entity
identity yields 37,379 observations with exactly two retained type3 records;
69 singleton groups are excluded. These are candidate headlight pairs, not
visually identified lamps or counts of distinct vehicles/events.[^producer-review]

| Copied pair state | Pair-sample observations |
| --- | ---: |
| Both ordinary-eligible, both admitted | 9,422 |
| Both ordinary-eligible, neither admitted | 18,974 |
| Both ordinary-eligible, only one admitted | 472 |
| Both below the coverage threshold | 8,349 |
| One coverage-rejected, one ordinary-eligible | 162 |

Every one of the 472 eligible split pairs straddles ordinary rank24. A grouping
change could alter these split outcomes, but most fully eligible omitted pairs
lose both lights; grouping alone would not address those omissions. Preserving
two-light groups at a fixed budget can displace another light and must account
for native priority, special entries and physical faces. Repeated samples are
not independent visual events. The capture lacks the native priority key,
distance inputs and exact visible-light identity; it cannot determine which
competing shadows should win.[^producer-review]

# A second shadow-enable consumer

`002C1220` resolves the descriptor from `S+50` through `025AEA10` and descriptor
registry VA `7FFC3D2A8240`. For types 1 and 3 it reads `L+0D`; when zero, several
configuration-dependent setup scalars become zero before state comparison and
setup. This is a concrete consumer outside manager admission. A persistent
descriptor write therefore has a broader native observation surface than a
temporary manager-list filter. No timing or GPU saving is inferred.[^setup-consumer]

Registration `02599870` names `bCastShadow` at property-relative `+5`, maximum
distance at `+44`, and fade distance at `+48`. A property base at `L+8` would
explain the enable offset, but that correspondence is not yet a proven writable
ownership contract. Metadata alone supplies neither a native fade API nor a
temporal/dither transition.[^metadata]

# Ownership limits and evidence requirements

Candidate construction, list publication, priority/distance sorting and factor
writers and occlusion readback are now statically mapped above. Descriptor
ownership, initial coverage, query issue geometry/cadence and a safe earlier
mutation boundary remain incomplete.
Before filtering earlier, recover:

1. Relevant `L+0D` writers and writable/published descriptor ownership,
  template sharing, copy-on-write and dirty propagation.
2. Authoritative publication/thread boundary, lifetime and rollback behavior.
3. Current candidate membership and complete lamp groups, plus proven
  headlight versus siren/world/shared identity at the proposed boundary.

Do not substitute physical enable setters `007862C0`/`00785C20`: they update
light-object flags and publish the combined enable state to spatial `+48`.
Do not call `02593920` as a guessed read-only lookup: its resolver `025BB1E0`
can allocate/copy a `58`-byte spatial record and publish modified state.
[^physical-setters][^resolver]

The existing owned-scalar batch publication can maintain a derived identity
index, but it does not contain the complete current candidate census. Native
vehicle updates are conditional; unchanged publication is not unchanged
admission. Preserve full-handle generations, ambiguity/expiry and nonwaiting
fail-open behavior. The [adaptation plan](wd2-shadow-reference.md) owns that CPU
optimization; [vehicle selection](vehicle-shadow-selection.md) owns the current
policy. Vehicle-owned type 1 is not a proved siren classification.

[^manager]: Global manager identity and decompiled/disassembled predicates.
[^admission-instructions]: Saved Global instruction excerpt corroborates the eligibility reads and ends at the ordinary budget comparison.
[^admission82]: Complete four-sample Global .82 log; candidate indices and ordinary/special counts are derived from its recorded rows.
[^candidate-observer]: Candidate copying omits the native eligibility inputs; post-native observation joins copied candidates to the binding vector.
[^population-profile]: Immutable Global instruction/constant spans and pure finite copied-input evaluator; optional diagnostic proof does not authorize mutation or establish runtime acceptance.
[^queue-builder]: Native admission output consumption and queue-entry writes.
[^visibility]: PrepareShadowVisibility callback supplies the current list holder.
[^manager-hook]: Existing pre-manager list filtering and immediate restoration.
[^setup-consumer]: Function `FUN_7ffc39eb1220` in the saved consumer export.
[^metadata]: Native light property registration, not a writable API proof.
[^physical-setters]: Native physical light enable publication.
[^resolver]: Native spatial resolve/copy/publication mechanism.
[^producer-review]: Hash-gated Global image inspection and strict CRC/schema decoding of the existing .87 capture; preserved script, disassembly, input hashes and aggregate results. Static mapping and sampled observations establish no visual improvement.

[^background-query-review]: Hash-gated Global wrapper factory, concrete vtable and chained-unwind readback exports; static evidence only.
