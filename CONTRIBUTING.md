# Contributing to the CPACC content pack

Thanks for helping improve the bank. This repository contains question content for the CPACC certification only.

## Before you start

- **Never submit a question from a live IAAP exam.** Reproduce only from public sources, in your own words.
- **Report a security problem privately.** Do not open a public issue with a working payload or a live malicious URL. See [.github/SECURITY.md](.github/SECURITY.md).
- Questions must be answerable from the current CPACC Body of Knowledge and the public references you cite.
- Every change must keep the pack valid. The validation rules are in the app's `src/lib/authoring/` and run through `scripts/bank/validate.ts`.
- One question per issue or pull request. A batch is hard to review and hard to merge.
- By contributing, you agree that your contribution is licensed under [CC BY-SA 4.0](LICENSE), the same licence as the rest of the pack.

## Language and conduct

This pack follows its own [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md). It has two parts: how we treat each other in issues and reviews, and how questions are worded. The wording rules apply to every new question and every edit.

- **People first by default:** "a person with a disability", "a student who is deaf". Identity-first is valid where the community prefers it ("Deaf people", "autistic people", "blind people"). Never use a condition as a noun for a person ("a quadriplegic", "an epileptic", "the disabled").
- **Describe the barrier, not the deficit:** "uses a wheelchair", not "wheelchair-bound", "has multiple sclerosis", not "suffers from". Never "victim of".
- **No pity and no inspiration:** no "less fortunate", "brave despite", or "tragic".
- **No disability as metaphor or insult:** no "blind to", "tone-deaf", "crippling", "crazy", "OCD", "lame", "deaf ears".
- **Quote, do not adopt, an outdated term.** It may appear only when the term is the subject, inside a quotation, or part of a proper name. Put it in quotation marks and explain it in the rationale or explanation.
- **A slur or a dehumanising frame blocks a pull request.** A dated term is a change request, not a rejection of the contribution.

