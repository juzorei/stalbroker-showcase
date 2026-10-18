# Public Material Denylist

[English](PUBLIC_DENYLIST.md) | [Русский](PUBLIC_DENYLIST.ru.md)

The [allowlist](PUBLIC_ALLOWLIST.md) contains the exact file manifest and the owner's approval for the current docs. Future additions need separate review and owner approval. The exclusions below apply unless the owner explicitly approves a scope change after review.

## Do not include

- **Secrets and access data:** credentials, passwords, tokens, session data, environment files, private keys, cookies, account/chat identifiers, and usernames.
- **Logs and runtime records:** application or raw CI logs, crash dumps, tracebacks with environment details, network traces, runtime JSON, saved user/bot state, caches, and recovery files.
- **Game and desktop media:** screenshots, live captures, account/character images, extracted UI templates, game OCR crops, or other imagery revealing accounts or operating context.
- **Operating details:** exact screen coordinates, window titles, process-management or kill commands, local installation paths, launch/account/credential setup instructions, step-by-step automation, timing/tuning recipes, and recovery procedures.
- **Binaries and dependencies:** executables, wheels, virtual environments, native libraries, OCR models, downloaded tools, build outputs, and compiled caches.
- **Private source and history:** code or copied snippets, full configurations, Git history, commit metadata, private repository URLs, and development-environment metadata.
- **Unsupported claims:** production readiness, guaranteed profit, proven live OCR, verified live GUI/Steam/Telegram behavior, or completed buy-and-resell E2E without new evidence.

## Use a clean substitute

Where possible, write a conceptual explanation, generate a clearly labeled synthetic example or mock, or prepare a summary with sensitive content removed. Do not just blur or partly mask a sensitive original when a clean synthetic substitute is possible. Substitutes still need review and approval; they are not a way around this list.
