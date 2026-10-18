# Stalbroker

## Screen-based automation · OCR · State recovery

**Private implementation · Documentation showcase · Status reviewed 18 October 2026**

Stalbroker automates price-based purchase attempts in a desktop game's auction interface. It reads visible prices from screen images, compares them with a configured threshold, and coordinates input, notifications, and state updates. This case study explains the engineering behind that workflow; it does not distribute the bot.

## The engineering problem

A screen-driven workflow cannot assume that a click succeeded, that a price was read correctly, or that the application is still in the expected state. Stalbroker separates those concerns into screen interaction, recognition, purchase decisions, persistence, supervision, and a Telegram control layer.

## What is implemented

- **Image-to-price recognition.** OCR post-processing and a template-matching option with a Tesseract fallback. Synthetic tests cover template mechanics; real-screen template accuracy remains unverified.
- **Threshold-based purchase attempts.** Unreadable prices and prices above the configured limit are rejected before attempting a purchase. Visual confirmation drives the subsequent state update.
- **State recovery.** JSON writes use temporary-file replacement. Loading restores defaults where appropriate and starts with execution disabled. This does not guarantee a checkpoint after every purchase.
- **Supervision.** Restart checks, failure counters, exception handling, notifications, and terminal stop conditions are separated from price recognition.
- **Remote control abstraction.** Telegram transport, commands, menus, and conversational state are separate modules.

## Architecture

```text
Screen observation → Price recognition → Threshold decision
                                              │
                                              v
                                      Purchase attempt
                                              │
                                              v
                                      Visual confirmation
                                              │
                                              v
                                  Counters + estimated economics

Supervisor coordinates the loop, failure handling and stop conditions.
Persistence writes state at explicit save points, not after every purchase.
Telegram commands and notifications provide an operator-facing control layer.
```

The diagram describes the private implementation at a conceptual level. It is not an operational recipe or a live demonstration.

## Evidence and current status

Historical CI evidence reviewed during the **18 October 2026 source audit** records **33 passing tests on Ubuntu and 33 on Windows**. These are the same suite on two platforms, not 66 distinct tests. The suite covers offline logic including OCR mechanics, calculations, configuration, persistence, and image/template scoring.

The tests were **not rerun during preparation of this package**. They do not validate live GUI interaction, Steam integration, Telegram network behavior, or an end-to-end buy-and-resell cycle. Private CI evidence is summarized here; it is not publicly reproducible from these documents.

**Economic counters are estimates, not settled proceeds.** The purchase path derives `total_earned` and `total_profit` from an assumed resale value. Automated resale was not found in the inspected implementation, so this showcase makes no claim of verified profit or a complete trading cycle.

## Read the case study

- [Architecture and engineering decisions](docs/architecture.md)
- [Evidence ledger and verification scope](docs/evidence.md)
- [Known limitations](docs/limitations.md)

The current deliverable is a complete **text-only case study**. No video, screenshots, interactive demo, or public source code is included. Synthetic visual examples are candidates for a later addition, not available features.

## Publication boundary

The source stays private. This package was prepared locally; no GitHub repository was created or published as part of its preparation. It contains six Markdown files and no runtime, source export, configuration, logs, or credentials.

[Public-material allowlist](PUBLIC_ALLOWLIST.md) · [Public-material denylist](PUBLIC_DENYLIST.md)
