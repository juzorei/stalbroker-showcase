# Limitations

[English](limitations.md) | [Русский](limitations.ru.md)

The docs describe code structure and offline checks. They are not an operating guide or evidence that the bot works reliably in a live session. The audit date, saved CI count, and test scope are recorded in [Evidence](evidence.md).

## Unverified behavior

- **GUI and Steam:** no demonstrated authentication, process discovery, launch, restart, or live interaction.
- **Telegram:** delivery, polling, retries on a real network, access control, and service availability remain unverified.
- **Template OCR:** synthetic glyph tests check segmentation and mask comparison, not accuracy on real game frames.
- **Trading:** purchase attempts do not establish a completed buy-and-resell cycle. Automated resale was not found in the inspected implementation. `total_earned` and `total_profit` use assumed resale values, fees, and rounding; they are estimates, not realized profit or reconciled proceeds.
- **Recovery:** atomic JSON replacement does not guarantee safe concurrent writes or survival of power loss, disk failure, or process termination. Saves are not made after every confirmed purchase.

## Claims not made here

There are no claims of production readiness, profitability, reliability, safety, compliance, or suitability for unattended use. There are no performance, latency, accuracy, uptime, or return-on-investment benchmarks, and no interpretation of account, platform, game, or messaging-service rules.

The source is private; the public docs include no runtime, demo, screenshots, or video. They provide no launch, shutdown, recovery, or troubleshooting procedures. Sensitive data and operational material are excluded under [the denylist](../PUBLIC_DENYLIST.md). New claims need new evidence; additions need review and owner approval under [the allowlist](../PUBLIC_ALLOWLIST.md).
