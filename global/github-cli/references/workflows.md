# Common GitHub workflows

The examples use shell variables `repo`, `pr`, `issue`, and `run_id`.

1. Set `repo` to the confirmed repository.
2. Set the object variables to the confirmed identifiers.
3. Set other variables to the values required for the selected command.

Execute only the commands that the task requires.

## Pull requests

Inspect a specific PR with explicit fields:

```sh
gh pr view "$pr" --repo "$repo" \
  --json number,url,title,body,state,isDraft,baseRefName,headRefName,headRefOid,headRepositoryOwner,reviewDecision,mergeStateStatus,statusCheckRollup
gh pr diff "$pr" --repo "$repo"
gh pr view "$pr" --repo "$repo" --comments
gh pr checks "$pr" --repo "$repo" --json name,state,bucket,link
```

`--comments` shows conversation comments. It does not show all inline review threads. For inline review comments, use the REST review-comments endpoint. For thread resolution and replies, use GraphQL. See [api.md](api.md).

Before `gh pr checkout`, inspect `git status --short`. Preserve uncommitted work. If you do not need a checkout, use `gh pr diff`. Run repository checks that apply to the change. Do not execute unfamiliar code only to inspect a PR.

Before PR creation:

1. Verify the actual branch diff.
2. Verify the intended base branch.
3. Verify the remote head branch.
4. Inspect the repository PR templates.
5. Include the applicable required fields.
6. Check for an existing PR with the same head and base.

```sh
gh pr list --repo "$repo" --head "$head" --base "$base" --state open \
  --json number,url,headRefName,baseRefName
```

For a fork branch, also verify the head repository. Different repositories can use the same branch name.

Write a description of the change and validation. Then create the requested draft or ready PR:

```sh
gh pr create --repo "$repo" --base "$base" --head "$head" \
  --title "$title" --body-file "$body_file" --draft
```

If the user requests a draft PR, use `--draft`. If the user requests a ready PR, omit `--draft`.

An explicit `--head` prevents automatic push or fork prompts. First, make sure the branch exists in the intended remote repository. For a supported fork head, use `USER:BRANCH`.

`gh pr create --dry-run` can still push Git changes. If a preview must have no remote effects, prepare the body locally. Inspect the local body before PR creation.

Update a description or post a comment only when the user requests it:

```sh
gh pr edit "$pr" --repo "$repo" --title "$title" --body-file "$body_file"
gh pr comment "$pr" --repo "$repo" --body-file "$comment_file"
```

A request to review code does not necessarily authorize a GitHub review submission. If submission is authorized, select the requested action: `--comment`, `--approve`, or `--request-changes`. Use `--body-file` for the review body. Do not infer approval from successful CI checks.

Immediately before an authorized merge:

1. Read the PR's current head SHA.
2. Check the required checks.
3. Check the review decision.
4. Check the merge state.

Follow the repository policy and intended merge method. Use `--match-head-commit "$head_sha"` to prevent a merge if the head changes after inspection.

If the head SHA does not match, inspect the PR again. Do not only replace the SHA and retry. Use `--admin`, `--auto`, or `--delete-branch` only when the user authorizes that behavior.

A merge queue can queue a PR instead of immediately merging it. Verify the resulting state.

## Issues

For a search, specify the state and result limit:

```sh
gh issue list --repo "$repo" --state open --limit 50 \
  --json number,title,labels,url
gh issue view "$issue" --repo "$repo" \
  --json number,title,body,state,labels,assignees,url
gh issue view "$issue" --repo "$repo" --comments
```

Before you change an issue, read the issue and applicable discussion. Before issue creation, inspect the issue templates. For authorized writes:

```sh
gh issue create --repo "$repo" --title "$title" --body-file "$body_file"
gh issue comment "$issue" --repo "$repo" --body-file "$comment_file"
```

Before you close, reopen, assign, or label an issue, check its current state. Use the command help to confirm supported edit flags. After a failure with an unclear result, check for existing issues or comments before you retry.

## GitHub Actions and checks

Start with the PR's checks or a list of runs for the applicable branch. Match `headSha` to the commit under investigation:

```sh
gh run list --repo "$repo" --branch "$branch" --limit 20 \
  --json databaseId,headSha,status,conclusion,workflowName,event,url
gh run view "$run_id" --repo "$repo" \
  --json headSha,status,conclusion,jobs,url
gh run view "$run_id" --repo "$repo" --log-failed
```

The newest branch run can relate to a different commit, workflow, or event. External services can provide PR checks without an Actions run. If necessary, use the check URL to inspect those checks.

For `gh pr checks`, exit code 8 means that checks are pending. For other nonzero results, inspect the output and the command's exit code definitions. A run without a conclusion can still be active. An absent conclusion does not indicate success.

Get the failed-step logs first. If necessary, get individual job logs or the full logs. Identify the failed job and relevant error evidence. Explain whether code, configuration, or infrastructure caused the failure. Logs can contain sensitive data. Quote only the relevant excerpts.

Reruns, cancellations, and workflow dispatches change remote state. They can also execute deployment jobs. Execute these actions only within the user's authorized scope.

Before an authorized action:

1. Select the exact run, attempt, or workflow that the action requires.
2. Confirm the ref and inputs if the action uses them.

Do not automatically rerun CI instead of investigating a failure. Limit status checks or watch commands to the available time budget. If you have not observed completion, report the pending state.
