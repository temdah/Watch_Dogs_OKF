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
- resource: ../../../evidence/catalog.json#E-ee70408dc3e7
  title: Global candidate-holder publisher and unresolved virtual producer
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

The Global body at `003DC780` obtains a primary candidate holder through the
renderer interface's indirect slot `+20`, then publishes it to render-record
`+40`, retaining a fallback-holder case. The retained image independently
corroborates call bytes `FF 50 20` at `003DD3C9` and store bytes `49 89 47 40`
at `003DD3DD`. The callback `003C6CE0` passes that holder to `0030A570`, whose
manager call receives the holder's head/count. This confirms the ownership
handoff, not the holder's insertion, sorting or priority policy.

A second indirect call at `003DD428` supplies an alternate holder at record
`+48`; it must not be merged with the primary stream. The concrete unresolved
producer is the primary receiver's slot `+20` implementation. Its comparator,
key inputs, insertion stability and complete-light-group semantics are not
established by the caller or the sampled first24 admission result. Descriptor/
candidate factor writers are also separate from this holder assignment.
These are static Global roles with an exact-byte cross-check, not live object
identity or authorization to permute candidates or write native descriptors.

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

`C+78` participates in a normalized coverage comparison; its producing subsystem
and physical meaning remain unproved. Neither it nor `C+68` is established as a
writable world-distance threshold. Admission omits the downstream queue/caster
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

The actual candidate constructor, `C+68`/`C+78` writers and list publication
boundary remain unmapped in this bounded review. Before filtering earlier, recover:

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
