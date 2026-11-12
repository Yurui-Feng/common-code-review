# Review lenses

Apply only the sections relevant to the change. These are prompts for investigation, not automatic findings or a required checklist.

## Failure semantics

Trace missing, unknown, empty and partial results through their callers. Watch for success inferred from "not one known failure," broad error handling that substitutes a plausible value, and batches that hide failed items. Check whether a message is acknowledged or a transaction committed before its work succeeds.

Raise a finding when a reachable failure is represented as success or required configuration is accepted unusably. Preserve deliberate optional values, documented fallback behavior and best-effort operations that expose their limits to callers. Do not add redundant validation to trusted internal invariants.

## Shared contracts and compatibility

Follow changed names, keys, schemas, units, error types and defaults through producers and consumers, including other packages and stored data. Check both directions of serialization, cleanup against the writer's layout, migrations and mixed-version operation when supported. Reuse an authoritative definition where appropriate; prove that independent definitions agree where sharing code is impractical.

Flag concrete disagreement or a violated compatibility promise. Do not demand a cross-language shared library merely to avoid a small intentional duplication. If the other side is unavailable, identify the unverified contract rather than asserting it is broken.

## State, ownership and resource lifetime

Inspect lifetime, mutability, concurrency, cancellation and disposal. Watch for required configuration frozen at the wrong time, global mutable state leaking between requests or tests, unchecked asynchronous work, partial initialization and resources never released after failure.

Evaluate import-time initialization and singletons in the actual runtime. A safe immutable constant, intentional startup validation or a documented long-lived client pool is not inherently wrong. Prefer clear ownership and a test seam when the absence of either causes concrete problems; do not require dependency injection everywhere.

## Retries, timeouts and idempotency

Check which failures are retryable, whether the operation may already have taken effect, and how duplicate delivery is handled. Compare child work, parent deadlines and cleanup time. A nominal timeout is ineffective if cancellation or resource cleanup waits indefinitely. Retry budgets and backoff must fit the caller's deadline and downstream contract.

Prefer the framework's retry or polling mechanism when it expresses the needed semantics. Custom coordination may be necessary; inspect its deadline, cancellation, completion condition and duplication rather than rejecting it by name. Do not retry non-idempotent effects without an explicit contract.

## Work bounds and performance

Trace user-controlled sizes, page sizes, fan-out, nested calls, queues and retry loops. Distinguish bounded batch processing from unbounded work on a request path. Check pagination completeness and progress; ensure a cap does not silently lose data that the interface promises to return.

Report a reachable resource or latency problem with the relevant input scale or call count. Avoid speculative micro-optimizations, arbitrary limits and blanket bans on scans. Use measurements or known complexity and deployment bounds where they matter.

## Untrusted input and authorization

Track authority and data across trust boundaries: tenant identity, authorization, injection sinks, path resolution, secrets, deserialization and subprocess arguments. Validate at the relevant boundary; escaping or validation for one sink does not establish safety for another.

For LLM features, treat retrieved text and tool output as untrusted data. Check whether they can change instructions or trigger privileged actions, and whether evaluation data leaks into training or candidate selection. Delimiters alone do not enforce authority. Tie findings to an actual data-to-action or measurement path.

## Tests that establish behavior

Read test bodies, assertions, fixtures and the actual test/build configuration. Check whether assertions can fail for the intended regression, whether mocks erase the behavior being tested, and whether checks described as type, timeout, integration or end-to-end tests actually exercise those properties. Assertions should establish the relevant contract without pinning irrelevant internals.

Prioritize changed behavior with meaningful risk: failure paths, boundary cases, state transitions and compatibility. Explain the specific regression a missing check would catch. Do not require tests for cosmetic edits or add tests that merely duplicate the implementation. Avoid forcing every behavior into every test layer.

## Test structure and isolation

Keep scenarios readable while placing reusable setup and mechanics in the framework's natural fixture/helper locations. Consider a shared helper for repeated mechanics only after identifying actual occurrences and a stable common responsibility. Parametrize cases whose behavior is structurally the same; preserve separate cases when their reasoning differs.

Check fixture scope against workers, retries, parallelism and teardown. Verify cleanup on partial setup failure and avoid shared identifiers that let tests delete each other's state. Use tolerant numeric assertions for calculations crossing representation boundaries when justified; exact equality remains correct for exact contracts. Split files along existing responsibilities, not arbitrary length targets.

## Abstractions and change scope

Ask what an interface, wrapper, class, registry or new dependency buys its callers. Look for copied logic drifting from an existing implementation, unnecessary forwarding layers and special cases spread across generic dispatch paths. Verify the existing facility actually meets the need before recommending reuse.

Favor the simplest shape that expresses the current requirements and stable extension points. A single implementation may still need an interface for a public boundary or test seam. Do not replace a few clear cases with a generic framework, or remove an abstraction just because it has one caller.

## Infrastructure and deployment

Compare names and identifiers with their real uniqueness scope and length constraints. Check resource replacement, retained data, permission scope, configuration propagation, dependency order and rollback behavior. Trace a declared permission to the workload that uses it; distinguish control-plane success from a usable deployed service.

Use the repository's provider and deployment conventions. Do not copy a cloud-specific naming rule into another platform or require a live deployment for an ordinary local review. Call out material deployment assumptions and verify them when authorized and feasible.

## Documentation and operational instructions

Check changed examples, commands, schema descriptions, defaults and file references against the implementation. Confirm the instructions work from the stated starting state and disclose significant destructive or customer-affecting effects within the user's authorization model.

Flag contradictions and missing steps that make the procedure fail or cause material surprises. Documentation may intentionally describe a future design; label that context instead of judging it as current behavior. Do not demand new approval prompts when the workflow already carries the necessary authority.

## Comments and communication

Prefer comments that explain non-obvious intent, constraints, invariants or tradeoffs. Check stale behavior claims, dead references, commented-out code and prose that obscures a small function. Preserve public documentation, legal notices, generated markers, analyzer directives and annotations that supply types or other semantics.

Report inaccurate comments when they mislead a consequential decision; treat length and narration as optional style feedback unless they violate an applicable requirement. Keep review descriptions focused on behavior and evidence rather than a mechanical inventory of every file.
