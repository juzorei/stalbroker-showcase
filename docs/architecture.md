# Architecture Notes

## Framing

The private project is best understood as a supervised, screen-driven workflow rather than a general-purpose trading service. It observes a desktop auction interface, extracts a price from a bounded image region, makes a threshold decision, and records the resulting state. Telegram is a control abstraction around that workflow, not evidence of a public service.

## Boundaries

### 1. Screen and input boundary

The control boundary isolates screen observation and input operations from auction decisions. The separation is valuable because screen interaction is inherently environment-dependent: decision logic can be reasoned about separately from the mechanism that supplies pixels and input events. The [evidence ledger](evidence.md) records this as a conceptual boundary without exporting the private implementation structure.

This showcase intentionally omits exact coordinates, window titles, process-management details, and operational launch steps.

### 2. OCR boundary

The OCR boundary exposes a narrow “image to price” contract. Its template path binarizes a strip, splits symbols on empty columns, normalizes glyphs, compares masks, and rejects the entire value when a symbol falls below the configured score. A Tesseract path is available as a fallback, and template availability is explicit. The [evidence ledger](evidence.md) summarizes this behavior without exporting private source paths.

The design reduces ambiguity at the decision boundary: a partial or uncertain price is not silently converted into a buy candidate. However, the template path is only validated against synthetic glyphs in the available test evidence; it is not confirmed live. See the [evidence ledger](evidence.md) for the exact claim boundary.

### 3. Auction decision boundary

The auction layer rejects an unreadable price and rejects prices above the configured buyout threshold before attempting a purchase. On a successful visual confirmation, it updates counters and estimated economics and requests a notification; a terminal insufficient-balance condition stops the workflow and saves state. The economics are estimates derived from an assumed resale value and a modeled fee and rounding policy. They are not proof of completed resale or realized profit; see the [evidence ledger](evidence.md).

### 4. Persistence boundary

Persistence is isolated behind JSON read/write helpers. Writes use a temporary file followed by replacement. On malformed JSON, the reader attempts recovery and returns control to caller defaults, even if retention fails. Loading bot state forces execution to start disabled, while conversational state is stored separately. Atomic replacement is not a concurrency or power-loss durability guarantee; the [evidence ledger](evidence.md) states this boundary explicitly.

### 5. Supervision boundary

The runner owns the long-lived loop and consolidates restart checks, exception handling, stop-state updates, persistence, and operator-facing notifications. A failed restart is counted and eventually becomes a controlled stop rather than an unbounded retry. An uncaught loop exception also transitions the state to stopped before reporting the failure. This is a design claim, not live recovery evidence.

This demonstrates supervision logic in the codebase; it does not prove that a live game process, desktop session, or external service remains healthy under real conditions.

### 6. Telegram control abstraction

The Telegram side is layered into transport, update/command handling, menus, notifications, and persisted conversational state. Transport owns request/retry boundaries, commands map control intents to state changes, and menus form the presentation abstraction. The [evidence ledger](evidence.md) records this separation without exposing the private module tree.

This is intentionally described as an abstraction. The available evidence does not establish Telegram network reliability, delivery semantics, production access control, or end-to-end operation.

## Data flow

1. A supervised loop requests a screen observation through the control boundary.
2. The OCR boundary returns a price or an explicit unreadable result.
3. The auction boundary compares the value with configured policy.
4. A successful confirmation updates counters and estimated economics.
5. Persistence writes the current state through an atomic boundary.
6. Notifications and Telegram menus expose a summarized control surface.
7. The runner continues, restarts according to policy, or moves to a stopped state on a terminal condition.

This flow is conceptual, not a transaction guarantee. Persistence occurs at explicit state-change and shutdown boundaries; the purchase path does not save a checkpoint after every successful confirmation. Shared module state and filesystem replacement are not a transactional store. This limitation is part of the [evidence ledger](evidence.md), not a promise of durability.

The original source remains private. This document is a curated description and does not reproduce implementation code.
