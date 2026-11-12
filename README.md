# Common Code Review

A portable agent skill for useful code reviews across languages and frameworks. It follows changed behavior through callers and contracts, verifies suspected defects, and reports actionable findings with severity and file/line evidence.

The core principles were adapted from historical review practices. This repository contains a newly written, generalized skill and synthetic examples; it contains no archived transcripts, internal links or company-specific source code.

## Use

With the skill installed in a compatible agent:

```text
Use $common-code-review to review this branch against main.
Focus on correctness, shared contracts and test coverage. Report findings; do not edit.
```

Other useful requests:

```text
Use $common-code-review to review this pull request, including its migration path.
Use $common-code-review to audit this module; existing defects are in scope.
Use $common-code-review to review and fix this change, then run the relevant checks.
```

For an agent without skill discovery, ask it to read `SKILL.md` and the relevant sections of `references/review-lenses.md`. Keep both files together so the reference resolves. Follow the host's required review format when it differs from the example.

## Install and export

Clone this private repository using an account with access. For Codex, place or symlink the `common-code-review` folder under your configured skills directory (`~/.codex/skills` by default). For other agents, use their supported skill installation location or load the files explicitly.

Export a portable bundle from a clean checkout:

```sh
git archive --format=zip --prefix=common-code-review/ --output=../common-code-review.zip HEAD
```

The archive has no runtime dependencies. `agents/openai.yaml` supplies optional Codex display metadata; the review instructions work without it. Installation does not change repository policies or authorize publishing, merging or deployment.

## Contents

- [SKILL.md](SKILL.md): scope, review workflow, false-positive controls and reporting.
- [Review lenses](references/review-lenses.md): targeted guidance for contracts, failures, tests, state, security, performance, design and documentation.
- [Validation notes](validation/RESULTS.md): the checks performed and their limits.

## Boundaries

Review conclusions depend on the code and context available. The skill reports verification limits and distinguishes demonstrated problems from open questions. It avoids automatic bans on globals, custom polling, long files, single-implementation interfaces or missing tests. Each concern must be justified in its actual language and runtime.
