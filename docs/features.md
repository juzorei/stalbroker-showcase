# Feature catalog

[English](features.md) | [Русский](features.ru.md)

This catalog covers the **18 October 2026** source-review snapshot: the Stalbroker trading system, shared services, and companion products. It describes 25 capability groups, not 25 independently deployed products. Source code remains private; no runtime or test execution was performed for this documentation rewrite.

## Reading the statuses

- **Connected** — implementation and a caller or execution path are identified in the source findings. This is not live acceptance.
- **Standalone** — a separate tool or service is implemented; it is not automatically part of the bot's trading loop.
- **Partial** — useful implementation exists, but an explicit integration or execution step is missing.
- **Research** — exploratory work, not a delivered product feature.

A group can contain more than one status. In particular, a request producer is not an execution consumer, a modeled operation is not an observed result, and a listing is not a sale.

## Trading and inventory

### 1. Auction purchasing — Connected

BuyEngine selects inexpensive single items and packs, comparing per-unit prices against limits and available budgets. It rereads the screen before acting and checks interface/balance evidence afterward. Purchases connect to the event journal and inter-account reservations. These checks describe the purchase path; they do not establish live OCR accuracy or transactional guarantees across the game and local state.

### 2. Reusable inventory seller — Connected

SellEngine finds inventory icons, moves a stack into the sale form, splits it into portions, returns leftovers, and posts a series with price, term, quota, and cooldown handling. The same engine serves generic trading, sector trading, crafting, donation, and the separate manual sell-all tool. This is real listing implementation, correcting the earlier showcase's claim that resale was absent. A successful posting is not proof that another player bought the lot.

### 3. Pricing and the generic trading cycle — Partial

The pricing model includes fees, a price floor, competitor undercutting, holding, and relists. However, the generic pass supplies an empty rival set. Its collect-mail stage pauses before collecting, and active lots without an outcomes callback also pause; the entrypoint does not supply that callback. Buyer/seller components are connected, but this route is not a closed financial loop. The findings do not establish continuous cancellation and repricing of already active listings.

### 4. Sector trading — Connected

A separate strategy organizes items into sectors and combines Lotsite medians with fresh market API quotes. Screen/rank checks, margin thresholds, and capital constraints inform buying. Its chain is purchase → collect mail → shelter → list at the median → retry unlisted remainder debt. Here “debt” means work/items still awaiting listing, not a claim about a financial liability. This strategy has its own mail collection and must not be described as blocked by the generic path's mail pause. Continuous active-lot repricing is not established.

### 5. Standalone sniper and Hotbuy adapter — Standalone / Partial

The standalone sniper combines a dynamic median ceiling, a manual cap, rank and identity checks for same-name items, fresh OCR, retargeting, and budget control. Hotbuy consumes sensor candidates, checks freshness, deduplicates, limits attempts, and invokes the sniper. That adapter does not forward every standalone guard, so the standalone safety conditions cannot be attributed wholesale to sensor-triggered purchases.

### 6. Crafting execution — Connected

The crafting route connects shelter, material purchases, station interaction, crafting, listing, and remainder debt. It distinguishes insufficient energy, material problems, and window/interface failures instead of treating them as one generic error. The Battle Kit automation role is unsupported; the expected-value calculator in group 18 does not open kits or make that role operational.

### 7. Donation and distribution — Partial

The Donate flow can pause participants, count resources, distribute allocations, sell, and optionally resume work. Equal-split arithmetic is reused from treasury logic, and a fallback sale through the hub is implemented. Item forwarding through mail parcels reaches an explicit unfinished stop. The allocation and sale pieces therefore do not establish a completed end-to-end parcel distribution system.

### 8. Shared treasury — Partial

Reservation, settlement, and equal-split logic exist with associated tests. Production settlement is not wired into the operating flow. Equal splitting has an actual reuse path in Donate; the existence of settlement calculations must not be presented as automatic reconciliation of all accounts.

## Execution and operator control

### 9. Cross-session “brain and hands” — Connected

A modular Python controller delegates screen capture, input, and clipboard operations to a separate standard-library/WinAPI agent in Windows sessions. Messages carry HMAC signatures. The main assembly connects buyer, seller, mail, trader or crafter, reservations, scheduling, recovery, and Telegram, and starts in IDLE. This is a component/integration description, not a security certification or a launch recipe.

### 10. Specialized computer vision — Connected

Recognition includes specialist digit readers, auction-row prices and quantities, balance reading, inventory icons, and interface anchors. Content caching reduces repeated interpretation, while explicit fresh reads support decisions that must not rely on old images. It is a broader perception layer than the earlier showcase's small OCR-loop description. No measured live recognition rate is claimed.

### 11. Own-operation event journal — Connected

The journal records purchase, listing, and outcome events with identifiers, deduplication, and atomic saves. These are records of the bot's own operation flow, not Lotsite market estimates. Storage can represent outcomes without proving that every strategy supplies them: the generic route is missing its outcome callback. Atomic local saving does not make a game action and a disk write one transaction.

### 12. Recovery and supervision — Connected

Source wiring includes recovery/escalation, resource and stuck watchers, self-healing worker supervision, heartbeats, and a relogin service. These mechanisms address different failure layers rather than a single blind restart loop. Their presence is not fresh evidence of successful recovery from real session loss, game changes, or network failure.

### 13. Account squads and shelter coordination — Connected

