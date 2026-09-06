# cert-githubaction


on event : 

syntax : 


workflow dispatch is give facility to trigger manually. 

name: CI
on: workflow_dispatch

3 different ways to build action

1. Composite Actions -> YAML + JS (bash, PowerShell)
2. JavaScript Actions -> This is the default for actions
3. Docker Container Actions -> 

## GITHUB_TOKEN permissions reference

Each `permissions` scope controls access to a different part of the GitHub API for the `GITHUB_TOKEN`:

| Scope | Controls access to |
|---|---|
| `actions` | Workflow runs, artifacts, and workflow logs via the API (e.g. re-running a workflow, deleting an artifact, canceling a run) |
| `attestations` | Creating build/artifact attestations — the provenance records used for supply-chain security (e.g. `actions/attest-build-provenance`) |
| `checks` | The Checks API — creating/updating check runs and check suites (the status boxes shown on a commit/PR from CI systems, distinct from plain commit statuses) |
| `contents` | The repository's files, commits, branches, tags, releases. `read` lets you `checkout`; `write` lets you push commits, create tags/releases |
| `deployments` | Deployment objects and deployment statuses (used by deployment-tracking integrations, not the actual deploy itself) |
| `discussions` | GitHub Discussions — reading/creating/commenting on discussion threads |
| `id-token` | Requesting an OIDC token for the run. `write` lets the job mint a short-lived OIDC JWT to authenticate to cloud providers (AWS/Azure/GCP) without stored secrets. There's no meaningful "read", only `write` or `none` |
| `issues` | Issues — creating, commenting, labeling, closing |
| `models` | Access to GitHub Models (AI model inference API). Only `read` or `none` — no write concept since you're just calling a model |
| `packages` | GitHub Packages registry — `read` to pull, `write` to publish packages |
| `pages` | GitHub Pages deployments — building and deploying a Pages site |
| `pull-requests` | PRs — commenting, labeling, merging, requesting reviewers, editing (`read` lets you list/view PRs, `write` lets you edit them like `gh pr edit`) |
| `security-events` | Code scanning alerts (the Security tab) — used by `github/codeql-action` to upload SARIF results |
| `statuses` | Commit statuses — the simpler status API (different from `checks`; predates Checks, used by some legacy CI integrations) |

Everything except `id-token` and `models` accepts `read`, `write`, or `none`.

**Checks vs statuses:** `statuses` is the older, simpler "commit status" API (a single state + description per SHA, no detailed output). `checks` is the newer, richer Checks API that supports annotations, multiple check runs per commit, and the structured pass/fail UI you see from GitHub Actions and most modern CI tools. Use `statuses` for a simple custom status via API; use `checks` for rich, structured check results.

**Important behavioral trap:** as soon as a `permissions:` key is declared anywhere in the workflow (workflow-level or job-level), every scope not explicitly listed defaults to `none` — it does NOT inherit the repository's default `GITHUB_TOKEN` setting.

Full reference:
- [Use GITHUB_TOKEN for authentication in workflows](https://docs.github.com/en/actions/how-tos/writing-workflows/choosing-what-your-workflow-does/controlling-permissions-for-github_token)
- [Assigning permissions to jobs](https://docs.github.com/en/enterprise-cloud@latest/actions/using-jobs/assigning-permissions-to-jobs)
