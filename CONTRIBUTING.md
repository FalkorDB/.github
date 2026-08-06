# Contributing to FalkorDB

Thanks for your interest in contributing! These guidelines apply to **all
repositories in the [FalkorDB organization](https://github.com/FalkorDB)** — the
FalkorDB graph database and every client library, tool and integration we
publish.

If the repository you are contributing to has its own `CONTRIBUTING.md`, that
file takes precedence over this one.

## Licensing of contributions

Licenses differ across our repositories (MIT, Apache-2.0, BSD-3-Clause,
AGPL-3.0 and SSPL are all in use). By contributing code in any form — a pull
request on GitHub, a patch by email, or a fragment posted in a public discussion
— you agree to release your contribution under the license of the repository it
is contributed to, as found in that repository's `LICENSE` file. Please check
that file before you start.

Do not add or change license headers unless the repository's existing sources
already carry them; in that case, follow the convention already used there.

## How to use GitHub issues

Issues should be used to report **bugs** and to file **detailed feature
requests**, on the repository the issue actually concerns. Everything else
belongs in the organization
[Discussions](https://github.com/orgs/FalkorDB/discussions).

Please do not open issues for general questions or usage help. We are happy to
help you in [Discussions](https://github.com/orgs/FalkorDB/discussions).

Issues and pull requests for the documentation site belong in the documentation
repository:

    https://github.com/FalkorDB/docs

If you are reporting a security bug or vulnerability, **do not open a public
issue** — see our
[security policy](https://github.com/FalkorDB/.github/blob/main/SECURITY.md).

## How to submit a change

1. Fork the repository on GitHub
   ([how to fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo)).
2. Create a topic branch: `git checkout -b my_branch`.
3. Make your change, and add or update tests where the repository has a test
   suite.
4. Build and run the tests locally — see the repository's `README.md` for the
   commands, since they differ per language and project.
5. Commit your work with a clear message: `git commit -am "Describe the change"`.
6. Push the branch to your fork: `git push origin my_branch`.
7. Open a pull request against the repository's default branch
   ([how to open a PR](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)).
8. Respond to review feedback. Once CI is green and the PR is approved, a
   maintainer will merge it.

For large or invasive changes, please open an issue or a discussion first so we
can agree on the approach before you invest time in the implementation.

## Code of conduct

All participation is governed by our
[Code of Conduct](https://github.com/FalkorDB/.github/blob/main/CODE_OF_CONDUCT.md).

Thanks!
