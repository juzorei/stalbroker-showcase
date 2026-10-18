# Architecture

[English](architecture.md) | [Русский](architecture.ru.md)

Stalbroker runs a supervised loop around a desktop auction interface. Screen interaction, recognition, purchase decisions, state storage, and Telegram control have separate responsibilities.

## Screen and OCR

The screen layer supplies images and input operations; it does not decide whether to buy. This keeps environment-dependent interaction separate from price checks.

OCR takes a price image and returns a number or an unreadable result. The template path binarizes the image strip, splits symbols at empty columns, normalizes glyphs, and compares masks. If any symbol scores below the threshold, it rejects the whole value. Template availability is checked explicitly; Tesseract is available as a fallback.

## Purchase decisions

The auction logic rejects unreadable prices and prices above the configured buyout threshold before attempting a purchase. A successful visual confirmation updates counters and estimated returns, then requests a notification. Insufficient balance stops the loop and saves state.

The estimates use an assumed resale value, a modeled fee, and rounding rules. They do not record completed sales.

## State storage

JSON helpers write to a temporary file and replace the target. If JSON is malformed, the reader attempts recovery and lets the caller use defaults even if retaining the damaged file fails. Loading bot state forces execution off. Conversational state is stored separately.

Saves happen at explicit state-change and shutdown points, not after every confirmed purchase. Shared module state and file replacement do not form a transactional store or guarantee safety under concurrent writes or power loss.

## Supervision

The runner handles restart checks, exceptions, stop-state updates, saves, and notifications. It counts failed restarts and eventually stops rather than retrying forever. An exception caught by the main loop also marks execution as stopped before reporting the failure.

## Telegram control

Transport handles requests and retries. Commands map operator actions to state changes; menus and notifications present the result. Update handling and saved conversational state are separate from transport.

## Data flow

```text
Screen → OCR → Threshold check → Purchase attempt → Visual confirmation
                                                          │
                                                          v
                                               Counters + estimates

Supervisor: continue, restart, or stop; save at explicit points.
Telegram: operator commands, menus, and notifications.
```

This describes the code's control flow, not a demonstrated live session. Test coverage and unverified behavior are listed in [Evidence](evidence.md).
