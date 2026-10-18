# Limitations and Non-Claims

[English](limitations.md) | [Русский](limitations.ru.md)

This case study is intentionally narrower than the private project and should be read as an engineering narrative, not as a product release or operational guide.

## Evidence limits

- The case-study brief reports **33 tests on Ubuntu and 33 tests on Windows in the last saved CI run**. This historical result was not independently retrieved or rerun during preparation. It is offline regression evidence, not a live-system qualification.
- **Live GUI behavior is not demonstrated.** The showcase contains no screenshots, runtime captures, or interactive session.
- **Steam integration is not demonstrated.** No claim is made about authentication, process discovery, launch, restart, or interaction with Steam.
- **Telegram network behavior is not demonstrated.** The control layer is described as an abstraction; delivery, polling, retries under real network conditions, access control, and service availability are not established.
- **End-to-end buy/sell behavior is not demonstrated.** There is no claim that a real lot was bought, resold, settled, or reconciled.
- **Template OCR is not confirmed live.** Synthetic glyph tests validate mechanics such as segmentation and mask comparison, not recognition quality on real game frames. The evidence ledger records this as offline-only evidence.
- **`total_earned` and `total_profit` are estimated economics.** They are derived from configured or assumed values and a modeled fee/rounding policy, not from independently verified sale proceeds. The evidence ledger describes the estimate without exposing private source paths.
- The **original source code is private**. The curated documentation has been published publicly with the owner's authorization; no runtime or demo has been published. Future additions require separate approval and review. This package does not reproduce the source and should not be treated as a substitute for source access.

## Scope limits

- No claim of production readiness, profitability, reliability, safety, compliance, or suitability for unattended use is made.
- No performance, latency, accuracy, uptime, or return-on-investment benchmark is asserted.
- No account, platform, game, or messaging-service policy interpretation is offered.
- No operational launch, shutdown, recovery, or troubleshooting procedure is included.
- No credentials, tokens, chat identifiers, usernames, local paths, process details, exact coordinates, binary dependencies, logs, screenshots, or runtime state are part of this showcase.

## Interpretation

The strongest supported conclusion is modest: the private project contains separable engineering boundaries for screen interaction, OCR, persistence, supervision, and remote-control abstraction, with offline tests and a saved two-platform CI configuration. Everything beyond those boundaries requires new, appropriately redacted evidence and should be labeled as such.
