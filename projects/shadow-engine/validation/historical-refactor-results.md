---
type: Historical Validation
title: Binary equivalence as a control for native-patch refactoring
status: draft
sources:
- resource: ../../../evidence/catalog.json#E-24e7e608eade
  title: Preserved historical technical evidence
- resource: ../../../evidence/catalog.json#E-c2336fbf9bfe
  title: Preserved historical technical evidence
---

# What was compared

A Shadow Engine refactor split 2,903 source lines into eight ordered include
modules. Before the version update it reproduced SHA256
`D622440495530E905C96B0B8D5CC6C0D9A4E7EDE3F0979BF75341F8A260415C0`.
The two final 76,288-byte binaries differed in 42 version/checksum bytes and no
executable ranges. The versioned output hash was
`23334CBE5B0D69619F23CFDFE610489EA553C94EB52D788BFDA777911E8F7BE2`.

A later refactor replaced 98 transitional aliases with 457 explicit context
accesses and preserved identical ASI bytes. Bootstrap responsibilities were split
into discovery/validation, transaction handling and orchestration.

# What this proves

Under the recorded compiler and inputs, a byte-identical result controls for
accidental code-generation changes. Version/checksum-only differences require
range-aware comparison rather than a whole-file hash alone. Neither comparison
proved a performance improvement: the existing FPS regression survived the first
refactor. Source modularity is not evidence of altered engine behavior.
