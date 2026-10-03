---
type: Technical Primer
title: Game engine fundamentals through Shadow Engine
description: Rendering, resource lifetime and binary investigation concepts, with qualified
  Shadow Engine examples.
tags:
- shadow-engine
- graphics
- rendering
- resource-lifetime
- reverse-engineering
status: draft
sources:
- id: historical-primer
  resource: ../../../evidence/catalog.json#E-6d57db2178a8
  title: Preserved historical engine fundamentals primer
- resource: ../architecture/shadow-pipeline.md
  title: Shadow Engine Pipeline
- resource: ../architecture/engine-capacity-layout.md
  title: Shadow Capacity Layout
- resource: ../architecture/resource-pass-lifecycle.md
  title: Shadow Resource and Pass Lifecycle
- resource: ../architecture/black-flicker-diagnostics.md
  title: Black Shadow Flicker Attribution
- resource: ../architecture/external-slice-results.md
  title: External Slice Results
- resource: ../architecture/vehicle-light-classification.md
  title: Vehicle-Light Classification Boundary
- resource: ../architecture/patch-transactions.md
  title: Patch Transaction Model
- resource: ../architecture/runtime-profiles.md
  title: Runtime Profile Architecture
---

# Frames and cooperating systems

A game engine combines gameplay, animation, physics, visibility, lighting,
rendering, audio and streaming. At 60 frames per second, one frame interval is
approximately 16.67 ms; at 30 it is 33.33 ms. Those intervals are a scheduling
budget, not a guarantee that every subsystem completes sequentially within one
CPU thread.

```text
input/network -> gameplay -> animation/physics -> visibility/LOD
              -> lighting/shadow selection -> render graph/commands
              -> GPU submission -> presentation
```

Real engines overlap these stages. The GPU may render one frame while the CPU
prepares another and streaming anticipates later demand. Worker threads can
build different parts of a frame concurrently. A value that is correct when
produced can become invalid before a later consumer uses it. This motivates
observing a resource at several lifetime boundaries rather than only at the
visible failure.

A gameplay vehicle also becomes several specialized representations: transforms
and velocity for simulation, models and materials for rendering, light records
for lighting, shadow eligibility for selection, and separate damage/audio state.
A compact renderer light may lack a stable pointer back to the vehicle. Names,
similar positions or renderer type alone cannot replace a proven ownership join;
the [classification contract](../architecture/vehicle-light-classification.md)
states what Shadow Engine actually knows.

Contiguous arrays, handles and data-oriented layouts can improve locality and
batch processing. They also allow a bad index to overwrite a neighboring field
while remaining inside allocated memory, so corruption need not crash immediately.

# CPU work, rasterization and render graphs

The CPU commonly selects visible meshes, important lights, shadow work,
resource residency and pass dependencies. The GPU performs parallel numerical
work such as vertex transformation, rasterization, depth tests, texture sampling,
material/lighting evaluation and post-processing. A CPU resource pointer usually
refers to a wrapper, handle or API view rather than directly to texture pixels.

In conventional rasterization, vertices pass through model, world, view and
projection transforms; triangles are assembled and rasterized into covered
samples; shaders evaluate material and lighting; depth and blending determine
the resulting output. Engines use intermediate targets for depth, normals,
materials, shadow maps, reflections, accumulated lighting and temporal history.

A render pass consumes specified inputs and produces outputs. A render graph
describes dependencies between these operations. If one pass reads a texture
produced by another, execution and resource lifetime must respect that dependency.
The existence of a CPU graph node or a returned submission call does not prove
that asynchronous CPU work or GPU work has completed.

Shadow Engine consequently needs both added shadow resources and their producer
and consumer paths. An allocated map with no usable pass registration is not an
operational shadow slot. See [resource/pass lifetime](../architecture/resource-pass-lifecycle.md).

# Shadow mapping and distinct budgets

A shadow map is commonly a depth texture rendered from a light's viewpoint.
For a spotlight, nearby geometry is rendered using the light's projection. During
normal rendering, a shaded point is transformed into that projection and its
depth is compared with the stored surface depth. A point behind that surface is
shadowed relative to the light.

A point light needs directional coverage around its position. Six cube-map
faces are a common general technique; engines can use different projections or
specialized face layouts. This general model does not prove that a particular
Watch Dogs queue entry safely supports six faces. Its native layout and observed
face-count limits require separate evidence.

Shadow work consumes texture memory, repeated geometry rendering, CPU command
construction, GPU bandwidth and synchronization. These questions remain distinct:

| Boundary | Question |
| --- | --- |
| Allocation | Does the required storage or resource exist? |
| Admission | Is the light selected for shadow work? |
| Scheduling | Is its map updated during this cycle? |
| Residency | Is the existing shadow retained or replaced? |
| Consumption | Does the later lighting pass sample the intended result? |

Increasing allocation does not guarantee admission, update cadence or residency.
Watch Dogs' dynamic and cached-owner lanes can compete before physical faces are
full; retained cached owners share a coarse refresh position. The detailed
[pipeline](../architecture/shadow-pipeline.md) owns those engine-specific facts.
Visible quality loss alone does not identify which boundary failed.

# Pools, inline arrays and coupled expansion

