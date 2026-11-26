# Accessibility statement

This statement covers the **question content** in this repository and its **documentation**. It is not the accessibility statement for the Mocks app or any deployed version of it. The pack is data, it has no interface of its own, and conformance is a property of the page that renders it.

## Scope

**Covered**

- Every question field: `stem`, `options.text`, `shortLabel`, `rationale`, `explanation`, `references`, and `tags`.
- This repository's documentation: `README.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, and this file.
- The issue forms and pull request template used to report and review content.

**Not covered**

- The Mocks app, the `/author` editor, the exam player, and any deployed site. Those belong to [`mocks-org/mocks`](https://github.com/mocks-org/mocks) and its own accessibility statement.
- The IAAP CPACC exam, its booking system, and its accommodations process. This pack cannot grant an accommodation, contact IAAP for that.
- Third-party pages linked from `references`. We choose and check the citation, not the destination's accessibility.

## Target

The content is written to be usable when rendered by a player that targets **WCAG 2.2 Level AA**. The pack does not claim conformance on its own, because a JSON file cannot conform. Contrast, typography, focus, zoom, reflow, and timing are set by the app.

## What the content guarantees

| Guarantee                                                                                                | How it is checked                           |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------- |
| No answer depends on colour, position, shape, or a purely visual detail                                  | Human review                                |
| A question reads linearly, the stem, then each option in order, without needing the others               | Human review                                |
| Options are shuffled and labelled at render time. No explanation or rationale refers to an option number | Schema (labels are never stored) and review |
| No "all of the above" or "none of the above", and no absolute-word cue that gives the answer away        | Length audit and review                     |
| Plain language, short sentences, acronyms expanded on first use, no idioms or unexplained jargon         | Human review                                |
| Answering requires reading and choosing only. No question depends on hearing, hover, drag, or timing     | Human review                                |
| No images in v0. When images arrive they need meaningful alt text, dimensions, and a resolved key        | Schema and review                           |
| Inclusive, people-first wording, with outdated terms quoted rather than adopted                          | [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)    |
| A reference has a descriptive title and a public URL, and its link is checked every week                 | CI (`link-check`)                           |

## How it is checked

- **Automated, in this repository:** `bank:validate` (schema, unique IDs, option count, exactly one correct option, references present, duplicate questions, no `TODO`), `length-audit` (answer cues, including absolute words), and a weekly `link-check`.
- **Human, in this repository:** a second pass on accuracy, sourcing, wording, distractor quality, and the guarantees above. Language is reviewed against the code of conduct.
- **In the app, not here:** an axe suite on the demo pack, keyboard testing, and screen-reader use of the player. Those results belong to the app's statement.
- **Not checked:** per-question testing with assistive technology, a measured reading level, and cognitive-load testing with real candidates.

## Known limitations

- **English only.** There are no translations, and idioms are avoided but not eliminated by a translation review that does not exist.
- **No per-question assistive-technology testing.** Review is a checklist applied by sighted reviewers. We do not claim that a screen-reader user has answered every question.
- **No measured reading level.** "Plain language" is a judgement in review, not a scored target.
- **Small review capacity.** Most questions have been written and reviewed by a single maintainer. Independent review is limited, and external reviewers are welcome.
- **Older questions are corrected on review, not audited in bulk.** A question published before this statement is brought into line when it is next edited or reviewed.
- **No image descriptions yet.** Images are not published in v0, so the alt-text path is specified but untested with real content.
- **The pack cannot fix the player.** Contrast, focus visibility, zoom, reflow, and time limits are the app's responsibility. If the problem is the interface, report it there.

## Feedback

Report an accessibility problem with the [fix-question form](https://github.com/mocks-org/mocks-cpacc/issues/new?template=fix-question.yml). Include:

- the question ID (shown on the results screen)
- what makes the question hard or impossible to answer, and with which assistive technology and browser if relevant
- a suggested wording when you have one

An accessibility report is treated as a content bug, not a style preference. A question that cannot be answered with a screen reader is prioritised over a wording improvement. If the problem is in the app's interface rather than the question, open an issue in [`mocks-org/mocks`](https://github.com/mocks-org/mocks/issues).

## Review

- This statement is reviewed with each release and at least once a year.
- Last reviewed: 2026-11-26.
- It is versioned with the pack. The release tag and commit a deployment uses are recorded in that deployment's `content/packs.json`.

## References

- [Web Content Accessibility Guidelines (WCAG) 2.2](https://www.w3.org/TR/WCAG22/)
- [W3C WAI: Writing for web accessibility](https://www.w3.org/WAI/tips/writing/)
- [W3C WAI: WCAG 2 overview](https://www.w3.org/WAI/standards-guidelines/wcag/)
- [Code of conduct](CODE_OF_CONDUCT.md)

This statement is part of the pack and is licensed under [CC BY-SA 4.0](LICENSE).
