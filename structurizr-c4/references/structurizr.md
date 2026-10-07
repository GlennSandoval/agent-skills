# Structurizr reference

Consult the authoritative pages for the construct being changed rather than guessing syntax. Use documentation matching the project's tool version when current examples differ from installed behavior.

- [C4 diagram types](https://c4model.com/diagrams): select the appropriate abstraction and supplementary diagram.
- [C4 review checklist](https://c4model.com/diagrams/checklist): titles, scope, boundaries, labels, and notation.
- [DSL language reference](https://docs.structurizr.com/dsl/language): grammar, permitted children, views, expressions, styles, and directives.
- [DSL basics](https://docs.structurizr.com/dsl/basics): tokenization and string substitution.
- [Identifiers](https://docs.structurizr.com/dsl/identifiers): identifier scope and hierarchical references.
- [Implied relationships](https://docs.structurizr.com/dsl/cookbook/implied-relationships/): behavior when dependencies roll up through model levels.
- [Validation](https://docs.structurizr.com/validate): parser validation command.
- [Export](https://docs.structurizr.com/export): supported formats and options.

## Version-aware tooling

Prefer a project wrapper or pinned CI tool over a global executable. Inspect its help and version before adapting commands. Current unified tooling and older standalone CLI distributions can have different launchers and capabilities; do not migrate them as a side effect of a diagram edit.

The documented validation arguments are:

```text
<project Structurizr launcher> validate -workspace <path/to/workspace.dsl>
```

For an existing standalone CLI installation whose launcher is `structurizr.sh`, an example is:

```sh
structurizr.sh validate -workspace docs/architecture/workspace.dsl
```

The executable name and workspace path are project-specific. Supply an actual discovered launcher when reporting a runnable command. Avoid inventing Docker image tags or assuming a daemon is available. Reuse pinned images if the project already uses them. If tooling must be installed, follow current official installation documentation and applicable environment permissions.

Successful parsing establishes syntax and model constraints, not diagram readability or correspondence with the code. Architecture inspections, if supported, are additional feedback rather than a substitute for either check.

## Advanced view checks

- Dynamic views should describe a bounded scenario using relationships supported by the static model. Verify ordering and direction; do not invent new dependencies only to complete a story.
- Deployment views should instantiate existing systems or containers in named environments. Verify runtime replicas and infrastructure against deployment evidence rather than extrapolating from the logical model.
- Filtered views depend on their base view. Check both the base selection and tag filters when elements vanish unexpectedly.
- Review the expanded entry workspace after changes to includes; checking only an included fragment can miss scope and ordering failures.
- Keep manually maintained layout or workspace JSON when the project uses it; regenerate derived exports through its established workflow.
- Exporters can lose styling or view features. Inspect the requested output format rather than assuming it matches the native Structurizr renderer.
