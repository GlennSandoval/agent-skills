---
name: documentation-and-adrs
description: Records decisions and documentation. Use when making architectural decisions, changing public APIs, shipping features, or when you need to record context that future engineers and agents will need to understand the codebase.
---

# Documentation and ADRs

## Overview

Document decisions, not just code. The most valuable documentation captures the
*why* — the context, constraints, and trade-offs that led to a decision. Code
shows *what* was built; documentation explains *why it was built this way* and
*what alternatives were considered*. This context is essential for future
humans and agents working in the codebase.

## Writing style

Unless explicitly instructed otherwise:

- Use New Zealand English spelling and conventions, such as _initialise_,
  _optimise_, _colour_, _behaviour_, and _organisation_. This takes precedence
  over spelling recommendations in either style guide.
- Choose the writing style for each section based on its purpose:
  - Use the [Google style guide](https://developers.google.com/style) for
    general developer documentation, such as explanations, concepts,
    architecture, decisions, and rationale.
  - Use [ASD-STE100](https://www.asd-ste100.org/) for detailed technical
    instructions that tell readers how to perform a task, such as changing code,
    installing or configuring tools, or following a technical procedure.
  - If a section contains both explanation and instructions, separate them into
    sections or subsections where practical. Use the style that matches each
    part; do not apply one style to the whole document by default.
- Write clear, concise, reader-focused documentation. Use active voice,
  descriptive headings, and consistent terminology.
- Wrap Markdown prose and list items to 80 columns where reasonable. Do not
  impose an 80-column limit on tables; make them as wide as needed for their
  content.
- Preserve the exact spelling of code identifiers, commands, API fields,
  product names, and quoted text.

## When to Use

- Making a significant architectural decision
- Choosing between competing approaches
- Adding or changing a public API
- Shipping a feature that changes user-facing behaviour
- Onboarding new team members (or agents) to the project
- When you find yourself explaining the same thing repeatedly

**When NOT to use:** Don't document obvious code. Don't add comments that
restate what the code already says. Don't write docs for throwaway prototypes.

Not every trigger above produces an ADR. Significant decisions go through the
ADR criteria below; API changes go in API documentation; shipped changes go in
the changelog.

## Architecture Decision Records (ADRs)

ADRs capture the reasoning behind decisions that will matter to future readers.
Follow the template rules under "ADR Format and Numbering". Do not substitute a
different template or a one-paragraph format.

### When to Write an ADR

Create an ADR only when all three are true:

- **Hard to reverse** — the cost of changing the decision later is meaningful.
- **Surprising without context** — a future reader would wonder why the choice
  was made.
- **A real trade-off** — there were genuine alternatives and specific reasons to
  choose one.

Common candidates include architectural shape and integration patterns;
technology choices with meaningful lock-in; data models and boundaries;
authentication and API architecture; build tools, hosting, and infrastructure;
deliberate deviations; and constraints not visible in code. These are prompts to
apply the three criteria, not automatic reasons to write an ADR. A public API
change or user-facing feature is not by itself an ADR trigger.

### ADR Format and Numbering

Store ADRs in the project's existing ADR directory. If there is none, use
`docs/adr/`. Use sequential four-digit numbering. Scan the directory for the
highest number and increment it; if there are no ADRs, start at `0001`. Use the
number in both filename and title (for example, `0012-some-decision.md` with
`# ADR 0012: Some decision`). Create the directory lazily when the first ADR is
needed.

Use the template in the ADR directory (`template.md`) when it exists.
Otherwise, use this canonical fallback:

```md
# ADR {number}: {title}

- **Status:** {proposed/accepted/deprecated/superseded}
- **Date:** {YYYY-MM-DD}
- **Authors:** {names}

## Context

{background and why the decision is needed}

## Decision

{what was decided and why}

## Alternatives considered

{options that were rejected, and why}

## Consequences

{implications, trade-offs, and follow-up actions}

## References

- {links to docs, issues, discussions}
```

Retain the chosen template's title, metadata, and core sections. For the
fallback, these are Status, Date, Authors, Context, Decision, Alternatives
considered, Consequences, and References. If project ADR examples exist, follow
their useful additions and level of detail without replacing the chosen
template.
Add supporting sections—such as risks, scenarios, or implementation
details—when they clarify the rationale or consequences; do not add detail just
to fill out a template.

### ADR Lifecycle

- Do not delete old ADRs; they preserve historical context.
- When a decision changes, write a new ADR that references and supersedes the
  old one. Update the old ADR's status as appropriate if the project uses one.

Use the status values specified by the chosen template. If a project template
includes a status field but does not specify values, follow existing project ADR
conventions; if there are none, use the fallback's values (`proposed`,
`accepted`, `deprecated`, or `superseded`).

## Inline Documentation

### When to Comment

Comment the *why*, not the *what*:

```typescript
// BAD: Restates the code
// Increment counter by 1
counter += 1;

// GOOD: Explains non-obvious intent
// Rate limit uses a sliding window — reset counter at window boundary,
// not on a fixed schedule, to prevent burst attacks at window edges
if (now - windowStart > WINDOW_SIZE_MS) {
  counter = 0;
  windowStart = now;
}
```

### When NOT to Comment

```typescript
// Don't comment self-explanatory code
function calculateTotal(items: CartItem[]): number {
  return items.reduce((sum, item) => sum + item.price * item.quantity, 0);
}

// Don't leave TODO comments for things you should just do now
// TODO: add error handling  ← Just add it

// Don't leave commented-out code
// const oldImplementation = () => { ... }  ← Delete it, git has history
```

### Document Known Gotchas

```typescript
/**
 * IMPORTANT: This function must be called before the first render.
 * If called after hydration, it causes a flash of unstyled content
 * because the theme context isn't available during SSR.
 *
 * See ADR 0003 for the full design rationale.
 */
export function initializeTheme(theme: Theme): void {
  // ...
}
```

## API Documentation

For public APIs, document them inline with types (TypeScript) or with an
OpenAPI specification (REST):

### Inline with Types (Preferred for TypeScript)

```typescript
/**
 * Creates a new task.
 *
 * @param input - Task creation data (title required, description optional)
 * @returns The created task with server-generated ID and timestamps
 * @throws {ValidationError} If title is empty or exceeds 200 characters
 * @throws {AuthenticationError} If the user is not authenticated
 *
 * @example
 * const task = await createTask({ title: 'Buy groceries' });
 * console.log(task.id); // "task_abc123"
 */
export async function createTask(input: CreateTaskInput): Promise<Task> {
  // ...
}
```

### OpenAPI / Swagger for REST APIs

```yaml
paths:
  /api/tasks:
    post:
      summary: Create a task
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/CreateTaskInput'
      responses:
        '201':
          description: Task created
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Task'
        '422':
          description: Validation error
```

## README Structure

Every project that is not a throwaway prototype should have a README that
covers:

```markdown
# Project Name

One-paragraph description of what this project does.

## Quick Start
1. Clone the repo
2. Install dependencies: `npm install`
3. Set up environment: `cp .env.example .env`
4. Run the dev server: `npm run dev`

## Commands
| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server |
| `npm test` | Run tests |
| `npm run build` | Production build |
| `npm run lint` | Run linter |

## Architecture
Brief overview of the project structure and key design decisions.
Link to ADRs for details.

## Contributing
How to contribute, coding standards, PR process.
```

## Changelog Maintenance

For shipped features and fixes, keep a changelog (for example, `CHANGELOG.md`):

```markdown
# Changelog

## [1.2.0] - 2025-01-20
### Added
- Task sharing: users can share tasks with team members (#123)
- Email notifications for task assignments (#124)

### Fixed
- Duplicate tasks appearing when rapidly clicking create button (#125)

### Changed
- Task list now loads 50 items per page (was 20) for better UX (#126)
```

## Documentation for Agents

Special consideration for AI agent context:

- **CLAUDE.md / rules files** — Document project conventions so agents follow
  them
- **Spec files** — Keep specs updated so agents build the right thing
- **ADRs** — Help agents understand why past decisions were made (prevents
  re-deciding)
- **Inline gotchas** — Prevent agents from falling into known traps

## Common Rationalisations

| Rationalisation | Reality |
|---|---|
| "The code is self-documenting" | Code shows what. It doesn't show why, what alternatives were rejected, or what constraints apply. |
| "We'll write docs when the API stabilises" | APIs stabilise faster when you document them. The doc is the first test of the design. |
| "Nobody reads docs" | Agents do. Future engineers do. Your 3-months-later self does. |
| "ADRs are overhead" | A 10-minute ADR prevents a 2-hour debate about the same decision six months later. |
| "Comments get outdated" | Comments on *why* are stable. Comments on *what* get outdated — that's why you only write the former. |

## Red Flags

- Public APIs with no documentation or types
- README that doesn't explain how to run the project
- Commented-out code instead of deletion
- TODO comments that have been there for weeks
- No ADRs for decisions that meet the ADR criteria
- Documentation that restates the code instead of explaining intent

## Verification

After documenting, check the following where relevant to the work:

- [ ] ADRs exist for decisions that meet the ADR criteria above
- [ ] The affected README covers the description, quick start, commands,
  architecture overview, and contributing guidance
- [ ] Affected API functions have parameter and return type documentation
- [ ] Affected known gotchas are documented inline where they matter
- [ ] No commented-out code remains in the changed code
- [ ] Affected rules files (CLAUDE.md etc.) are current and accurate
- [ ] Shipped user-facing changes are recorded in the changelog
