---
name: code-simplification
description: Simplify existing code to improve clarity and maintainability without changing behaviour. Use for requests to simplify or refactor code, including recent changes. Do not use for feature development or prose edits.
---

# Code Simplification

Make code easier to understand and change. Preserve its observable behaviour.
Prefer clear code over fewer lines. Reduce the effort needed to understand the
code.

## Choose the scope

Use the files, changes, or component that the user specifies. If the request
refers to recent work, inspect the relevant diff. Also inspect the surrounding
code. If you cannot identify the target, ask which code to simplify before you
edit it. Do not expand a local simplification into a refactor of the entire
repository.

Before you choose changes:

1. Read the applicable repository instructions.
2. Inspect the callers and tests.
3. Identify the conventions in nearby code.

Preserve existing user edits. Exclude unrelated changes from the diff.

## Preserve behaviour

Unless the user explicitly requests a behaviour change, preserve these
properties:

- Return values, public signatures, types, and supported inputs.
- Side effects and their order, including mutations, input/output operations,
  and emitted events.
- Error conditions, error details that callers depend on, and recovery
  behaviour.
- Evaluation order, short-circuit evaluation, lazy evaluation, and the order of
  asynchronous operations.
- Relevant performance characteristics, resource cleanup, and concurrency
  guarantees.

Before you treat two expressions as equivalent, check the language rules. Check
these differences where applicable:

- Truthiness checks and null checks.
- Missing values and empty values.
- Equality checks and type coercion.
- Single evaluation and repeated evaluation of expressions with side effects.

If you find a bug, distinguish the bug fix from the simplification. Do not
change behaviour without telling the user. If the bug is outside the requested
scope, report it separately.

## Simplify where it helps

Choose changes that make the code's intent clearer:

- If exit paths and cleanup remain equivalent, use guard clauses to reduce
  nesting.
- Remove redundant branches, temporary state, or forwarding layers that add no
  useful meaning.
- If duplicate code implements the same rule and is likely to change together,
  combine it.
- Use names that explain the purpose of each item.
- Keep useful intermediate variables.
- Keep related logic together.
- Extract a helper when it names a distinct operation or removes repeated
  logic.
- Use established project utilities and patterns when they clarify the code and
  keep important behaviour visible.

Prefer clear control flow over nested ternary expressions, dense expressions,
or complex abstractions. Do not extract a helper only to move lines elsewhere.
Do not add support for hypothetical future needs. Do not add new dependencies
for a local simplification. Do not make broad architectural changes for a local
simplification. Do not combine code with different responsibilities just
because it looks similar.

Remove code only when evidence shows that nothing uses it. Check the relevant
references. Where applicable, check dynamic registration, reflection,
configuration, generated consumers, and public entry points. If you cannot
establish whether anything uses the code, keep it. Explain the uncertainty.

## Keep comments and documentation accurate

Follow the `documentation` skill for comment conventions and writing style.
When simplifying, apply these additional rules:

- Do not weaken or delete comments that explain constraints, trade-offs, or
  known gotchas to make the code look shorter.
- Remove a comment that restates the code only when your change makes it
  redundant or when it sits in code you are rewriting.
- Update or remove comments, docstrings, and examples that your change makes
  inaccurate.
- Delete commented-out code only in the code you change. Leave it in unrelated
  areas.
- Do not add `TODO` comments to defer parts of the simplification.
- If a simplification forces a non-obvious structure, record the reason in a
  short comment.
- Because behaviour is unchanged, public API documentation and the changelog
  normally stay as they are. Update them only if your change affects what they
  describe. If you find that they are already wrong, report it separately.

## Verify the result

Make changes in small, related groups. Review the diff for unintended behaviour
changes. Compare the original and revised execution paths. Include boundary
conditions and failure cases that the edit affects.

Run the repository checks that are appropriate for the change. These can
include focused tests, type checks, lint checks, or builds. If the refactor
could change important behaviour without test coverage, add or update a test.
Do not create tests that only repeat the implementation structure.

If a check fails, determine whether your change caused the failure. Fix
failures that your change introduced. If you cannot verify behaviour, state
what remains unverified. Do not claim that you proved equivalent behaviour.

In the final response, explain what became simpler. State which checks you ran.
Describe any remaining uncertainty. If no change would clearly improve the
code, say so. Do not force a refactor just to produce a diff.
