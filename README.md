# Mocks CPACC content pack

Unofficial practice questions for the **[IAAP Certified Professional in Accessibility Core Competencies (CPACC)](https://www.accessibilityassociation.org/cpacc)** exam. This repository is a content pack for the [Mocks](https://github.com/mocks-org/mocks) app, not the app itself.

> Mocks is independent and non-commercial. CPACC is a certification mark of the International Association of Accessibility Professionals (IAAP). This pack is not affiliated with, endorsed by, or sponsored by IAAP, and its questions are not official exam questions.

## What is in here

```
exam.json                # exam configuration (id: cpacc)
exam/
├── bank.json            # bank settings + module draw counts
└── questions/<module>/*.json  # one question per file
LICENSE                        # CC BY-SA 4.0
```

| Field            | Value                                                       |
| ---------------- | ----------------------------------------------------------- |
| Exam             | CPACC (official provider: IAAP)                             |
| Exam slug / ID   | `cpacc`                                                     |
| Bank             | `cpacc-exam`, version `0.1.0-beta`                          |
| Authoring schema | `schemaVersion: 3`                                          |
| Modules          | `disabilities` (40), `accessibility` (40), `standards` (20) |
| Format           | 100 questions, 4 options each, 120 minutes, 80% to pass     |

The pack root is shaped exactly like one exam directory inside the app's `content/` folder. That means the app can validate and seed it without a conversion step.

## Use it from the app

The app pins this pack by commit SHA in `content/packs.json`:

```json
{
  "cpacc": {
    "source": "https://github.com/mocks-org/mocks-cpacc",
    "ref": "<full commit SHA>"
  }
}
```

Then, from the app repository:

```sh
pnpm content:add github:mocks-org/mocks-cpacc --ref <full commit SHA>
pnpm bank:validate
pnpm bank:seed:local
```

**Note:** To install a specific release use:

```sh
pnpm content:add github:mocks-org/mocks-cpacc --ref <full commit SHA>
```

- `--ref` installs that exact release, without it `content:add` takes the newest tag and records its commit.
- `content:add` does not seed a database, so the `bank:seed` step is not optional.
- `pnpm content:update cpacc` moves an installed pack to the latest release tag (or `HEAD` when there is no tag).
- Content is never authored in the app repository.

## Validate locally

The validation rules live in the app's `scripts/bank` tooling. Check out the app next to this pack and:

```sh
parent/
├── mocks/          # the app, provides the validator
└── mocks-cpacc/    # this pack
```

Run from the `mocks-cpacc/` root

```sh
node ../mocks/scripts/bank/validate.ts .
```

The pack root expands to every bank it contains. To run the option-length audit and the reference check as well:

```sh
node ../mocks/scripts/bank/length-audit.ts .
node ../mocks/scripts/bank/link-check.ts .   # network
```

`link-check` fails on a 404/410 or a host that no longer resolves.  
Timeouts and 5xx answers are retried and then reported as unverified without failing, so a blocked runner does not fail the weekly run, use `--strict` to make those fatal.

CI runs the same checks against the app's default branch (`.github/workflows/validate.yml`), so a local checkout is more of a convenience rather than required.

## CI setup

The workflow checks out the app to use its schema and validator. Configure the checkout on this repository, it is intentionally not guessed from the owner name.

| Setting                | Kind     | Value                                                                  |
| ---------------------- | -------- | ---------------------------------------------------------------------- |
| `MOCKS_APP_REPOSITORY` | variable | `<owner>/<app-repo>` (required)                                        |
| `MOCKS_APP_REF`        | variable | full app commit SHA (optional -- defaults to the app's default branch) |
| `MOCKS_APP_TOKEN`      | secret   | read access to the app repository (required for private repos)         |

- The optional ref is a **full commit SHA**, not a tag or branch. Leave the variable unset to follow the app's default branch, which is the set of rules the app applies today. Set it only to reproduce an older result or to unblock a release against an app commit you trust.
- The token only needs to read the app repository. A fine-grained PAT with **Contents: Read** on it, or a GitHub App installation token (the workflow's `GITHUB_TOKEN` cannot read another private repository).
- Secrets are not passed to pull requests from forks. If this pack becomes public while the app stays private, external PRs cannot run this job. Make the app public or publish the schema before opening the pack.
- There is no implicit `<owner>/<app-repo>` default. The official pack uses `mocks-org/mocks` as `MOCKS_APP_REPOSITORY`.

### With `gh`

```sh
gh variable set MOCKS_APP_REPOSITORY --repo <owner>/mocks-cpacc \
  --body <owner>/<app-repo>
gh variable set MOCKS_APP_REF --repo <owner>/mocks-cpacc \
  --body <full app commit sha>          # optional
gh secret set MOCKS_APP_TOKEN --repo <owner>/mocks-cpacc
```

The app commit each run used is printed in the job summary. A `MOCKS_APP_REF` that no longer resolves is reported as a warning and the run continues on the default branch, so a rewritten app history never blocks this repository. The SHA must exist in the repository named by `MOCKS_APP_REPOSITORY`.

## Licence

The question content in this repository is licensed under [CC BY-SA 4.0](LICENSE). The Mocks app code is licensed separately under MIT. If you redistribute a modified version of this pack, you must keep the same licence and credit the source.

## Releases

Releases are tags (`v0.1.0`, `v0.2.0`, …). The app stores the full commit SHA of the tag it uses, so a release is reproducible and auditable. Content changes should arrive as pull requests, not direct pushes to `main`.
