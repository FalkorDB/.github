# FalkorDB/.github

Organization-wide defaults and shared automation for every repository in the
[FalkorDB](https://github.com/FalkorDB) GitHub organization.

> Looking for FalkorDB itself? Head to [FalkorDB/FalkorDB](https://github.com/FalkorDB/FalkorDB),
> the [docs](https://docs.falkordb.com), or [www.falkordb.com](https://www.falkordb.com).

## What's in this repository

| Path | Purpose |
| ---- | ------- |
| [`profile/README.md`](profile/README.md) | The page shown on the [organization profile](https://github.com/FalkorDB). |
| [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) | Default Code of Conduct ([Contributor Covenant 2.1](https://www.contributor-covenant.org/version/2/1/code_of_conduct/)). |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Default contribution guidelines: licensing, issues vs. Discussions, PR flow. |
| [`SECURITY.md`](SECURITY.md) | Default security policy and vulnerability reporting process. |
| [`.github/workflows/report-scheduled-failure.yml`](.github/workflows/report-scheduled-failure.yml) | Reusable workflow that reports failing nightly runs against `falkordb/falkordb:edge`. |
| [`.github/workflows/release-notes.yml`](.github/workflows/release-notes.yml) | Reusable workflow that rewrites a release's auto-generated notes into user-facing ones. Its scripts live in [`.github/scripts/release-notes/`](.github/scripts/release-notes). |

## Default community health files

GitHub uses the `CODE_OF_CONDUCT.md`, `CONTRIBUTING.md` and `SECURITY.md` in this
repository for any FalkorDB repository that doesn't have its own copy (in its root,
`docs/` or `.github/` folder). A repository's own file always takes precedence.

Because these files apply to every repository at once, keep them generic: anything
specific to one project belongs in that project's own repository.

## Reusable workflows

### `report-scheduled-failure`

A cron-triggered workflow has nobody watching it, so a failing nightly run can go
unnoticed. This workflow posts the failure to the drivers team's Google Chat, or,
if no webhook is configured, opens (and then comments on) a single tracking issue
labelled `nightly-edge-failure` in the calling repository.

Call it from the workflow that runs against `falkordb/falkordb:edge`:

```yaml
report-scheduled-failure:
  name: Report scheduled failure
  needs: [build]  # every job the run should be considered failed for
  if: ${{ always() && github.event_name == 'schedule' && contains(needs.*.result, 'failure') }}
  permissions:
    issues: write  # required: a called workflow can only downgrade permissions
  uses: FalkorDB/.github/.github/workflows/report-scheduled-failure.yml@<full commit sha>
  secrets:
    DRIVERS_GOOGLE_CHAT_WEBHOOK_URL: ${{ secrets.DRIVERS_GOOGLE_CHAT_WEBHOOK_URL }}
```

| Name | Kind | Required | Description |
| ---- | ---- | -------- | ----------- |
| `issue-title` | input | no | Title of the tracking issue. Defaults to `CI is failing against falkordb/falkordb:edge`; keep it stable per repository. |
| `DRIVERS_GOOGLE_CHAT_WEBHOOK_URL` | secret | no | Google Chat incoming webhook. When unset, the tracking-issue fallback is used. |

**Pin to a full commit SHA, not a branch.** Passing secrets to a mutable ref would let
any later change here run with the caller's secrets. Dependabot's `github-actions`
ecosystem keeps `uses:` pins up to date in repositories where it is enabled.

### `release-notes`

GitHub's auto-generated release notes list PR titles, most of which mean little to
users. When a release is published, this workflow rewrites them with an Azure OpenAI
model:

- It drops changes users don't notice, such as dependency bumps, CI and refactors.
- It writes one plain sentence per remaining change, under features, improvements,
  fixes, security and deployment.
- It keeps GitHub's original notes collapsed at the bottom.

Reruns start again from those originals, so running it twice never rewrites the
rewrite.

Call it from a workflow of its own, so the repository also gets a manual **Run
workflow** button for one tag, a range of tags, or a dry run that only prints the
result. The header of [`release-notes.yml`](.github/workflows/release-notes.yml) has
the full caller to copy, including those manual inputs; its core is:

```yaml
jobs:
  polish:
    permissions:
      contents: write       # edit the release
      pull-requests: read   # read the PRs it lists
      id-token: write       # find this workflow's commit, to run its scripts
    uses: FalkorDB/.github/.github/workflows/release-notes.yml@<full commit sha>
    with:
      product: FalkorDB Python client
      product-description: the Python library for FalkorDB graph databases
      tag: ${{ inputs.tag }}
      from-tag: ${{ inputs.from_tag }}
      dry-run: ${{ inputs.dry_run || false }}
    secrets:
      OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
```

| Name | Kind | Required | Description |
| ---- | ---- | -------- | ----------- |
| `product` | input | yes | The product's name as the notes should call it. |
| `product-description` | input | no | One phrase on what the product is, for the model's context. |
| `whats-new` | input | no | Lead the notes with a short `## What's New` section. Only for a product that shows it to users after they upgrade, as FalkorDB Browser does. Defaults to `false`. |
| `tag` | input | no | Release tag to rewrite, or the newest one of a range. Empty on a release event. |
| `from-tag` | input | no | Oldest tag of a range; every published release from it through `tag` is rewritten. |
| `dry-run` | input | no | Print the new notes without updating the release. |
| `OPENAI_API_KEY` | secret | yes | Key for the Azure OpenAI resource. |
| `AZURE_OPENAI_ENDPOINT` | variable | yes | The resource URL, e.g. `https://my-resource.openai.azure.com`. Set on the organization or the calling repository. |
| `AZURE_OPENAI_DEPLOYMENT` | variable | no | The model deployment name. Defaults to `gpt-6-luna`. |

A section between `<!-- release-downloads:start -->` and `<!-- release-downloads:end -->`
lines is never shown to the model and is put back unchanged. FalkorDB Browser keeps its
download links there.

Before relying on it, run it by hand with **dry-run** on to check the output.

## Contributing

Changes to this repository affect the whole organization, so please open a pull
request rather than pushing to `main`. See [CONTRIBUTING.md](CONTRIBUTING.md) for
the general process, and report security issues privately as described in
[SECURITY.md](SECURITY.md).

## Community

- [Discord](https://discord.gg/6M4QwDXn2w)
- [GitHub Discussions](https://github.com/orgs/FalkorDB/discussions)
- [FalkorDB Cloud](https://app.falkordb.cloud)
