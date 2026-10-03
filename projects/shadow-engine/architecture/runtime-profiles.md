---
type: Compatibility Contract
title: Runtime Profile Architecture
description: Immutable regional executable layouts selected before common patch policy is applied.
tags:
- shadow-engine
- runtime-profile
- regional
- compatibility
status: draft
sources:
- id: profiles
  resource: ../../../evidence/catalog.json#E-4d85852a0d8b
  title: Runtime profile table
- id: preflight
  resource: ../../../evidence/catalog.json#E-73d1a7ddc532
  title: Runtime preflight
- id: cloth-profile-module
  resource: ../../../evidence/catalog.json#E-1f29073db08d
  title: Diagnostic-build parser profile data
- resource: ../../../evidence/catalog.json#E-06bda26c626e
  title: Runtime preflight
---

# Model

Global/04DF, Shev/A4EE, VMPless, Complete Edition and Asia/Miru are
represented by immutable `RuntimeProfile` data.
Each profile describes its PE identity, clustered or explicit RVA strategy,
helper addresses, validation signatures, and detour prologue.[^profiles]

# Invariant

Core modules do not branch on profile number or store label. Capacity,
residency, admission, result routing, and cleanup are shared policy. A new build
is supported by adding a complete, validated profile rather than forking the
engine implementation.

# Failure behavior

Profile selection must be unique and coherent. Every required mutation site is
validated during read-only preflight. Unknown, ambiguous, or incomplete layouts
may produce diagnostics but receive no hooks or writes.

[^profiles]: Runtime profile table

# Optional research profiles

The separate cloth experiment stores independently validated GEOM parser RVAs
in profile data: Global, VMPless, Complete Edition and Asia have mapped boundaries;
A4EE remains zero/inactive. This does not imply that cloth hooks ship in the active
shadow build. See [cloth evidence](../research/cloth-high-fps-investigation.md).
