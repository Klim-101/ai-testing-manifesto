# Contributing

Thank you for helping test this manifesto. The most valuable contribution is a concrete case where the text fails: a situation where following it to the letter still allows an unsupported conclusion, or where it adds cost without adding trust.

## Kinds of contribution

| Kind | How | What happens |
| --- | --- | --- |
| Counterexample | Open a *Counterexample* issue. | Discussed openly; may lead to an amendment or a new example in the rationale. |
| Amendment to the values or principles | Open an *Amendment* issue before any pull request. | Needs discussion, because it changes the commitments. Accepted amendments start a new version. |
| Rationale improvement (examples, practices) | Issue or pull request. | Reviewed more freely; the rationale changes more often than the core. |
| Language fix, typo, translation | Pull request. | Merged without a version bump if it does not change meaning. |
| Pilot report | Open an issue describing the context, what you measured and what did not work. | Linked from the rationale with your consent. |

## What a good amendment contains

1. The problem with the current text.
2. The proposed wording.
3. A practical example where the new wording leads to a better decision.
4. The principles and values it affects.

## Versions and translations

- Each language lives in its own folder: `en/` (reference text) and `ru/`. A change that alters meaning in `en/` must update `ru/` in the same pull request, or mark the translation as outdated until it is fixed.
- A new translation goes into a new folder named by its language code, for example `de/`, with the same file names.
- Endorsing one version does not carry over automatically to a changed version.
- Every release is recorded in [CHANGELOG.md](CHANGELOG.md).

## Credit and license

By contributing, you agree that your contribution is licensed under [CC BY 4.0](LICENSE), the same license as the rest of the text. Contributors are credited in the changelog. Names and roles appear in any list of participants only with explicit consent.

No single company or tool vendor has the final say over the principles. Do not use this repository to promote a product.
