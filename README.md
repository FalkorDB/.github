# FalkorDB/.github

Organization-wide defaults and shared CI for the [FalkorDB](https://github.com/FalkorDB) repositories.

## What lives here

| Path | What it does |
| --- | --- |
| [`profile/README.md`](profile/README.md) | The public overview shown on [github.com/FalkorDB](https://github.com/FalkorDB). |
| [`CONTRIBUTING.md`](CONTRIBUTING.md), [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md), [`SECURITY.md`](SECURITY.md) | Default community files. GitHub shows them in every FalkorDB repository that has no file of its own. |
| [`.github/workflows/`](.github/workflows) | Reusable workflows that FalkorDB repositories call, so a fix lands once instead of in every copy. |

## Shared workflows

| Workflow | What it does | Used by |
| --- | --- | --- |
| [`release-notes.yml`](.github/workflows/release-notes.yml) | Rewrites a release's auto-generated notes into user-facing ones with an Azure OpenAI model, on publish or by hand. | falkordb-browser |
| [`report-scheduled-failure.yml`](.github/workflows/report-scheduled-failure.yml) | Reports a failed nightly run against `falkordb/falkordb:edge` to Google Chat, or to a tracking issue. | The client libraries |

Each workflow's header comment has the full caller to copy, its inputs and the permissions it needs.

### Polish release notes

When a release is published, the workflow rewrites GitHub's generated notes:

- It drops changes users don't notice, such as dependency bumps, CI and refactors.
- It writes one plain sentence per change, grouped under features, improvements, fixes, security and deployment.
- It keeps GitHub's original notes collapsed at the bottom.

Reruns start again from those originals. Your repository also gets a manual **Run workflow** button, for one tag, a range of tags, or a dry run that only prints the result.

**To add it to a repository:**

1. Copy the caller from the header of [`release-notes.yml`](.github/workflows/release-notes.yml) into `.github/workflows/release-notes.yml` in your repository.
2. Set `product` to the name your users know the product by. Optionally set `product-description` to one phrase on what it is.
3. Turn on `whats-new: true` only if your product reads a `## What's New` section from the release notes, as FalkorDB Browser does.
4. Run it by hand with **dry_run** on, to check the output before the next release.

It needs these on the organization or on the calling repository:

| Name | Kind | Value |
| --- | --- | --- |
| `OPENAI_API_KEY` | Secret | Key for the Azure OpenAI resource |
| `AZURE_OPENAI_ENDPOINT` | Variable | The resource URL, e.g. `https://my-resource.openai.azure.com` |
| `AZURE_OPENAI_DEPLOYMENT` | Variable, optional | The model deployment name; defaults to `gpt-6-luna` |

To keep a section of your own in the notes that the model must not touch (FalkorDB Browser keeps its download links this way), put it between `<!-- release-downloads:start -->` and `<!-- release-downloads:end -->` lines. The workflow leaves it out of the model's input and puts it back unchanged.

### Report scheduled failure

Add it as the last job of a workflow that runs on a schedule. When the run fails, it posts to the drivers team's Google Chat. Without the `DRIVERS_GOOGLE_CHAT_WEBHOOK_URL` secret, it opens or updates one tracking issue instead. See the header of [`report-scheduled-failure.yml`](.github/workflows/report-scheduled-failure.yml) for the job to copy.

## Calling a shared workflow

```yaml
uses: FalkorDB/.github/.github/workflows/<name>.yml@<ref>
```

- **A full commit SHA** is the safer choice. Dependabot's `github-actions` updates keep it current where they're enabled.
- **`@main`** picks up every change merged here on the next run, with no PR in your repository.

A shared workflow runs with the secrets and token permissions your caller gives it. So a change merged here reaches every repository that follows `main`. Review changes to this repository with that in mind.

A called workflow can only keep or narrow the permissions its caller grants. If a run fails with a permissions error, compare the caller's `permissions:` with the list in the workflow's header.

## Adding a shared workflow

1. Add it under `.github/workflows/` with `on: workflow_call`, and declare its inputs and secrets.
2. Start the file with a header comment that explains what it does and gives the caller to copy, as the existing ones do.
3. If it needs scripts, keep them under `.github/scripts/<workflow>/`. Check them out at the workflow's own commit, as `release-notes.yml` does. The `github` context belongs to the caller, so a plain checkout gets the caller's repository instead.
4. Add it to the table above.
