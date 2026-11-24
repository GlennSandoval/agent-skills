---
name: documentation
description: Writes and maintains project documentation. Use when changing public APIs, shipping features, writing READMEs or inline documentation, or when you need to record context that future engineers and agents will need to understand the codebase.
---

# Documentation

## Overview

Document decisions, not just code. The most valuable documentation captures the
*why*—the context, constraints, and trade-offs that led to a decision. Code
shows *what* was built; documentation explains *why it was built this way* and
*what alternatives were considered*. This context is essential for future
humans and agents working in the codebase. See
[Record decisions](#record-decisions) for when and where to record them.

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
  product names, quoted text, and names fixed by external APIs, libraries,
  protocols, or file formats, such as `Cache-Control`, `setUTCHours`, or
  `color` in CSS and Mermaid.

## When to use

- Adding or changing a public API
- Shipping a feature that changes user-facing behaviour
- Onboarding new team members or agents to the project
- Explaining the same thing repeatedly

## When not to use

- Documenting obvious code
- Adding comments that restate what the code already says
- Writing documentation for throwaway prototypes

## Record decisions

Record a decision when a future reader could reasonably ask "why was it done
this way?" and the code cannot answer. Examples include choosing a library or
pattern, accepting a known limitation, or rejecting an obvious alternative.

### Where to record decisions

Follow the repository's existing convention. Look for decision records, design
documents, RFCs, or an architecture section in the README or rules files. Use
the same location, format, and numbering.

If the repository has no convention:

1. Do not create a new decision-record system without agreement.
2. Put the rationale as close as possible to what it explains: an inline
   comment for a local decision, or the README architecture section for a
   project-wide decision.
3. Include the rationale in the pull request description or commit message.

### What to include

Whatever the format, a decision record states the following:

- The context and constraints that applied
- The decision
- The alternatives considered and why they were rejected
- The consequences, including known limitations

When a decision changes, record the new decision and link it to the old one.
Do not silently rewrite the original rationale.

## Inline documentation

### When to comment

In implementation comments, explain the *why*, not the *what*. Public API
documentation is the exception; see [API documentation](#api-documentation).

```typescript
// BAD: Restates the code
// Increment counter by 1
counter += 1;

// GOOD: Explains a trade-off the code cannot show
// Fixed-window limit: a client can send up to twice the limit across a
// window boundary. Accepted because this limit stops runaway retry loops,
// not abuse; abuse protection is handled upstream.
if (now - windowStart > WINDOW_SIZE_MS) {
  counter = 0;
  windowStart = now;
}
```

### When not to comment

Don't comment self-explanatory code, leave TODO comments for work you can do
now, or leave commented-out code:

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

### Document known gotchas

Document constraints that a reader can't infer from the code, next to the code
they affect:

```typescript
/**
 * IMPORTANT: Pass the raw request body, not parsed JSON. The sender signs
 * the exact bytes it sends. Re-serialising parsed JSON can change key order
 * or whitespace, so valid signatures fail verification.
 */
export function verifyWebhookSignature(rawBody: Buffer, signature: string): boolean {
  // ...
}
```

## API documentation

API documentation describes the contract: what callers pass, what they get
back, what can fail, and any side effects. This is *what* documentation, and it
is the exception to commenting only the *why*, because a signature cannot
express the full contract. Describe what callers can rely on, not how the
function works internally, and don't restate the function name.

Record public API changes in the API documentation.

Document public APIs inline with types for TypeScript, or with an OpenAPI
specification for REST APIs. The following sections show an example of each.

### Inline with types (preferred for TypeScript)

The following example documents a TypeScript function with TSDoc:

```typescript
/**
 * Creates a task owned by the authenticated user.
 *
 * @param input - Task creation data (title required, description optional)
 * @returns The created task with server-generated ID and timestamps
 * @throws {@link ValidationError}
 * Thrown if the title is empty or exceeds 200 characters.
 *
 * @throws {@link AuthenticationError}
 * Thrown if the user is not authenticated.
 *
 * @example
 * ```ts
 * const task = await createTask({ title: 'Buy groceries' });
 * console.log(task.id); // "task_abc123"
 * ```
 */
export async function createTask(input: CreateTaskInput): Promise<Task> {
  // ...
}
```

### OpenAPI for REST APIs

The following example documents a REST endpoint with OpenAPI:

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
        '401':
          description: User is not authenticated
        '422':
          description: Validation error
```

## README structure

Every project that is not a throwaway prototype needs a README that covers the
following:

```markdown
# Project name

One-paragraph description of what this project does.

## Quick start

1. Clone the repository.
2. Install dependencies: `npm install`
3. Set up the environment: `cp .env.example .env`
4. Run the development server: `npm run dev`

## Commands

| Command | Description |
|---------|-------------|
| `npm run dev` | Start the development server |
| `npm test` | Run tests |
| `npm run build` | Create a production build |
| `npm run lint` | Run the linter |

## Architecture

Brief overview of the project structure and key design decisions.
Link to the project's decision records or design documentation, if any.

## Contributing

How to contribute, coding standards, and the pull request process.
```

## Documentation for agents

Maintain the following documentation so that AI agents have the context they
need:

- **Rules files, such as CLAUDE.md:** Document project conventions so agents
  follow them, including where the repository records decisions.
- **Spec files:** Keep specs updated so agents build the right thing.
- **Inline gotchas:** Prevent agents from falling into known traps.

## Common rationalisations

| Rationalisation | Reality |
|---|---|
| "The code is self-documenting" | Code shows what. It doesn't show why, what alternatives were rejected, or what constraints apply. |
| "We'll write docs when the API stabilises" | Writing the documentation is how you find what is still unstable. A behaviour that is hard to explain, or an error case you can't describe, is a design problem, and it costs least to fix before callers depend on it. Documentation also states what callers can rely on. Without it, callers depend on whatever behaviour they observe. If the API is still changing, document it now and mark it as unstable. |
| "Nobody reads docs" | Agents do. Future engineers do. Your three-months-later self does. |
| "Comments get outdated" | Comments that restate the code go stale with every edit, so don't write them. Comments that explain *why* change only when the reasoning changes. API documentation changes only when the contract changes. |

## Red flags

- Public APIs with no documentation or types
- A README that doesn't explain how to run the project
- Commented-out code instead of deletion
- TODO comments that have been there for weeks
- Documentation that restates the code instead of explaining intent

## Verification

After documenting, check the following where relevant to the work:

- [ ] The affected README covers the description, quick start, commands,
  architecture overview, and contributing guidance.
- [ ] Affected public APIs describe parameters and return values beyond what
  their type signatures convey.
- [ ] Affected known gotchas are documented inline where they matter.
- [ ] No commented-out code remains in the changed code.
- [ ] Affected rules files, such as CLAUDE.md, are current and accurate.
- [ ] Significant decisions are recorded in the repository's usual location,
  with alternatives and consequences.
