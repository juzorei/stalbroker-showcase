# Evidence

[English](evidence.md) | [Русский](evidence.ru.md)

## Audit and saved CI

The **18 October 2026 source audit** reviewed a saved private CI run, its workflow, and the test inventory. The run recorded **33 passing tests on Ubuntu and the same 33 on Windows** — not 66 distinct tests. Six test modules contained 33 test functions.

No source tests or application modules were run for this documentation. The saved result describes the historical revision, not a fresh check of the current runtime. The source and CI logs are private: readers cannot inspect them or reproduce the run from this public repository.

## What the evidence covers

| Area | Reviewed evidence | Limit |
| --- | --- | --- |
| Offline CI | The workflow configured Ubuntu and Windows runners for the same suite. Tests cover item/config matching, OCR cleanup, templates, persistence, profit calculations, and image/template scoring. | No live GUI, Steam, Telegram network, or buy-and-resell E2E coverage. |
| OCR | Synthetic glyph tests cover multi-symbol reads, unknown-symbol rejection, blank/incomplete glyph sets, engine selection, fallback behavior, and IoU. | These test mechanics on generated inputs, not template OCR accuracy on game frames. |
| Persistence | Tests cover round trips, missing-file defaults, corrupt-file recovery, temporary-file cleanup, and conversational state. | They do not establish durability under process termination, disk failure, power loss, or concurrent writers. |
| Economics | Fee and rounding helpers calculate estimates. The purchase path updates `total_earned` and `total_profit` from an assumed resale value. | These are not verified sale proceeds or realized profit. Automated resale was not found in the inspected implementation. |
| Supervision | Code records restart reasons, counts failed restarts, catches loop exceptions, saves stopped state, and reports terminal conditions. | This describes intended control flow, not observed recovery from a live desktop or game failure. |
| Telegram | Code separates transport, commands, menus, and notifications. | This supports the component design, not network operation, delivery guarantees, or access control with real credentials. |

Atomic JSON replacement applies to individual saves. It does not provide transactions, concurrency protection, or power-loss durability, and the purchase path does not checkpoint every confirmed purchase.

No live GUI session, Steam interaction, Telegram network call, or buy-and-resell cycle was demonstrated for these docs. Passing offline tests does not establish production readiness. See [Limitations](limitations.md) for the remaining gaps and [the denylist](../PUBLIC_DENYLIST.md) for material excluded from publication.
