# Public Material Allowlist

This is a review policy for possible future showcase additions. Inclusion here is **not permission to publish**. The current package is local-only, text-only, and contains only the six files listed below.

## Current materials

- `README.md`
- `docs/architecture.md`
- `docs/evidence.md`
- `docs/limitations.md`
- `PUBLIC_ALLOWLIST.md`
- `PUBLIC_DENYLIST.md`

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
