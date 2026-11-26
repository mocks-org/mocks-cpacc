# Code of conduct

This repository is a question bank about accessibility. Its questions are read by people preparing for a professional certification, and many of those readers are disabled themselves. The words in a stem, an option, or an explanation are part of the product: a question that uses an outdated term teaches that term.

This document has two halves. [How we treat each other](#how-we-treat-each-other) covers behaviour in issues, pull requests, and reviews. [Language in question content](#language-in-question-content) covers the wording of the questions themselves. Both apply to maintainers, contributors, reviewers, and reporters.

## Scope

- This repository: issues, pull requests, review comments, discussions, commit messages, and release notes.
- Every field of a question: `stem`, `options.text`, `shortLabel`, `rationale`, `explanation`, `references`, `tags`, and the `author` credit.
- Any space where someone is representing this project, including the app's authoring tool when it is used to draft a question for this pack.

## Our commitments

1. **Accurate.** A question is checked against its cited source, not against a model or a memory.
2. **Dignified.** People are described as people, not as conditions, cases, or cautionary tales.
3. **Inclusive.** Wording does not exclude or stereotype by disability, gender, age, race, ethnicity, nationality, religion, class, body size, or mental health.
4. **Accessible.** Every question reads linearly and makes sense to a screen reader.
5. **Honest.** Authorship, review, and AI assistance are recorded, and mistakes are corrected in the open.

## How we treat each other

- **Critique the question, not the person.** "This option is doing too much work" is useful. "You clearly don't understand the social model" is not.
- **Assume good faith, then ask.** Most wording problems are habits, not malice. Say what you would change and why.
- **No harassment.** No slurs, threats, sexual attention, doxxing, or sustained personal attacks. No arguing that a group's existence or right to be described respectfully is "political".
- **Respect names and pronouns.** Use the name and pronouns a person uses for themselves, including in review comments and commit credits.
- **Do not ask anyone to speak for a group.** A disabled contributor is not the committee on disability language, and no one owes you a disclosure of their identity to justify an edit.
- **Credit people.** Reporters are credited in the pull request and the release notes, and `author` stays on the question.
- **Keep reports private.** A conduct report is not material for a public thread.

## Language in question content

These rules apply to every new question and every edit to an existing one. They do not require a bulk rewrite of the bank: a question is brought into line when it is next reviewed or corrected.

If you read only one rule, read this one: **describe the person, then the barrier, then the task.** Most outdated wording fails because it makes the condition the subject and the person the object.

### 1. People first by default

Write about the person before the condition.

- "a person with a disability", "people with low vision", "a student who is deaf", "a candidate with dyslexia".
- Not "a quadriplegic", "an epileptic", "a diabetic", "the disabled", "the mentally ill".

Identity-first language is equally valid, and some communities prefer it: "Deaf people", "autistic people", "blind people", and "disabled people" in the social-model tradition. Use identity-first wording when:

- the community named prefers it for itself,
- the question is about identity, culture, or the social model, or
- you are quoting a source that uses it.

Do not mix both forms in one question. When the question is about terminology itself, make the term the subject and explain in the rationale why it is used or rejected.

### 2. Describe the barrier, not the deficit

| Avoid                                               | Write instead                                                                    |
| --------------------------------------------------- | -------------------------------------------------------------------------------- |
| wheelchair-bound, confined to a wheelchair          | a wheelchair user, a person who uses a wheelchair                                |
| suffers from, afflicted by, stricken with           | has, lives with, is being treated for, is diagnosed with                         |
| victim of, battling, fighting                       | has, is being treated for                                                        |
| the disabled, the blind, the deaf, the mentally ill | disabled people, blind people, Deaf people, people with mental health conditions |

A ramp question is about the ramp. "A person who uses a wheelchair cannot enter the building" keeps the barrier in the environment. "A wheelchair-bound person cannot enter" puts the barrier in the body.

### 3. No pity, no inspiration

Do not frame disabled people as brave, tragic, inspiring, "less fortunate", or "suffering". A question about the charity model may describe that framing because the framing is the subject, but the narration must not adopt it.

- Wrong: "Despite her disability, she is a productive employee."
- Right: "She uses a screen reader and completes the same tasks as her colleagues."

### 4. No disability as metaphor or insult

Do not use a condition to mean something else, even casually.

- "blind to the risk", "tone-deaf to feedback", "turn a blind eye", "fall on deaf ears".
- "crippling debt", "a lame excuse", "crazy deadlines", "a bit OCD", "bipolar priorities", "schizo architecture".

Use the plain meaning instead: overlooked, insensitive to, ignored, severe, weak, unpredictable, particular, changing.

### 5. Gender and family

- Use **they** for a person of unknown or unspecified gender. Never "he or she", "(s)he", or "he/she".
- Do not default to "he" for a developer, administrator, engineer, or user. If a scenario needs a name, use one that is clearly fictional and vary it.
- Do not assume a spouse, a partner of a particular gender, a parent, or a family structure.
- Use gender-neutral titles: chair, spokesperson, flight attendant, firefighter.
- When a source or a person uses a specific term for themselves, keep it.

### 6. Age

- "older adults", "people aged 65 and over", "children", "young people".
- Not "the elderly", "seniors" as a group noun, "old people", or "geriatrics" for people.
- "Age-related hearing loss" is fine: it names the cause, not the person.

### 7. Race, ethnicity, nationality, religion

- Capitalise identity terms as the group and the source use them: Black, Indigenous, Latino, Latina, Latine.
- Name the country or region when the claim is specific. Avoid "third world", "developing world", and "the West" as stand-ins for a place.
- Do not use "normal", "standard", or "regular" to mean white, male, non-disabled, straight, or middle-class. Use "typical", "non-disabled", or "the majority" when you need a contrast.
- Do not treat a group as a monolith or build a question whose correct answer is a stereotype.
- "Minority" needs a referent: "people from ethnic minority groups in the United Kingdom", not "minorities".

### 8. Mental health, body size, and socioeconomic status

- "a person with schizophrenia", "a person with a substance use disorder", "a person experiencing homelessness", "a person with a low income", "a person with a larger body".
- Not "a schizophrenic", "an addict", "the homeless", "the poor", "an obese person".
- "died by suicide", not "committed suicide".

### 9. Plain and accessible language

- Short sentences, one idea per question, acronyms expanded on first use.
- No idioms, cultural references, or unexplained jargon. A candidate whose first language is not English still has to answer.
- Do not make the answer depend on colour, shape, position, or a purely visual detail.
- Read the stem and each option in order, without the others, as a screen reader would.
- Avoid double negatives and "except" chains.

The option and explanation rules in [CONTRIBUTING.md](CONTRIBUTING.md#option-rules) still apply. Inclusive wording does not excuse a weak distractor.

### 10. Scenario characters

- Use clearly fictional names. Do not attach a real person's name to an invented scenario.
- Vary names, roles, and settings without falling into a pattern where the only woman is the assistant or the only disabled character is the one who needs help.
- The character is not the punchline. A distractor can be wrong without mocking a group.
- When the barrier is the subject, the environment causes it, not the person's body.

### 11. When an outdated term has to appear

Sometimes the term is the lesson. It may appear only when:

- the question is about the term itself (for example, why "handicapped" is no longer used in signage), or
- it sits inside a quotation from a cited source, or
- it is part of a proper name, such as "American Foundation for the Blind" or "National Association of the Deaf".

When it appears, put it in quotation marks, attribute it, and explain in the rationale or explanation why it is used or rejected. Never use it as a joke, a throwaway distractor, or a `shortLabel`. Do not make a distractor wrong merely because it sounds offensive: the rationale must give a substantive reason.

### 12. Words we avoid

| Avoid                                         | Use instead                                                                     |
| --------------------------------------------- | ------------------------------------------------------------------------------- |
| handicapped, the handicapped                  | people with disabilities, disabled people                                       |
| deaf and dumb, deaf-mute                      | Deaf person, person who is hard of hearing                                      |
| retarded, mentally retarded                   | person with an intellectual disability                                          |
| special needs, special needs child            | disabled child, child with a disability ("special education" for the service)   |
| differently abled, handicapable, challenged   | person with a disability                                                        |
| high-functioning, low-functioning             | describe the support need or the skill                                          |
| normal, healthy (as the opposite of disabled) | non-disabled, people without disabilities, typical                              |
| addict, junkie, alcoholic                     | person with a substance use disorder, person who uses drugs, person in recovery |
| the homeless, the poor, the elderly           | people experiencing homelessness, people with low income, older adults          |
| manpower, man-hours, chairman, guys           | workforce, staff hours, chair, everyone, team                                   |
| he or she, (s)he, he/she                      | they                                                                            |
| master/slave, whitelist/blacklist, dummy      | primary/replica, allowlist/denylist, placeholder                                |
| sanity check, grandfathered                   | quick check, confidence check, legacy, exempted                                 |
| third world, developing countries             | name the country or region, low- and middle-income countries                    |
| illegal alien, illegal immigrant              | undocumented person, person without legal status (only when relevant)           |

The table is a floor, not a ceiling. A term that is not listed can still fail the rules above.

### 13. If you are not sure

- Prefer the term a community uses for itself, and check a current style guide before guessing.
- Ask in the issue or pull request. A maintainer decides, and the decision is written into the review.
- Do not guess at a person's identity, condition, or pronouns to make a scenario work. Rewrite the scenario.
- Language changes. This document is reviewed with the bank and can be changed by pull request.

## Reviewing language

- Language is reviewed next to accuracy and sourcing, not after them.
- Raise a wording problem as a suggestion with a concrete alternative. "Can we say 'people with low vision' here?" is easier to act on than "this is ableist".
- A dated term is a change request. A slur, a dehumanising frame, or a stereotype used as the correct answer is a blocker.
- A reviewer does not have to disclose their own identity to apply these rules, and no one is required to speak for a group.
- If the author and reviewer disagree, a second maintainer decides. The question stays in `review` until it is resolved.

## Reporting and enforcement

Report a conduct problem privately to the maintainers. Do not open a public issue that names a person. Direct-message a maintainer through GitHub, or open a short issue asking for a private channel without naming anyone or repeating the content.

Maintainers will:

1. Acknowledge the report within five working days.
2. Keep the report and the reporter's identity confidential.
3. Recuse anyone involved in the incident from the decision.
4. Choose a response proportional to the problem: a private word, a required edit, removal of a comment, or a temporary or permanent ban from the repository.
5. Explain the decision to the reporter and to the person concerned, without disclosing third parties.

An appeal goes to a maintainer who was not part of the decision. Retaliation against a reporter or a witness is itself a violation.

Security problems have their own private route: [.github/SECURITY.md](.github/SECURITY.md). Do not use this section for a payload or a live malicious link.

## For maintainers

- Apply this document to your own questions first.
- Do not merge a question that violates the language rules, even if it is otherwise accurate.
- Record the reason for a language decision in the pull request, so the next reviewer does not relitigate it.
- When the bank's terminology guidance changes, update this file, `CONTRIBUTING.md`, and the app's authoring guide in the same release.

## Changes to this document

Pull requests are welcome. Propose the change, say which rule or example it affects, and cite a current source when the change is about a term. The same review applies as for a question: a second person reads it before it merges.

## References

- [APA Style: Disability](https://apastyle.apa.org/style-grammar-guidelines/bias-free-language/disability)
- [W3C WAI: Writing for web accessibility](https://www.w3.org/WAI/tips/writing/)
- [Google developer documentation style guide: Inclusive language](https://developers.google.com/style/inclusive-documentation)
- [Microsoft Writing Style Guide: Bias-free communication](https://learn.microsoft.com/en-us/style-guide/bias-free-communication)
- [GOV.UK - Inclusive language: words to use and avoid when writing about disability](https://www.gov.uk/government/publications/inclusive-communication/inclusive-language-words-to-use-and-avoid-when-writing-about-disability)
- [Conscious Style Guide](https://consciousstyleguide.com/)
- [Contributor Covenant, version 2.1](https://www.contributor-covenant.org/version/2/1/code_of_conduct/)

The community-conduct section follows the structure of the Contributor Covenant 2.1. The language guidance is original to this pack and draws on the style guides above.

This document is part of the pack and is licensed under [CC BY-SA 4.0](LICENSE), like the rest of the content.