Real-time engines use fixed pools, arenas, ring buffers, handle tables and
freelists to control allocation and reuse. Consider this illustrative structure:

```c
struct ShadowQueueExample {
    ShadowEntry entries[16];
    uint32_t count;
    TailState state;
};
```

Changing a logical bound from 16 to 24 does not enlarge `entries`. Added writes
could overwrite `count`, `state` or another allocation. A coherent expansion
must account for physical allocation, producer and consumer bounds, moved tail
fields, all instructions that access those fields, associated handles/passes and
the lifetime of pointers into the storage.

Shadow Engine's real queue has multiple independently growing regions, so even
one uniform relocation stride is insufficient. The
[capacity layout](../architecture/engine-capacity-layout.md) records their exact
derivations and the failed uniform-stride experiment. These general examples
are teaching aids, not a replacement structure definition or patch recipe.

# Wrappers, jobs and ownership

```text
logical key -> lookup -> engine wrapper/handle -> API view -> GPU allocation
```

A wrapper can carry descriptors, reference counts, state and deferred destruction.
It must survive its last legitimate consumer, which may run after the submitting
CPU call returns. Acquisition and release symmetry matter even when two acquired
references have the same pointer value. Pointer equality does not collapse two
ownership obligations into one.

Builders can execute synchronously on one path and as jobs on another. Record
generation, producer cycle, task identity and thread context help determine
whether observations belong to the same work. Without that connection, comparing
one generation's lookup with another generation's renderer state can falsely
suggest corruption. A diagnostic association is useful evidence but does not
automatically become authority to reset or retire resources.

The historical F8 containment repair illustrates this distinction. Restoring a
damaged field could otherwise release a displaced resource incorrectly. Its
sidecar remembered and natively acquired the displaced resource, restored the
expected field and paired that ownership with a later release. This added wrapper
work and contained an observed failure; it was not the permanent architecture.
The recovered indexed overwrite was subsequently prevented by routing extra
results into separate storage. The current
[external-result contract](../architecture/external-slice-results.md) owns
publication, rejection, duplicate handling and retirement. The old sidecar is
historical evidence, not an active repair recommendation.

# Offsets, hooks and executable identity

When source declarations are unavailable, a recovered field can be named by its
byte offset. The historical render-record resource fields include `+0xF8`,
`+0x100`, `+0x108`, `+0x110` and `+0x118`; those offsets are not Ubisoft semantic
names and do not identify the same field in arbitrary objects.

```asm
mov [r14+110h], rax
```

This stores the 64-bit value in RAX at byte offset `0x110` from the base in R14.
Establishing what the base and value represent requires data-flow and
calling-convention evidence. A plausible nearby constant is not enough.

A detour redirects a native call to a hook; a trampoline preserves the displaced
instructions so the original execution can continue. In the Windows x64 calling
convention, the first four pointer/integer argument positions use RCX, RDX, R8
and R9, with later arguments on the stack. Incorrect signatures, instruction
boundaries or preserved state can corrupt execution. Complete validation and
transactional installation belong to the [patching contract](../architecture/patch-transactions.md).

Subtracting a module's load base from an address gives its relative virtual
address, or RVA. This removes that load's ASLR displacement, not differences
between executable builds. A return RVA can distinguish callers of a shared
lookup only for the mapped runtime identity. Always retain the applicable
[profile and proof scope](../architecture/runtime-profiles.md).

# Finding a writer by bracketing observations

Suppose one same-lifetime observation is correct at A and wrong at B. A new
checkpoint C can narrow the interval: wrong at C suggests `(A, C]`; correct at C
suggests `(C, B]`. This reasoning requires reliable ordering and identity. With
asynchronous jobs, the observations may instead be on different execution paths
or generations, so task/cycle evidence must establish the relationship first.

The historical primer traced F8 from a correct lookup through the F110 lookup
return, then through a final tail lookup reported at RVA `0x3DE0FE`, before a
wrong builder-exit value. It proposed examining the remaining F118 store and
renderer-building operations. That was an intermediate bracket, not a recovered
bad instruction or a current investigation target. Later asynchronous evidence
refined the model, and exact SliceExecute indexed stores explained the overwrite.
The [black-flicker investigation](../architecture/black-flicker-diagnostics.md)
preserves that progression and the rejected writer hypotheses.

Wrong writes can remain legal memory accesses: null in an optional field,
another valid resource pointer, an adjacent array slot or a semantically wrong
handle. They may produce missing shadows, black frames or bad releases without
a crash. Conversely, missing log termination does not establish a crash.
Observed behavior, static mapping and causal inference should remain distinct.

# Reading the system through one resource

Follow one resource from allocation through production, scheduling, consumption
and destruction. Match emitted fields to their source and native instructions,
then ask who owns each value, whether it is a pointer/handle/index/inline object,
how long it stays valid, which thread can write it, and whether a call executes
work immediately or merely schedules it. Distinguish physical capacity from a
logical policy and correlation from a demonstrated cause.

A useful learning sequence is coordinate spaces and linear algebra, rasterization,
shadow mapping, render graphs and synchronization, data-oriented storage,
job systems, Windows x64/PE/ASLR, assembly data flow and resource ownership.
The purpose is to trace a complete producer/consumer contract rather than
memorize isolated addresses or infer safety from a successful allocation.
