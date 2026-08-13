# SubmitMap MCP server

A remote MCP server for [SubmitMap](https://submitmap.com), a directory of
product launch platforms and startup directories.

Every platform in the directory is a typed record rather than a link: who it
accepts, what disqualifies you, the exact submission steps, the expected
approval time, and whether the backlink is dofollow. The data is hand-walked,
not scraped.

This repository holds the registry metadata. The server itself is hosted, so
there is no package to install and nothing to run locally.

## Endpoint

```
https://submitmap.com/api/mcp
```

Transport: streamable HTTP. Protocol version: `2025-06-18`.

## Configuration

```json
{
  "mcpServers": {
    "submitmap": {
      "type": "http",
      "url": "https://submitmap.com/api/mcp"
    }
  }
}
```

Per-client setup, including the OAuth flow, is documented at
<https://submitmap.com/docs/>.

## Tools

Read-only, and usable with no account at all:

- **`search_platforms`** — Search the directory. Filter by query, category,
  pricing, link type, backlink requirement or approval speed.
- **`get_platform`** — The full record for one platform: eligibility,
  disqualifiers, submission steps, requirements, gotchas and expected outcome.
- **`qualify_project`** — Describe a product inline and get back which
  platforms it qualifies for now, which are reachable once something is
  supplied (with the exact list of what is missing), and which are out of
  reach.

With an account token, for automating submissions:

- **`whoami`** — Which account the token belongs to and what is left of the
  free tier.
- **`create_project`**, **`update_project`**, **`list_projects`** — Store a
  product and the pack a submission form asks for.
- **`submission_playbook`** — Everything needed to submit one project to one
  platform in the maker's own browser: a preflight of what is missing, the
  sign-in rule, the pack values mapped onto that form's fields, the steps and
  the gotchas.
- **`plan_submissions`** — Write the run order for a project.
- **`record_submission`**, **`list_submissions`** — Log what was sent and
  track where each one stands.

## Authentication

The three read tools need nothing. The account tools accept
`Authorization: Bearer smap_...`, and the server also advertises OAuth via
`/.well-known/oauth-protected-resource`.

Tokens are created at <https://submitmap.com/app/tokens>.

## Links

- Directory: <https://submitmap.com>
- Docs: <https://submitmap.com/docs/>
- Agent guide: <https://submitmap.com/for-agents/>
- Server card: <https://submitmap.com/.well-known/mcp/server-card.json>
