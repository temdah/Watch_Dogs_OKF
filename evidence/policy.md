---
type: Technical Reference
title: Evidence and redistribution policy
status: draft
sources:
- resource: catalog.json#E-396fa4cfc699
  title: Preserved historical technical evidence
---

# Evidence and redistribution policy

This bundle contains reusable Watch Dogs programming knowledge and technical
evidence summaries. Mod implementation source is maintained separately. It does not publish:

- Ubisoft executables or game data;
- captured process images or memory dumps;
- crash dumps or user save data;
- proprietary decompiler exports that reproduce substantial game code;
- third-party loader/compiler binaries without explicit redistribution terms;
- local machine paths, credentials or private test material.

Referenced raw artifacts remain private research provenance. Public conclusions
must be understandable without downloading those artifacts.

## Claim labels

- **Runtime-observed:** recorded by a preserved clean-session log or direct user
  observation, with the observation boundary stated.
- **Statically confirmed:** supported by recovered instructions, writers,
  readers and control flow.
- **Inference:** the strongest current explanation, not instruction-level proof.
- **Untested:** built or proposed but not validated in the game.

Visual observations must not be promoted to complete fixes without repeatable
captures. Lack of a reported crash must not be described as proof of unlimited
stability.
