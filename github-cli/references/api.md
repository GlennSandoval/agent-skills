# GitHub API through gh

Use built-in commands when they meet the task requirements. Use API calls for missing data, complete pagination, or precise authorized updates.

## Target and method

`gh api` accepts REST paths or `graphql`. For an Enterprise host, set `--hostname`.

If the checkout context is unclear, specify the owner and repository in the endpoint. Quoted `{owner}` and `{repo}` placeholders use the current repository or `GH_REPO`.

The `-f` and `-F` field flags change the default REST method from GET to POST. For read queries with parameters, explicitly set `--method GET`:

```sh
gh api --method GET "repos/$repo/pulls" \
  -f state=open -F per_page=100 --paginate \
  --jq '.[] | {number, title, html_url}'
```

The `-f` flag sends strings. The `-F` flag converts booleans, integers, null, and supported placeholders. It reads values with an `@` prefix from files.

For a prepared JSON body, use `--input "$payload_file"`. With `--input`, field flags become URL query parameters.

For writes, also specify the intended method. A GraphQL HTTP POST can contain a read query or a mutation. Inspect the GraphQL operation to determine whether it changes data.

## Pagination and response structure

REST `--paginate` follows pagination links. Each page remains a separate JSON value. To collect the pages in an outer array, add `--slurp`.

Flatten only the collection you requested. Array endpoints and objects with `items` have different response structures. Search APIs have separate result limits. Pagination does not remove those limits.

For GraphQL pagination:

1. Declare `$endCursor: String` as a query variable.
2. Use `after: $endCursor` in the connection.
3. Select `pageInfo { hasNextPage endCursor }`.

Plan pagination separately for each nested connection. The first 100 threads do not necessarily include all threads or replies.

Pass GraphQL source as a safely quoted string. Alternatively, read it from a file with `-F query=@PATH`. Use GraphQL variables for user values. Do not insert user values directly into query text.

Inspect GraphQL `errors` and `data`. Partial data does not prove that the complete operation succeeded.

## PR discussion details

```sh
# Conversation comments, inline review comments, and submitted reviews differ.
gh api --method GET "repos/$repo/issues/$pr/comments" --paginate
gh api --method GET "repos/$repo/pulls/$pr/comments" --paginate
gh api --method GET "repos/$repo/pulls/$pr/reviews" --paginate
```

If thread grouping, resolution status, or reply relationships matter, use GraphQL `repository.pullRequest.reviewThreads`. Select only the required fields. Paginate threads and comments as necessary.

Before an inline review submission, verify these values against the current PR diff:

1. The current head commit.
2. The file path.
3. The diff side.
4. The diff line.

Do not guess line positions from an old checkout.

## Failures

Read the error message and response status. A 403 can indicate missing permissions, organization policy, or rate limits. A 404 can hide a private resource.

Use the applicable response headers to check rate limits. Follow the reset or retry timing. Do not print complete request or response traces or credential environment variables.

If a mutation has an unclear result, query the affected state before you retry. If the operation completed only in part, report that result. Do not create a duplicate object or comment.

Details: [gh api manual](https://cli.github.com/manual/gh_api), [REST pagination](https://docs.github.com/en/rest/using-the-rest-api/using-pagination-in-the-rest-api), and [GraphQL pagination](https://docs.github.com/en/graphql/guides/using-pagination-in-the-graphql-api).