A per-account process supervisor staggers starts, exchanges state and commands, and applies restart backoff. Explicitly stopped or fatal workers are not automatically restarted. Shelter invitation and acceptance paths are wired. This establishes coordination logic, not a tested fleet size, throughput limit, or unattended-operation guarantee.

### 14. Telegram and account dashboards — Connected

Bot Telegram controls cover start/stop, items, prices, limits, status, reports, screenshots, account summaries, and worker starts. A local FastAPI account dashboard and web panels expose balances, daily spending, activity, heartbeat, pause/recovery telemetry, and cached views tolerant of partial data. Panels assign modes, budgets, and items, resolve names/medians, and request job restarts. Producing or displaying telemetry does not guarantee it is complete or current.

### 15. Sweep, sellout, and manual sell-all — Partial / Connected

Sweep and sellout have executor modules plus panel previews and request signals. The core entrypoints have no worker-side consumer wiring for those requests. Even if a panel or service writes the signal, that is not evidence of execution: these buttons are only partially integrated. Manual sell-all is a distinct connected seller tool and must not be confused with the unfinished request paths.

## Market data and development tools

### 16. Lotsite catalog and market history — Standalone, with bot data consumers

Lotsite provides a market catalog, current lots, quality/upgrade variant histories, distributions, freshness indicators, and fee-adjusted profit/ROI estimates. Its poller handles pagination, parallel ingestion, upserts keyed by stable lot identities, first-seen tracking, expired/disappeared lots, and history deduplication across own and external variants. Early disappearance is a sale heuristic, not a confirmed financial transaction. Market API delivery is delayed, not real-time. History migration, backup, and rollback tooling exists; its existence does not prove a migration was applied or restored successfully.

### 17. Craftsite planning and bot assignment — Standalone / Connected

The calculator models recipes, ingredients, batches, fuel, profit estimates, and approximate leveling. Direct assignment writes a recipe and buy ceilings for bot work, connecting planning to execution configuration. The UI can use an optional built React frontend or an HTML fallback. Calculations and assignment do not demonstrate successful real-world crafting or sale at the estimated prices.

### 18. Battle Kit expected-value calculator — Standalone

A separate route calculates expected value from slots, probabilities, stacks, market prices, and fees. It is an analysis tool, not an automatic kit-opening workflow. The unsupported Battle Kit bot role in group 6 remains unsupported even though this calculator exists.

### 19. Read-only MCP analysis adapters — Standalone

SQLite and market API adapters expose schema inspection, bounded SELECT queries, and market history/price summaries. They are developer tools for reading and analyzing data, not an autonomous product agent, a bot-control plane, or an unrestricted database writer.

### 20. Sensor analytics and radar exploration — Connected adapter / Research

Sensor analytics parse candidate offers, compare variant medians, check freshness and identity, and use screen verification before feeding Hotbuy. The adapter limitation in group 5 still applies. Player-radar work is research only; it is not a delivered radar capability in this catalog.

### 21. Windows fleet tooling — Standalone

Provisioning and session-lifecycle tooling includes health checks, locks, timeouts, staged restarts, and progress reporting. A busy agent can be considered alive instead of being mistaken for a dead process. These tools are not a commercial installer, bot-seat manager, licensing service, or product update system. Deployment scale and runtime performance are not established here.

## Medsite: a separate companion SaaS

### 22. Market publication and subscription access — Standalone

Medsite, **«Медианы Аукциона»**, is a separate service in the same private repository. It consumes read-only Lotsite files/data rather than licensing the bot. Public pages include a feed, catalog, and item view; premium access adds market, sales, search, and journal views with time-cutoff access and metadata. Its median is item-wide, not an exact quality/upgrade-variant median. A paid tariff with zero additional delay does not remove the upstream source delay. A “sales” view based on market data does not turn disappearance heuristics into confirmed transactions.

### 23. Accounts, payments, and promotions — Standalone

Medsite has scrypt-hashed accounts, sessions, administration, expiry extensions, manual grants, and promotions with transactional limits. YooKassa confirmation refetches provider state and uses external identifiers/idempotency. Telegram Stars handles invoices, precheckout, successful-payment processing, and idempotent term extensions. These are configuration-dependent payment paths, not evidence of active customers or settled production revenue. Recurring billing, refunds, and full payment reconciliation are not established.

### 24. Notifications, administration, and support — Standalone, with a known UI issue

The service has its own Telegram account linking, digests, expiry reminders, and administrative alerts, separate from bot controls. Delivery uses bounded retries and global deduplication, not durable exactly-once delivery to every recipient. Administration covers subscriptions, promotions, links, payments, audit records, and support messages. The support backend saves before notification and has its own limit; the UI is wired, but a current JavaScript scope bug can report failure after a successful save. Frontend acceptance remains unverified, and this is not a complete ticket lifecycle.

### 25. Service storage and maintenance — Standalone

Medsite keeps its own account/payment SQLite database, uses WAL and request-scoped connections, and reads the market database read-only. Consistent-backup and retention-cleanup tooling exists. This separation distinguishes service identity/payment state from market observations and bot execution state; it does not prove a deployed backup schedule, a successful restoration, or a comprehensive security audit.

## Where to go next

[Architecture](architecture.md) explains how the components connect. [Evidence](evidence.md) distinguishes supplied source findings from test results and live behavior. [Limitations](limitations.md) collects incomplete paths, dry-mode effects, and unverified claims. Return to the [overview](../README.md).
