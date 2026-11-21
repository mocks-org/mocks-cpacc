# Contributing to the CPACC content pack

Thanks for helping improve the bank. This repository contains question content only, the app that renders it lives in [mocks-org/mocks](https://github.com/mocks-org/mocks).

## Before you start

- Questions must be answerable from the current CPACC Body of Knowledge and the public references you cite.
- Every change must keep the pack valid. The validation rules are in the app's `src/lib/authoring/` and run through `scripts/bank/validate.ts`.
- By contributing, you agree that your contribution is licensed under [CC BY-SA 4.0](LICENSE), the same licence as the rest of the pack.

You need **Node 26** and a checkout of the app next to this repository:

```
parent/
├── mocks/          # the app, provides the validator
└── mocks-cpacc/    # this pack
```

## Validate

From this repository's root:

```sh
node ../mocks/scripts/bank/validate.ts .
```

- The command exits non-zero on any error.
- Fix errors before opening a pull request.
- Warnings are visible but do not fail the run.

Optional checks:

```sh
node ../mocks/scripts/bank/length-audit.ts .   # option-length / answer-cue audit
node ../mocks/scripts/bank/link-check.ts .     # reference URLs (network)
```

- `link-check` fails on a 404/410 or a host that no longer resolves.
- Timeouts and 5xx answers are retried and then reported as unverified without failing, because a blocked CI runner does not prove the page is gone.
- Re-run it locally or manually before editing a citation CI could not verify.
- `--strict` makes those failures fatal.

CI runs `validate` and `length-audit` on every pull request, and `link-check` weekly. It checks out the app at a pinned commit into `.mocks-app/`, so a local app checkout is only needed for the commands above.

Do not commit `.mocks-app/`. The checkout uses the `MOCKS_APP_REPOSITORY` variable and, for a private app repository, the `MOCKS_APP_TOKEN` secret.  
See [CI setup](./README.md#ci-setup).

## Add a question

1. Choose the module the question belongs to:

   | Module ID       | Title                                                | Draw |
   | --------------- | ---------------------------------------------------- | ---- |
   | `disabilities`  | Disabilities, Challenges, and Assistive Technologies | 40   |
   | `accessibility` | Accessibility and Universal Design                   | 40   |
   | `standards`     | Standards, Laws, and Management Strategies           | 20   |

2. Copy an existing file in `exam/questions/<module>/` as a starting point.
3. Name the file after the question ID: `cpacc-exam-<module>-<four digits>.json`. The filename must equal the `id` field, and the ID must start with the exam slug `cpacc-`.
4. Fill in every field. A published question needs:
   - `stem` -- the question text, in English.
   - `options` -- exactly 4 options, each with a unique `id`, `text`, `shortLabel`, and `rationale`.
   - `correctOptionId` -- the ID of exactly one correct option.
   - `explanation` -- a shared lesson that works for every learner. Do **not** refer to option numbers ("option 1", "answer 4"), the app shuffles options.
   - `references` -- at least one source. `web` needs a public URL, `publication` needs author/publisher and a four-digit year, `general` needs a `note` explaining why no single source is needed.
   - `reviewer`, `reviewedAt`, and `sourceCheckedAt` -- required once `status` is `published`. Dates use `YYYY-MM-DD`.
   - `images` -- leave empty, images are not published yet.
   - `status` -- `draft`, `review`, `published`, or `retired`.

5. Run the validator, then the length audit. Rewrite options to fix a length or cue problem, never pad an option just to change its length.

## Option rules

- Exactly 4 options for exam questions.
- Exactly one correct option, the other three must be plausible and defensible distractors.
- No duplicate option text or IDs within a question.
- Avoid absolute words in distractors (`all`, `always`, `never`, `only`, `must`, …) if they make the wrong answer obvious.
- Keep the correct answer from being consistently the longest or shortest option (the audit reports the distribution per module and per 20-question window).
- Avoid using "all of the above", "none of the above", or negative stems that depend on a single word.

## Review requirements

A question can be published only after a second person has:

- checked the answer against the cited source (`sourceCheckedAt`),
- checked the explanation and every option rationale (`reviewedAt`),
- recorded their name in `reviewer`.

If you change the stem, an option, or the correct answer of a published question, update the review metadata in the same pull request.

## Bank metadata

`exam.json` and `exam/bank.json` are shared across the pack. Change them only when the exam blueprint changes:

- `exam.json` sets the exam title, provider, duration, question count, option count, pass threshold, and status.
- `exam/bank.json` sets the bank version, status, and the per-module draw counts. Draw counts must add up to `exam.json`'s `questionCount`.

Bump `bank.version` when you publish a new set of questions. Tag the release (`v0.1.0`, `v0.2.0`, …) so the app can pin a full commit SHA.

## Pull requests

- One topic per pull request (a module, a review pass, a metadata change).
- Include the validator output in the description when it changes question counts or status.
- Do not edit generated files, there are none in this repository. The app generates its own SQL and JSON artifacts.
