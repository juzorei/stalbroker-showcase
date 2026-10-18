# Public material denylist

[English](PUBLIC_DENYLIST.md) | [Русский](PUBLIC_DENYLIST.ru.md)

The [allowlist](PUBLIC_ALLOWLIST.md) defines the exact 14-file text-only publication scope. These exclusions cover the Stalbroker bot and every companion service, including Lotsite, Craftsite, fleet tools, and Medsite. Sharing a private repository does not grant blanket publication permission. Scope changes require explicit owner approval after review.

## Material not permitted

- **Private implementation:** source code, copied snippets, complete configurations, implementation dumps, extracted templates, source-derived assets, or a runnable reconstruction. High-level original prose is allowed; copying private code into a document is not.
- **Private references and history:** source paths, private repository/service URLs, commit hashes or metadata, internal identifiers, memory offsets, development-environment metadata, and private history. References to the public Markdown files in the allowlist are permitted.
- **Secrets and access data:** credentials, passwords, API keys, HMAC secrets, private keys, cookies, session data, environment files, account/chat identifiers, personal usernames, payment-provider secrets, and account-linking tokens. Naming a general mechanism such as HMAC or scrypt is not permission to expose its inputs.
- **Runtime and personal records:** raw application/CI logs, traces, crash dumps, saved bot/account state, journals, telemetry dumps, caches, recovery files, market database copies, account/payment databases, invoices, subscriber data, support messages, and backups. A conceptual description of these stores does not authorize publishing their contents.
- **Images and media:** screenshots, videos, live captures, desktop/game frames, OCR crops, inventory images, extracted UI templates, diagrams exported from private tooling, and synthetic media outside the approved text-only manifest.
- **Operational instructions:** launch, installation, account/credential setup, fleet provisioning steps, session lifecycle commands, process/kill commands, exact screen coordinates, window titles, local paths, timing/tuning recipes, recovery procedures, or step-by-step automation. Describing what a component does is different from explaining how to operate it.
- **Executable and build material:** binaries, dependencies, wheels, virtual environments, native libraries, OCR models, downloaded tools, built web bundles, scripts, demos, and compiled caches. None belongs to the current public manifest.

## Unsupported or misleading claims not permitted

- Reusing evidence from the different codebase described by the earlier showcase. The old “33 tests” and “resale absent” statements may appear only as explicitly rejected claims, not current Stalbroker evidence.
- Publishing a current test pass count, CI badge, live acceptance result, deployment claim, or security certification without the corresponding new verification. Test inventory and historical author statements are not fresh results.
- Promoting source wiring to observed reliability, or claiming uptime, throughput, capacity, profitability, guaranteed returns, paid customers, or production readiness from this snapshot.
- Equating a posted lot with a completed sale, market disappearance with confirmed settlement, or modeled profit/ROI with realized proceeds. Do not substitute the earlier project's assumed-return narrative for Stalbroker's own-operation journal.
- Hiding partial integrations: generic mail/outcomes, absent sweep/sellout consumers, unwired treasury settlement, unfinished Donate parcel forwarding, or Hotbuy's narrower guard propagation. Connected manual sell-all and sector mail must remain distinct from those gaps.
- Calling dry modes offline or side-effect-free, continuous active-lot repricing verified, Battle Kit automation supported, or player radar delivered.
- Presenting Medsite as bot licensing, its item-wide median as exact-variant pricing, or zero tariff delay as real-time source data. Payment handlers do not prove recurring billing, refunds, full reconciliation, revenue, or customers.
- Claiming durable exactly-once notifications, complete support ticketing, verified frontend correctness despite the known support scope issue, or demonstrated backup restoration without evidence.

## Safer public explanation

Use original conceptual prose and explicitly qualified source findings. Remove sensitive content instead of merely blurring or partially masking an original. A synthetic substitute, redacted artifact, or new file still needs separate approval; it does not bypass the manifest.

Preserve the corrections and provenance in [Evidence](docs/evidence.md), the status distinctions in the [feature catalog](docs/features.md), and the concrete gaps in [Limitations](docs/limitations.md). Keep English and Russian policies aligned. Return to the [overview](README.md).
