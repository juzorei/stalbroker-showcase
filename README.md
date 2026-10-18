# Stalbroker

[English](README.md) | [Русский](README.ru.md)

Stalbroker reads prices from a game's auction screen and attempts purchases when the price is within a configured limit. It combines screen input, OCR, saved state, supervision, and Telegram controls.

## How it works

- **OCR** converts a price image into a number. It includes post-processing, template matching, and a Tesseract fallback.
- **Purchase logic** rejects unreadable prices and prices above the limit. Visual confirmation triggers counter updates and a notification request.
- **State** is stored in JSON through temporary-file replacement. Loading restores defaults where needed and leaves execution disabled.
- **Supervision** handles restart checks, failure counts, exceptions, notifications, and stop conditions.
- **Telegram** provides commands and menus, with transport and conversational state kept separate.

## What was checked

The **18 October 2026 source audit** reviewed saved private CI results: **33 tests passed on Ubuntu and the same 33 on Windows**, not 66 different tests. They cover offline OCR mechanics, configuration, calculations, persistence, and image/template scoring. They were not rerun for these docs. The public repository cannot reproduce the private CI run.

These tests do not establish live GUI, Steam, or Telegram network behavior, or an end-to-end buy-and-resell cycle. Template OCR tests use only synthetic glyphs; they do not establish live recognition accuracy.

`total_earned` and `total_profit` estimate returns from an assumed resale value; they are not realized profit. Automated resale was not found in the inspected implementation.

Atomic JSON replacement does not guarantee safe concurrent writes or power-loss durability. State is saved at explicit points, not after every purchase.

## Read more

- [Architecture](docs/architecture.md) — components and data flow
- [Evidence](docs/evidence.md) — what the audit and tests support
- [Limitations](docs/limitations.md) — what remains unverified

The source stays private. This repository contains documentation only: no runnable bot, demo, screenshots, or video. Publication rules are linked below.

[Public-material allowlist](PUBLIC_ALLOWLIST.md) · [Public-material denylist](PUBLIC_DENYLIST.md)
