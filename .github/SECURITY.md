# Security policy

This repository ships **content, not code**. It holds question JSON, exam configuration, and documentation. There is no server, no database, no account system, and no build step that a consumer executes. The app that renders the pack lives in [`mocks-org/mocks`](https://github.com/mocks-org/mocks).

That makes the security surface narrow, but not empty. The realistic risks are in what the content can deliver and how a release is pinned.

## Supported versions

The pack is consumed at a pinned commit SHA. Only the latest release is supported. An older pin stays reproducible, but it is not patched, move to the current release to receive a fix. A fix reaches a deployment only when its operator re-pins the pack and reseeds the database.

## What counts as a vulnerability

| In scope                                                                                                                                       | Why it matters                                                                                      |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| Markup or URL injection in a question field (`stem`, `options`, `rationale`, `explanation`, `references`) that escapes the app's renderer      | The app allows a small Markdown subset and sanitises link schemes. A bypass enters through content. |
| A reference URL that serves malware, phishing, or unrelated material, including a cited domain that expired and was registered by someone else | The app renders references as clickable external links. The pack is the source of those URLs.       |
| A release that was altered outside a reviewed pull request (a moved tag, a rewritten pin, or a changed commit under an existing release)       | Consumers trust the SHA they pin. Release integrity is the pack's main supply-chain property.       |
| A secret or token exposed in the repository, its history, or its CI logs (for example `MOCKS_APP_TOKEN`)                                       | The workflow uses it to read the app repository during validation.                                  |
| A workflow change that would expose secrets to a pull request from a fork                                                                      | Fork PRs do not receive secrets. A change that removes that boundary is a vulnerability.            |

| Out of scope                                                                     | Where it goes                                                                                             |
| -------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| A wrong answer, an ambiguous stem, a weak distractor, or a disputed citation     | [Fix an existing question](https://github.com/mocks-org/mocks-cpacc/issues/new?template=fix-question.yml) |
| A dead reference link (404 or 410)                                               | The same form, `link-check` reports it weekly                                                             |
| A typo, a formatting problem, or a wording change                                | The same form                                                                                             |
| Rendering, scoring, authoring-tool, deployment, or accessibility bugs in the app | [Mocks issues](https://github.com/mocks-org/mocks/issues)                                                 |
| The fact that the questions are unofficial and are not IAAP exam items           | By design, see the README                                                                                 |

If you are unsure which side a report falls on, send it privately and we will route it.

## Reporting a vulnerability

**Preferred:** open the repository's **Security** tab and choose **Report a vulnerability**. That starts a private advisory visible only to the maintainers.

If that form is not available, send a direct message to a maintainer on GitHub. Do not open a public issue with a working payload or a live malicious URL.

Include:

- the question ID or file path, and the field involved
- what you expected and what happened
- a minimal reproduction, without real personal data (this repository holds none)
- whether the content is already in a release, and which tag or commit
- how you would like to be credited, or that you prefer not to be

Do not test against a deployment you do not own, and do not contact the owner of a third-party domain to demonstrate a takeover. A hijacked citation is fixed by replacing the reference, not by negotiating with its new owner.

## What we do

1. Acknowledge the report within five working days.
2. Confirm whether the issue is in a released pin and which versions are affected.
3. Prepare the fix privately when a public report would put users at risk, then publish the fix and an advisory.
4. Cut a patch release and tell consumers to re-pin. A deployment changes only after it reseeds, so the advisory says so.
5. Credit the reporter in the advisory and the release notes, unless they ask otherwise.

There is no bug bounty. Good-faith research that stays within this repository and does not degrade a service, access other people's data, or attack a third-party site will not be pursued by the maintainers.

## Third-party links

Reference URLs point to material the pack does not control. Standards bodies, government sites, publishers, and archives. Their security and availability are not this repository's to fix. A report that a citation now leads somewhere unrelated is still welcome, because the fix is ours (replace or retire the reference).

## Changes to this policy

Pull requests are welcome. A change to the reporting route or to the CI boundary should also be reflected in `README.md` and `CONTRIBUTING.md`.
