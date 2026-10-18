# Architecture

[English](architecture.md) | [Русский](architecture.ru.md)

Stalbroker separates trading decisions, desktop actions, execution records, and market analysis. The **18 October 2026** source-review snapshot describes a modular bot plus several companion services—not a single OCR loop or a single web application. The following is a conceptual map, with no deployment or account setup instructions.

## 1. Controller and session agent

The Python controller is the “brain”: it assembles buyer, seller, mail, trader or crafter, reservations, scheduling, recovery, and Telegram. It starts in IDLE rather than immediately trading. A separate “hands” agent uses the standard library and WinAPI for screen capture, input, and clipboard work across Windows sessions. Controller/agent messages are HMAC-signed.

This separation keeps strategy code apart from session-local interaction. It also creates several independently observable layers: a process can be alive, its agent can be busy, and a trading job can be paused. Fleet health logic accounts for a busy agent rather than equating “not immediately available” with “dead.” HMAC is a protocol mechanism, not evidence of a complete security audit.

## 2. Perception and reusable action engines

The perception layer reads specialist digits, auction rows, prices, quantities, and balances, and locates inventory icons and interface anchors. Content caching supports repeated observations; fresh reads are requested for decisions that depend on the current screen. The buyer uses these observations with per-unit limits, budgets, interface/balance result checks, and inter-account reservations.

The seller encapsulates inventory work: find an item, move a stack into the form, split portions, return leftovers, and submit listing series under price, term, quota, and cooldown constraints. Trading, sector, craft, Donate, and manual sell-all callers reuse this engine instead of each implementing their own inventory routine. A seller result concerns listing execution, not necessarily a subsequent sale outcome.

## 3. Strategies compose the engines differently

| Route | Source-described chain | Important boundary |
| --- | --- | --- |
| Generic trading | Buyer/seller components plus pricing, mail and active-lot stages | Mail pauses before collection; active lots pause without an outcomes callback, which the entrypoint does not supply. Pricing receives no rivals. |
| Sector trading | Item sectors → Lotsite median and fresh API quotes → screen/rank and capital/margin checks → buy → mail → shelter → median listing → remainder retry | This is a separate mail-enabled chain, not the generic route. No continuous active-lot repricing is established. |
| Standalone sniper | Median ceiling and manual cap → rank/identity/fresh OCR checks → retarget/budget-constrained attempt | Hotbuy invokes the sniper but does not forward all standalone guards. |
| Crafting | Shelter → buy materials → station → craft → sell → remainder debt | Energy, materials, and window failures are distinct. Battle Kit automation is unsupported. |
| Donate | Pause/count → allocation → sale → optional resume | Hub-sale fallback is implemented; parcel item forwarding stops at an unfinished step. |

The pricing model contains fee, floor, undercut, hold, and relist concepts. These modeled operations must not be confused with a continuously running cancellation/repricing service. Remainder debt in sector/craft routes tracks unfinished listing work. Treasury separately provides reservation, settlement, and equal-split logic; settlement is not production-wired, while Donate reuses equal splitting.

## 4. Journals, state, and recovery

The own-operation event journal stores purchases, listings, and outcomes with identifiers, deduplication, and atomic saves. Three facts must stay separate:

1. A strategy can attempt a game action.
2. A result can be recorded in local state.
3. A later sale outcome can be supplied to the journal.

The journal's ability to represent outcomes does not close a caller's missing integration. Nor does atomic file replacement make the game action and the local write one transaction.

Recovery wiring includes escalation, resource monitoring, stuck watchers, self-healing workers, heartbeats, and a relogin service. A per-account supervisor staggers starts, exchanges commands/state, and uses restart backoff without restarting explicitly stopped or fatal workers. Shelter invitations and acceptance are connected. These are source-level recovery paths, not newly observed recovery results.

## 5. Control surfaces and execution consumers

Telegram controls the bot's start/stop, items, prices, limits, status, reports, screenshots, account summaries, and worker starts. A local FastAPI account dashboard and web panels show balances, daily spending, activity, heartbeat, pause/recovery telemetry, and cached partial-data views. Panels also assign modes, budgets, and items, resolve names/medians, and request restarts.

Sweep and sellout require special care in this map. Their executor modules exist; panels have previews and produce request signals. But no worker consumer is wired in the core entrypoints. A service or panel writing a signal does not bridge that gap. Manual sell-all follows a different connected tool path.

## 6. Market observation and planning

Lotsite ingests delayed market API data through paginated, parallel polling and stable-key upserts. First-seen tracking, expiry/disappearance handling, and history deduplication support current-lot views and quality/upgrade variant histories, including own/external variants. Catalogs, distributions, freshness indicators, and fee-adjusted estimates are analytical outputs. An early disappearance may be classified as a sale heuristic, not a proven financial event.

Bot strategies and sensor analytics consume market context, but the game UI remains a separate observation/action surface. Sensor candidates use variant medians, freshness, identity, and screen checks before Hotbuy invocation. Player-radar work remains research.

Craftsite turns recipes, ingredients, batches, fuel, and approximate leveling into estimates. Direct assignment writes recipe choices and buy ceilings for the bot. Its optional built React UI and HTML fallback are presentation alternatives. Battle Kit expected-value calculation is a standalone route. Read-only SQLite/market API MCP adapters expose schema, bounded SELECT queries, and history/price summaries as developer tools, not an autonomous trading agent.

## 7. Medsite is a separate service

Medsite, «Медианы Аукциона», shares the private repository but is not a bot licensing layer. It consumes read-only Lotsite files/data. Public feed/catalog/item pages and premium market/sales/search/journal views sit above time-cutoff access and metadata. Item-wide medians are not exact variant medians; tariff delay and upstream market delay are different concepts.

Its own account/payment SQLite database uses WAL and request-scoped connections, while the market database is read-only. Account handling includes scrypt hashing, sessions, administration, expiry extensions, and promotions with transactional limits. YooKassa confirmation refetches provider state and handles external IDs/idempotency. Telegram Stars has invoice, precheckout, successful-payment, and idempotent term-extension paths. Manual grants are separate from paid confirmation; recurring billing, refunds, and full reconciliation are not established.

Medsite's Telegram linking, digests, expiry reminders, and administrative alerts are separate from bot commands. Bounded retries and global deduplication do not guarantee durable exactly-once delivery per recipient. Administration also covers subscription, promotion, link, payment, audit, and support records. Support saves before notification under a separate limit; a known frontend scope bug can report failure after a successful save. Backup and retention tooling belongs to the service's maintenance layer, not to proof of deployment.

## 8. Conceptual dependency map

- **Bot controls → controller → strategy → perception/action engines → session agent → game interface.**
- **Own-operation results → event journal → strategy/status consumers**, subject to each caller's actual integration.
- **Market API → Lotsite observations/history → dashboards, strategies, sensors, calculators, read-only analysis tools.**
- **Craftsite assignment → recipe and buy ceilings → crafting configuration.**
- **Lotsite read-only data → Medsite publication/access layer**, with a separate identity/payment store and notification system.
- **Sweep/sellout panel request → signal; worker consumption missing in core entrypoints.**

Fleet provisioning/session tools sit alongside these paths with locks, timeouts, staged restarts, health checks, and progress reporting. They do not constitute a commercial installer, seat/licensing manager, or update system.

See the [feature catalog](features.md), [evidence](evidence.md), and [limitations](limitations.md), or return to the [overview](../README.md).
