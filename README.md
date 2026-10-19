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

## Contributing

Changes to this repository affect the whole organization, so please open a pull
request rather than pushing to `main`. See [CONTRIBUTING.md](CONTRIBUTING.md) for
the general process, and report security issues privately as described in
[SECURITY.md](SECURITY.md).

## Community

- [Discord](https://discord.gg/6M4QwDXn2w)
- [GitHub Discussions](https://github.com/orgs/FalkorDB/discussions)
- [FalkorDB Cloud](https://app.falkordb.cloud)
