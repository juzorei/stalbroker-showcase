# Public Material Allowlist

[English](PUBLIC_ALLOWLIST.md) | [Русский](PUBLIC_ALLOWLIST.ru.md)

This is a review policy for possible future showcase additions. Inclusion here is **not permission to publish future additions**. The current curated documentation has been published publicly with the owner's authorization. The package is text-only and contains only the 12 files listed below (six English documents + six Russian translations); the source remains private, and no runtime or demo has been published.

## Current materials

- `README.md`
- `README.ru.md`
- `docs/architecture.md`
- `docs/architecture.ru.md`
- `docs/evidence.md`
- `docs/evidence.ru.md`
- `docs/limitations.md`
- `docs/limitations.ru.md`
- `PUBLIC_ALLOWLIST.md`
- `PUBLIC_ALLOWLIST.ru.md`
- `PUBLIC_DENYLIST.md`
- `PUBLIC_DENYLIST.ru.md`

## Future materials that may be prepared safely

Each future item requires its own review and explicit publication approval.

1. **Synthetic OCR examples** generated from artificial glyphs or neutral shapes, with no game frame, user data, source asset, runtime capture, or claim of live OCR quality.
2. **A redacted architecture diagram** showing conceptual boundaries and data flow only. It must omit coordinates, identifiers, local paths, process commands, operational details, and private implementation text.
3. **A mock Telegram UI** rendered from invented content. It must be clearly labeled as a mock and must not contain real messages, account identifiers, credentials, chat identifiers, or network traces.
4. **CI evidence** reduced to a redacted result summary for the offline test matrix. It may state the recorded test count and operating systems, but must not expose raw logs, private repository links, usernames, secrets, environment dumps, or imply live GUI/Steam/Telegram/E2E coverage.
5. **Revised narrative documents** that maintain the same evidence boundaries, use only generic repository-relative file references, and distinguish observed facts from estimates and unproven behavior.

## Required review checks

- Confirm ownership and permission for every included artifact.
- Remove all sensitive and operational content listed in `PUBLIC_DENYLIST.md`.
- Keep the original source private unless the owner separately decides otherwise.
- Preserve the explicit non-claims: live GUI/Steam/Telegram network/E2E buy-sell are not demonstrated; template OCR is not confirmed live; `total_earned` and `total_profit` are estimated economics.
- Do not turn a saved CI result into an unsupported quality label.
