# Evidence and claim provenance

[English](evidence.md) | [Русский](evidence.ru.md)

## Identity correction

**An earlier showcase described a different codebase.** Its statement that “33 tests” passed on two operating systems and its conclusion that automated resale was absent were not evidence about Stalbroker. Neither claim is carried forward as a Stalbroker finding. The earlier small OCR-loop and estimated-return narrative is replaced, rather than extended with features from an unrelated implementation.

For Stalbroker, the supplied source findings identify an inventory-aware seller used by several strategies, an own-operation journal with purchases/listings/outcomes, multi-session control, and a substantial market/web ecosystem. Implemented listing capability corrects “resale absent”; it does not establish that a live buy-to-sale financial loop completed successfully.

## Scope and method

The snapshot date is **18 October 2026**. This rewrite uses source-review findings supplied for the correct private project, including a separate review of the ecosystem. The documentation editor read the existing public documents and worked only on this showcase. Private source was not reread, edited, or executed for this rewrite.

The public repository contains no source, test suite, runtime, screenshots, or raw review artifacts. Readers cannot independently reproduce private source findings from these documents alone. Provenance here is a transparent summary of supplied findings, not line-level public citations or a claim that the editor performed another source audit.

Four kinds of statement are kept distinct:

1. **Implementation found:** a component or calculation exists.
2. **Connection found:** an entrypoint/caller invokes it, or a service consumes its output.
3. **Test inventory found:** tests target particular behavior; this is not a passing result.
4. **Runtime result observed:** live acceptance, deployment, performance, payment settlement, or successful recovery. No new result of this kind was produced here.

“Connected” in the [catalog](features.md) means the second category, never the fourth. “Standalone” means a separate implemented tool/service, not proven deployment. “Partial” records a specific missing step; “research” does not claim a delivered feature.

## What the source findings support

| Area | Supplied implementation/integration evidence | What it does not establish |
| --- | --- | --- |
| Buyer and perception | Per-unit singles/packs, budgets, fresh rereads, UI/balance result checks, reservations; specialist digits/rows/quantities/balance, icons, anchors, caching | Live recognition accuracy, purchase success rate, or game/disk atomicity |
| Seller | Inventory discovery, stack transfer/splitting, leftovers, listing series with price/term/quota/cooldown; reuse across trading, sector, craft, Donate, and manual sell-all | A posting is not a confirmed sale or realized profit |
| Generic pricing/trade | Fee/floor/undercut/hold/relist model; empty rivals passed; mail pause; active-lot outcome callback missing at entrypoint | Closed financial loop or continuous cancellation/repricing of existing lots |
| Sector strategy | Sector selection, Lotsite medians, fresh API quotes, screen/rank/capital/margin checks; buy/mail/shelter/list/remainder chain | Live profitability or continuous active-lot repricing; its mail path must not be conflated with the generic pause |
| Sniper and sensors | Standalone median/manual/rank/identity/OCR/retarget/budget guards; sensor freshness/dedup/attempt handling and Hotbuy invocation | Every standalone guard being propagated through Hotbuy; delivered player radar |
| Craft and Donate | Craft material/station/sale/debt route with distinct errors; pause/count/distribute/sell/resume and hub fallback | Automatic Battle Kit opening or completed parcel forwarding |
| Treasury | Reservation, settlement, equal split and associated tests; split reused by Donate | Production-wired settlement or comprehensive account reconciliation |
| Agent and recovery | Separate standard-library/WinAPI agent, HMAC messages, IDLE assembly; escalation, resource/stuck watchers, heartbeat, self-healing, relogin | Security certification, observed recovery, uptime, or supported fleet capacity |
| Account coordination | Per-account supervisor, staggering, state/commands, restart backoff, stopped/fatal exclusions, shelter invitation/acceptance | A demonstrated number of concurrent sessions or unattended reliability |
| Journal | IDs, deduplicated purchases/listings/outcomes, atomic saving | One transaction spanning game and disk, or complete outcome reporting from every strategy |
| Controls and panels | Telegram controls and summaries; local FastAPI dashboard; telemetry, cache/partial-data tolerance, assignments, name/median resolution, restart requests | Complete/fresh telemetry or end-to-end sweep/sellout: those request consumers are absent from core entrypoints |
| Lotsite | Catalog/current lots, variant histories/distributions, stable-key parallel polling, first-seen/expiry/disappearance/history handling, estimates, maintenance tooling | Real-time source data, confirmed sales inferred from disappearance, or applied migration/restore proof |
| Craftsite and Battle Kit | Recipe/batch/fuel/leveling estimates, direct recipe and buy-ceiling assignment, optional React/HTML UI; standalone expected-value route | Successful real-world production, exact leveling predictions, or a supported kit-opening bot role |
| MCP and fleet tools | Read-only bounded data analysis; provisioning, session health, locks, timeouts, staged restarts/progress, busy-agent handling | Autonomous product agent, commercial bot installer, licenses/seats, update platform, or measured deployment scale |
| Medsite market product | Separate SaaS consuming read-only Lotsite data; public and premium views, time-cutoff access, metadata, item-wide medians | Bot licensing, exact variant medians, real-time data on a zero-delay tariff, or confirmed market sales |
| Medsite accounts/payments | scrypt, sessions, expiry/admin, grants/promos; YooKassa refetch/IDs/idempotency; Stars invoice/precheckout/success/idempotent extensions | Configured production operation, customers, settled revenue, recurring billing, refunds, or full reconciliation |
| Medsite operations | Separate Telegram linking/digests/reminders/alerts; retries/dedup; administration; support save-before-notify; SQLite WAL/request connections, read-only market data, backup/retention tools | Exactly-once delivery per recipient, a complete ticket lifecycle, deployed backup/restore success, or frontend correctness |

