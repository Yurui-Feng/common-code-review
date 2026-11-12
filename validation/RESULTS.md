# Validation

Date: 2026-11-11.

This is a structural and editorial check of the skill package. It is not an independent model evaluation or a benchmark of review accuracy.

## Package checks

- The skill-creator validator accepts the frontmatter, naming and completed instructions.
- The UI metadata names the same skill and its default prompt invokes it correctly.
- Relative Markdown references resolve within the exported folder.
- The runtime instructions require no scripts, proprietary services or installed libraries.
- An export is checked by extracting the ZIP and comparing every file with the committed source.
- The export excludes the local archival evidence, machine paths, credentials and company-specific material.

## Manual scenario walkthrough

| Scenario | Intended review decision |
|---|---|
| A Python worker catches a failed required write, then acknowledges the item as complete. | Trace the write failure to lost work and report the failure semantics defect. |
| A JavaScript producer renames a wire field while a checked-in consumer still reads the old field. | Report the concrete contract mismatch with both locations. |
| A Go service reuses an immutable, concurrency-safe client initialized during intentional startup validation. | Do not flag a global or initialization merely because it exists. |
| A test parameterizes equivalent cases and keeps lifecycle setup in the framework's normal fixture. | Do not demand another parametrization or a thin fixture wrapper. |
| An external consumer's behavior is unavailable. | State the unverified compatibility assumption; do not invent its behavior. |
| A change corrects spelling in a comment without changing a contract or behavior. | Do not demand a new test or unrelated refactor. |

These walkthroughs check the instruction design only. They have not been run as automated reviewer trials. Future evaluation should use unseen changes and measure both valid findings and false positives; retain the repository context and expected behavior when comparing results.
