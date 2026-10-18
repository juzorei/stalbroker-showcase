# Public Material Denylist

[English](PUBLIC_DENYLIST.md) | [Русский](PUBLIC_DENYLIST.ru.md)

The following material must not be copied into this showcase or included in future additions without a separate, explicit scope change and review. The current curated documentation was published publicly with the owner's authorization; future additions require separate approval and review.

## Current materials

The package contains 12 Markdown files (six English documents + six Russian translations).

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

## Always excluded from this package

- **Secrets and access data:** credentials, passwords, tokens, session material, environment files, private keys, cookies, account identifiers, chat identifiers, and usernames.
- **Logs and runtime records:** application logs, CI raw logs, crash dumps, tracebacks with environment details, network traces, runtime JSON, persisted user/bot state, caches, and recovery files.
- **Game and desktop imagery:** game screenshots, live desktop captures, account/character images, extracted UI templates, OCR crops from the game, and any image that can reveal an account or operating context.
- **Operational details:** exact screen coordinates, process-management or process-kill commands, local installation paths, launch instructions, credentials setup, account setup, step-by-step automation procedures, timing/tuning recipes, and recovery procedures.
- **Local binaries and dependencies:** executables, wheels, virtual environments, native libraries, OCR models, downloaded tools, build outputs, and compiled caches.
- **Private implementation and history:** source code, copied code snippets, full configuration files, Git history, commit metadata, private repository URLs, and development-environment metadata.
- **Unsupported claims:** production-readiness labels, guaranteed profit, proven live OCR, verified live GUI/Steam/Telegram operation, or a completed buy-sell E2E claim without new evidence.

## Safe replacement principle

Replace excluded material with an independently written conceptual explanation, a clearly labeled synthetic example, a redacted summary, or a mock. Do not merely blur or partially mask a sensitive original when a clean synthetic substitute is possible.

The original source remains private. This package is a public curated case study, not an operational distribution. No runtime or demo has been published.