## Test evidence is an inventory, not a fresh result

The supplied review identifies tests around these areas:

- **Trading and UI logic:** buyer, seller, mail, sector strategy, sniper, crafting, squad coordination, and agent protocol.
- **Execution and data:** recovery, pricing, and storage.
- **Services and integration:** panels, authentication, migrations, payments, Telegram Stars, promotions, support, fleet tooling, and craft assignment.

This breadth is useful evidence of intended contracts and regression targets. It is not a report that those tests passed during this task. A historical author-recorded pass statement exists, but it is not a fresh verification result; no test-count badge or current pass count is published here. No CI run was supplied or verified for this rewrite, and no private tests were executed.

Test coverage also has boundaries. Backend support tests do not cover the current frontend JavaScript scope bug, which can display failure after the message was saved. Static inspection of a button, a signal writer, and an executor module does not prove that a worker connects them. A tested calculation does not establish that a game action, provider callback, or notification completed in a live environment.

## Financial and market evidence are different

| Record or output | Meaning | Do not infer |
| --- | --- | --- |
| Own-operation journal event | The bot's recorded purchase, listing, or supplied outcome, subject to caller integration | That every strategy supplies complete outcomes or all proceeds are reconciled |
| Successful listing result | An item was reported as posted by the execution path | A completed sale or realized profit |
| Lotsite early-disappearance classification | A market-observation heuristic for a possible sale | Confirmed buyer/seller settlement |
| Lotsite/Craftsite/Battle Kit estimate | A calculation using prices, fees, recipes, probabilities, or other modeled inputs | Earned income, guaranteed return, or observed crafting success |
| Medsite market/sales view | A presentation of market data with access/time restrictions | More authoritative transaction evidence than the underlying source |
| Medsite payment handling | Implemented provider confirmation and access-extension logic | Proven paid customers, recurring billing, or full financial reconciliation |

The previous showcase's estimated-return counters are not used to describe Stalbroker's journal. Conversely, the journal's outcome capability must not be used to promote market estimates into actual trading results.

## What was and was not checked for publication

Documentation checks concern the 14-file manifest, language counterparts, local links, claim consistency, and exclusion of private/operational material. They are not application acceptance tests. No live GUI trading, session recovery, network notification, payment flow, deployment, or performance benchmark was run for this rewrite. No uptime, profit, throughput, capacity, or paid-customer claim follows from this snapshot.

The [limitations](limitations.md) collect the actionable gaps in these findings. The [allowlist](../PUBLIC_ALLOWLIST.md) and [denylist](../PUBLIC_DENYLIST.md) define what may be published. See also the [architecture](architecture.md) and [overview](../README.md).
