---
name: structurizr-c4
description: Create, update, and review C4 architecture models and diagrams using Structurizr DSL. Use for workspace.dsl files, architecture discovery from code, and Structurizr validation or exports.
---

# Structurizr C4

Produce a coherent architecture model with focused views that answer the user's architectural question. Prefer Structurizr DSL as the editable source; preserve an existing Java or JSON authoring workflow when that is the project's source of truth.

## Discover before modeling or reviewing

- Read repository instructions and find existing workspaces, included DSL files, architecture documentation, ADRs, build wrappers, and CI validation commands. Follow existing paths, naming, styling, and supported tool versions.
- For review-only requests, do not change the model unless asked; inspect the existing views and their source of truth.
- Establish whether the request describes current architecture or a proposed design. Do not present proposals as implemented behavior.
- For code-derived models, inspect entry points, independently running applications, persistence, external integrations, and deployment configuration. Ground important elements and relationships in concrete files or documentation. Summarize uncertain boundaries as assumptions; ask only when they materially affect the result.
- Choose the smallest useful set of views. A request for C4 does not require all four levels.

## Model the architecture

- Separate people, software systems, containers, and components. A C4 container is an application or data store, not necessarily a Docker container. Components describe responsibilities inside one container; folders and classes are not automatically components.
- Use context views for the system's users and external dependencies; container views for its applications and stores; component views only when internal responsibilities need explanation. Use dynamic views for a specific interaction and deployment views for runtime placement.
- Define elements once in the model and reuse them across views. Keep deployment infrastructure and instances separate from the logical model. Distinguish environments explicitly.
- Give elements meaningful names and concise responsibility descriptions. Add technologies when supported by evidence and useful at that level.
- Make relationships directional and specific: who calls, publishes, reads, or writes what. Identify protocols where known. Avoid ambiguous labels such as “uses” when a more informative label is available.
- Review implied relationships when adding lower-level dependencies. With Structurizr's default strategy, the first lower-level relationship can determine the parent-level description; inspect rolled-up labels and summarize explicitly when misleading rather than adding redundant parent relationships indiscriminately.

## Author and evolve DSL

- Preserve element identifiers, explicit view keys, includes, and manual layout choices during edits. Renaming identifiers or view keys can disrupt references or layout continuity; do it only when needed and explain the impact.
- Keep one canonical model. Split files with `!include` only when it improves ownership or readability; resolve include paths relative to their containing DSL files.
- Add explicit, stable view keys for new views. Start new layouts with `autoLayout` unless the project has another convention. Keep inclusion rules focused on the question the diagram answers.
- Use tags and styles consistently to communicate meaning. Do not copy renderer-specific styling into another format without checking support.
- Read [references/structurizr.md](references/structurizr.md) for syntax sources, advanced view considerations, and validation commands. Check the project's installed version before introducing newer DSL features.

## Verify and deliver

1. Run the repository's existing validation command against the entry workspace, including its dependencies. Otherwise use an available Structurizr parser/validator following the reference. Fix errors introduced by the change and rerun.
2. Review semantics independently of syntax: boundaries, relationship direction, view scope, evidence, and consistency across levels. Parsing cannot establish architectural accuracy.
3. When a renderer is available, inspect the affected views for readable labels, overlap, unexpected implied edges, missing context, clear scope and boundaries, and an understandable key for element types and styling. If the user requests exports, verify the exported result in that format.
4. If tooling is unavailable, identify the source workspace and label any unperformed parser validation or visual inspection. Give an executable validation command only for a discovered project launcher. Otherwise show only the placeholder syntax from the reference (`<project Structurizr launcher> validate -workspace <entry workspace>`), state what must be installed, and do not substitute a guessed executable name. Do not claim success from text inspection alone.
5. For edits, report changed files, the architectural change, validation results, and material assumptions. For review-only requests, report prioritized findings with the affected view or element, evidence, impact, and a concrete correction; report verification limits even when no findings are found. Update relevant documentation only within the requested scope.

Treat includes, scripts, plugins, and remote themes as potential execution or network dependencies when handling unfamiliar workspaces. Inspect them before parsing. Use local tooling for confidential architecture; publishing or uploading a workspace requires authorization for that destination.
