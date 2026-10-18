# Evidence Ledger

This ledger separates what is supported by repository artifacts from what remains unproven. It is intentionally conservative and does not treat a unit test as a live-system demonstration.

## Provenance and citation convention

Status snapshot: **18 October 2026**. The source audit reviewed a historical private CI run reporting 33 passing tests on each of Ubuntu and Windows, together with the workflow and test inventory. No new source tests or application modules were executed during showcase preparation. The result describes that historical revision, not a fresh qualification of the current runtime.

The entries below are an evidence summary for the private implementation, not public source citations. They describe the review scope and its limits without exposing the private module tree. Readers can assess the narrative here but cannot reproduce the private implementation or inspect its private CI logs from this package.

## Evidence by boundary

| Area | Evidence | What it supports | What it does not support |
| --- | --- | --- | --- |
| Cross-platform CI | The source audit reviewed a saved CI run with 33 tests passing on Ubuntu and the same 33 passing on Windows. No new run was performed for this package. The reviewed private workflow configured both runners and invoked the suite. | A reproducible offline test job was configured for both operating systems. | GUI, Steam, Telegram network, or buy/sell E2E behavior. |
| Test inventory | Six private test modules contain 33 test functions in total across item/config matching, OCR cleanup, template mechanics, persistence, profit calculations, and image/template scoring. This inventory is a static review note, not a fresh run. | The tested offline boundaries and their regression surface. | The quality of real game frames or external integrations. |
| OCR mechanics | Synthetic glyph tests cover multi-symbol reads, rejection of an unknown symbol, blank/incomplete glyph sets, engine selection, fallback behavior, and IoU. | Internal template/OCR mechanics on generated inputs. | Live template OCR. Template OCR is not confirmed live. |
| Persistence | Tests cover round-trip values, defaults for a missing file, corrupt-file recovery, temporary-file cleanup, and conversational state. | Expected offline state-file behavior. | Durability under real process termination, disk failure, or concurrent writers. |
| Economics | Profit helpers model a fee and rounding policy; the auction path derives `total_earned` from an assumed resale value and updates `total_profit`. | The existence of a deterministic estimate. | Realized proceeds, completed resale, or accounting accuracy. `total_earned` and `total_profit` are estimated economics. |
| Supervision | The runner records restart reasons, counts failed restarts, catches loop exceptions, persists stopped state, and reports terminal conditions. | The intended supervised control flow. | Live recovery under a desktop/game failure. |
| Telegram abstraction | Transport, command processing, menu rendering, and notifications are separated into distinct layers. | A layered control abstraction. | Telegram network E2E, delivery guarantees, or real credentials/access. |
| GUI / Steam / E2E | No showcase artifact runs the original project, opens the GUI, contacts Steam or Telegram, or performs a buy-sell flow. | A clear non-claim boundary. | Any live integration claim. |

## Evidence policy

- The source repository is private.
- The evidence summary above is intentionally non-navigational; no implementation is copied into this package.
- No screenshot, log, runtime state, secret, credential, username, token, chat identifier, exact coordinate, process command, or operational launch instruction is evidence in this package.
- “33 tests on Ubuntu and Windows” refers to the last saved CI result reviewed during the source audit; it was not rerun for this package. The static test inventory is consistent with 33 named test functions. The showcase does not run the source project.
- “Passed” is not generalized into “production-ready.” Live GUI/Steam/Telegram network/E2E buy-sell behavior remains unproven.