The full term table is in [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md#12-words-we-avoid).

## Three ways to contribute

| Path                                                                                                      | Who it is for        | What you produce       |
| --------------------------------------------------------------------------------------------------------- | -------------------- | ---------------------- |
| [Fix an existing question](https://github.com/mocks-org/mocks-cpacc/issues/new?template=fix-question.yml) | no git needed        | a structured report    |
| [Submit a new question](https://github.com/mocks-org/mocks-cpacc/issues/new?template=new-question.yml)    | no git needed        | a structured proposal  |
| Fork this repository and open a pull request                                                              | comfortable with git | the JSON change itself |

There is a middle path too. The Mocks app `/author` route at [mocks.oxypteros.com/author](https://mocks.oxypteros.com/author) is a client-only editor that validates a question and exports its JSON, and it never sends content to a server. Draft there, export, then paste or attach the export in a pull request or an issue comment.

An issue is **intake, not delivery**. The repository is the source of truth, so an accepted report is re-authored as JSON and merged by a maintainer, or by you if you open the pull request.

Reporters are credited in the pull request body and in the release page.

## Report a problem or propose a question

Use the issue forms. They ask for exactly what is needed and nothing else.

- **Fix** asks for the question ID (shown as **Question ID** on the results screen), the stem as it appears, what is wrong, what is correct, and a public source.
- **New** asks for the module, stem, four options with a short label and a rationale each, the correct option, the explanation, references, difficulty, optional tags, and whether an AI tool drafted it.

Review metadata (`reviewer`, `reviewedAt`, `sourceCheckedAt`, `status`) is not requested. A submission stays in `review` until someone verifies it against its source. The writer's `author` credit is not review metadata, include it so contributors can be credited publicly on the site and in the repository.

### What happens next

The issue gets `needs-triage`, then one of `needs-source`, `accepted`, or `declined`. Accepted submissions are re-authored, merged, and listed in the next release.

## Set up to work on the pack

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

CI runs `validate` and `length-audit` on every pull request, and `link-check` weekly. It checks out the app's default branch into `.mocks-app/` (set `MOCKS_APP_REF` to pin a commit), so a local app checkout is only needed for the commands above.

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
   - `difficulty` -- 1 to 5, see [Difficulty and tags](#difficulty-and-tags).
   - `tags` -- 1 to 3 topic labels, see [Difficulty and tags](#difficulty-and-tags).
   - `provenance` -- `authored`, or `llm_assisted` when an AI tool drafted it.
   - `author` -- your name or handle. It is public credit and is not review metadata. Maintainers can add it from the pull request if you omit it.
   - `reviewer`, `reviewedAt`, and `sourceCheckedAt` -- required once `status` is `published`. Dates use `YYYY-MM-DD`.
   - `images` -- leave empty, images are not published yet.
   - `status` -- `draft`, `review`, `published`, or `retired`. A new submission starts as `review`.
5. Run the validator, then the length audit. Rewrite options to fix a length or cue problem, never pad an option just to change its length.

## Option rules

- Exactly 4 options for exam questions.
- Exactly one correct option, the other three must be plausible and defensible distractors.
- No duplicate option text or IDs within a question.
- Avoid absolute words in distractors (`all`, `always`, `never`, `only`, `must`, ...) if they make the wrong answer obvious.
- Keep the correct answer from being consistently the longest or shortest option (the audit reports the distribution per module and per 20-question window).
- Avoid using "all of the above", "none of the above", or negative stems that depend on a single word.

## Difficulty and tags

`difficulty` is a 1-5 self-assessment used for balance, not for scoring. Use the same anchors every time:

| Value | Meaning                                                                       |
| ----- | ----------------------------------------------------------------------------- |
| 1     | Recall a definition or a single fact.                                         |
| 2     | Recognise or apply a concept to a familiar example.                           |
| 3     | Apply a concept to a scenario, with distractors that need real understanding. |
| 4     | Compare models, analyse a situation, or choose between defensible options.    |
| 5     | Synthesise across modules or evaluate a trade-off.                            |

Most of the bank sits at 2 and 3 on purpose. A 5 should be rare, do not use it for a question that is merely long.

`tags` are lowercase kebab-case labels, 1 to 3 per question. Reuse one of these when it fits:

| Module          | Suggested tags                                                                                                                                                                                                       |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `disabilities`  | `visual-disabilities`, `auditory-disabilities`, `cognitive-disabilities`, `mobility-disabilities`, `speech-disabilities`, `assistive-technology`, `theoretical-models`, `functional-solutions-model`, `social-model` |
| `accessibility` | `universal-design`, `udl`, `inclusive-design`, `wcag`, `digital-accessibility`, `keyboard-accessibility`, `usability`, `built-environment`                                                                           |
| `standards`     | `international-conventions`, `crpd`, `eu-directives`, `management-strategies`, `business-case`, `communication`                                                                                                      |

A new tag is fine when none of these fits, as long as it is generic enough to be reused. Tags are reviewed with the question, so a one-off label may be replaced.

## Review requirements

A question can be published only after a second pass that:

- checks the answer against the cited source (`sourceCheckedAt`),
- checks the explanation and every option rationale (`reviewedAt`),
- checks the wording against [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) (people-first language, no outdated or dehumanising terms),
- checks the question against [ACCESSIBILITY.md](ACCESSIBILITY.md) (linear reading, no visual-only meaning, no option-number references),
- records the checker's name in `reviewer`.

The `reviewer` is the person who verified the question, not necessarily its author.

If you change the stem, an option, or the correct answer of a published question, update the review metadata in the same pull request.

## Bank metadata

`exam.json` and `exam/bank.json` are shared across the pack. Change them only when the exam blueprint changes:

- `exam.json` sets the exam title, provider, duration, question count, option count, pass threshold, and status.
- `exam/bank.json` sets the bank version, status, and the per-module draw counts. Draw counts must add up to `exam.json`'s `questionCount`.

Bump `bank.version` when you publish a new set of questions. Tag the release (`v0.1.0`, `v0.2.0`, ...) so the app can pin a full commit SHA.

## Pull requests

- One topic per pull request (a module, a review pass, a metadata change).
- Link the issue it resolves with `Closes #XX`.
- The pull request template lists the checks. Include the validator output in the description when it changes question counts or status.
- Do not edit generated files, there are none in this repository. The app generates its own SQL and JSON artifacts.
