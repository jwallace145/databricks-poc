# Contributing

This repository holds one file that matters, [`jwall-engineering-sites.yaml`](jwall-engineering-sites.yaml):
what this Databricks workspace project asks for. [jwall-engineering-infra](https://github.com/jwallace145/jwall-engineering-infra)
provisions the workspace from it. Everything else here is tooling for the rules below.

## Setup

```sh
npm ci                                                          # commitlint
pre-commit install --hook-type commit-msg --hook-type pre-commit
```

The hooks are a convenience. CI is the authoritative check.

## Commit messages

Every commit is a **single-line** [Conventional Commit](https://www.conventionalcommits.org/)
of at most 100 characters. Details go in the pull request description, never in a commit body.

- Format: `type(scope)?: subject`, with an imperative, lowercase subject and no trailing period.
- The only thing allowed after the header is a blank line followed by
  `Co-authored-by: Name <email>` trailers.
- Types: `feat`, `fix`, `docs`, `chore`, `refactor`, `ci`, `build`, `perf`, `style`, `test`, `revert`.
- A breaking change is marked with `!`, as in `feat!: drop a compute policy`.
- The type drives the next version: `feat` bumps the minor version, `fix` the patch,
  and `!` the major (the minor while the version is below 1.0).

| Message | Valid |
| --- | --- |
| `feat: add a workspace user` | Yes |
| `fix: correct a policy name` + blank line + `Co-authored-by: Claude <noreply@anthropic.com>` | Yes |
| `feat: add thing` + blank line + `This adds the thing because…` | No, body text |
| `Added thing` | No, not conventional |

CI lints every commit in the pull request, and the pull request title separately.

## Pull requests

Every change reaches `main` through a pull request. Nobody pushes to `main`.

- The title is a valid Conventional Commit: squash merges use it as the commit message.
- Open the pull request with a typed template and fill in every section:

  ```sh
  gh pr create --template <feat|fix|docs|chore|refactor|ci>.md
  ```

- Pull requests merge by squash or rebase only. There are no merge commits.

## How a change reaches the workspace

Merging here applies nothing. The infra repository reads the project file from
this repository's `main`:

1. Merge the change to `main`.
2. The next pull request in jwall-engineering-infra shows it in its **Databricks plan** comment.
3. The owner runs the **Databricks apply** workflow in jwall-engineering-infra for this project.

The network range, cost center, workspace admins and the compute policies the
project may use are set centrally, in jwall-engineering-infra's `config.yaml`.
The fields of the project file are documented in
[docs/databricks.md](https://github.com/jwallace145/jwall-engineering-infra/blob/main/docs/databricks.md#the-project-file).

## Releases

[Release Please](https://github.com/googleapis/release-please) keeps a release
pull request open with the next version and the changelog. Merging it tags the
version. It owns `CHANGELOG.md`; nobody edits that file by hand.
