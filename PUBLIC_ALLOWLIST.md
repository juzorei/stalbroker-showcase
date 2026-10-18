# Public Material Allowlist

[English](PUBLIC_ALLOWLIST.md) | [Русский](PUBLIC_ALLOWLIST.ru.md)

The owner has approved publication of the current documentation. It is public and text-only; the source remains private. No runtime or demo is published.

## Current files

The exact manifest is 12 Markdown files: six English documents and six Russian translations.

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

## Before adding anything

Every addition needs content review and explicit owner approval. The current approval does not extend to future material, even if it fits one of these categories:

- **Synthetic OCR examples:** artificial glyphs or neutral shapes only; no game frames, source assets, runtime captures, user data, or claims of live accuracy.
- **Architecture diagrams:** components and data flow only; no private implementation text, coordinates, identifiers, local paths, process commands, or operating details.
- **Telegram mocks:** clearly labeled, with invented content; no real messages, account/chat identifiers, credentials, or network traces.
- **CI summaries:** recorded test counts and operating systems, with sensitive content removed; no raw logs, private links, usernames, secrets, or environment dumps.
- **Revised docs:** distinguish observed facts, estimates, and unverified behavior; use only generic repository-relative file references.

Check ownership and permission for each artifact, then apply [the denylist](PUBLIC_DENYLIST.md). Keep the source private. Preserve the limits in [Evidence](docs/evidence.md): offline CI is not live GUI/Steam/Telegram network or buy-and-resell E2E coverage; synthetic OCR tests do not establish live accuracy; `total_earned` and `total_profit` are estimates. A saved CI result is not a quality guarantee.
