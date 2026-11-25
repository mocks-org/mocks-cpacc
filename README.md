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
| Bank             | `cpacc-exam`                                                |
| Authoring schema | `schemaVersion: 3`                                          |
| Modules          | `disabilities` (40), `accessibility` (40), `standards` (20) |
| Format           | 100 questions, 4 options each, 120 minutes, 80% to pass     |

The pack root is shaped exactly like one exam directory inside the app's `content/` folder. That means the app can validate and seed it without a conversion step.

## Use it from the app

> **This repository is a content pack, not an app.** It holds questions and exam configuration and does nothing on its own. To use it, pick one:
>
> - **Use it online** at **[mocks.oxypteros.com](https://mocks.oxypteros.com)**, which always runs the latest release of this pack. No install, no account.
> - **Install the [Mocks app](https://github.com/mocks-org/mocks)** first and then add the pack to it, following the steps below.

---

- Every command runs from the **root of your app repository** (`mocks/`), never from this pack.
- Both sections below assume the app is already installed. If `pnpm dev` serves `/portal/cpacc-demo`, you are ready.
- If you only run Mocks locally, stop after **Local app**.
- If you also deploy it, complete **Local app** first, then **Remote app**.

### Local app (your machine)

#### Install it for the first time

```sh
pnpm content:add github:mocks-org/mocks-cpacc   # newest release
pnpm bank:validate content/cpacc                # check this pack only
pnpm bank:seed:local --exam cpacc               # load it into local D1
```

`pnpm dev` then serves it at `/portal/cpacc`.

#### Update to the latest release

```sh
pnpm content:update cpacc
pnpm bank:validate content/cpacc
pnpm bank:seed:local --exam cpacc
```

#### Move to a specific release, or downgrade

Replace the first line with the release you want, using the full 40-character commit SHA listed on the pack's [releases](https://github.com/mocks-org/mocks-cpacc/releases) page:

```sh
pnpm content:update cpacc --ref <full commit SHA>
pnpm bank:validate content/cpacc
pnpm bank:seed:local --exam cpacc
```

`--ref` is always the full 40-character commit SHA, never a tag or a branch (a tag can be moved, and the pin has to stay reproducible).

### Remote app (your deployment)

"Remote" means **your own deployed version of Mocks**. The Cloudflare Worker and remote D1 database you created when you deployed it.

Installing is always a local action, `content:add` and `content:update` write files into your repository, and only the seed reaches the cloud. So there are only three steps: install the pack locally, commit it, then seed the deployed database. Deploying the Worker never moves questions by itself, the app reads them from D1.

The one-time prerequisites are the same ones the Mocks deploy walkthrough already covered. The D1 id in `wrangler.jsonc`, `pnpm exec wrangler login`, and `pnpm db:migrate:remote` for the deployed schema.

#### First time on the live site

Assuming you already installed and seeded the pack in **[Local app](#local-app-your-machine)** above. Commit the pack files (`content/packs.json` and `content/cpacc/**`) and seed deployed database:

```sh
pnpm bank:seed:remote --exam cpacc
```

#### Update the live site to the latest release

First make sure you have **[updated the pack locally](#update-to-the-latest-release)** commit the pack files and re-seed the remote database:

```sh
pnpm bank:seed:remote --exam cpacc
```

#### Move the live site to a specific release, or downgrade

Same procedure, first **[move to a specific release, or downgrade](#move-to-a-specific-release-or-downgrade)** locally, then commit the pack files and last re-seed the remote database:

```sh
pnpm bank:seed:remote --exam cpacc
```

#### Notes:

- **Always pass `--exam cpacc` to the remote seed.** Without it, `bank:seed:remote` writes every pack on disk, including the bundled demo, into the live database.
- The remote seed replaces that bank's rows, so it is the switch that changes what visitors see.
- If the deployed site has no pack yet and the repository does not have one either, do the **[Local app](#local-app-your-machine)** install first. That is what writes `content/cpacc/` and the pin. Then return here for the single seed command.

### After a local or remote change

- Commit `content/packs.json` and `content/cpacc/**` together, that commit is the release record.
- `pnpm content:list` shows what is pinned, at which short SHA, and how many questions it holds.
- Add `--dry-run` to any `content:` command to see what it would change without writing.
- `content:add` copies files and writes the pin but never touches a database, so the `bank:seed` step is not optional.

## Validate locally

The validation rules live in the app's `scripts/bank` tooling. Check out the Mocks app next to this pack and:

```sh
parent/
├── mocks/          # the Mocks app, provides the validator
└── mocks-cpacc/    # this pack
```

Run from the **`mocks-cpacc/` root**

```sh
node ../mocks/scripts/bank/validate.ts .
```

The pack root expands to every bank it contains. To run the option-length audit and the reference check as well:

```sh
node ../mocks/scripts/bank/length-audit.ts .
node ../mocks/scripts/bank/link-check.ts .   # network
```

- `link-check` fails on a 404/410 or a host that no longer resolves.
- Timeouts and 5xx answers are retried and then reported as unverified without failing, so a blocked runner does not fail the weekly run.
- Use `--strict` to make those fatal.

CI runs the same checks against the app's default branch (`.github/workflows/validate.yml`), so a local checkout is more of a convenience rather than required.

## CI setup

> Only needed if you fork/clone this pack repository. Skip this section if you only install or use the pack.

The workflow checks out the app to use its schema and validator. Configure the checkout on this repository, it is intentionally not guessed from the owner name.

| Setting                | Kind     | Value                                                                  |
| ---------------------- | -------- | ---------------------------------------------------------------------- |
| `MOCKS_APP_REPOSITORY` | variable | `<owner>/<app-repo>` (required)                                        |
| `MOCKS_APP_REF`        | variable | full app commit SHA (optional -- defaults to the app's default branch) |
| `MOCKS_APP_TOKEN`      | secret   | read access to the app repository (required for private repos)         |

- The optional ref is a **full commit SHA**, not a tag or branch. Leave the variable unset to follow the app's default branch, which is the set of rules the app applies today. Set it only to reproduce an older result or to unblock a release against an app commit you trust.
- The token only needs to read the app repository. A fine-grained PAT with **Contents: Read** on it, or a GitHub App installation token (the workflow's `GITHUB_TOKEN` cannot read another private repository).
- Secrets are not passed to pull requests from forks. If this pack becomes public while your Mocks app repo stays private, external PRs cannot run this job. Make the app public or publish the schema before opening the pack.
- There is no implicit `<owner>/<app-repo>` default. This pack uses the official `mocks-org/mocks` as `MOCKS_APP_REPOSITORY`.

### With `gh`

```sh
gh variable set MOCKS_APP_REPOSITORY --repo <owner>/mocks-cpacc \
  --body <owner>/<app-repo>
gh variable set MOCKS_APP_REF --repo <owner>/mocks-cpacc \
  --body <full app commit sha>          # optional
gh secret set MOCKS_APP_TOKEN --repo <owner>/mocks-cpacc
```

- The app commit each run used is printed in the job summary.
- A `MOCKS_APP_REF` that no longer resolves is reported as a warning and the run continues on the default branch, so a rewritten app history never blocks this repository.
- The SHA must exist in the repository named by `MOCKS_APP_REPOSITORY`.

## Licence

The question content in this repository is licensed under [CC BY-SA 4.0](LICENSE). The Mocks app code is licensed separately under MIT. If you redistribute a modified version of this pack, you must keep the same licence and credit the source.

## Releases

- Releases are tags (`v0.1.0`, `v0.2.0`, …).
- The Mocks app stores the full commit SHA of the tag it uses, so a release is reproducible and auditable.
