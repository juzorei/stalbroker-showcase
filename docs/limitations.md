# Limitations and unfinished connections

[English](limitations.md) | [Русский](limitations.ru.md)

These limits apply to the **18 October 2026** source-review snapshot. They distinguish implemented components from completed integrations and observed behavior. They do not reduce Stalbroker to the unrelated implementation described by the earlier showcase: the seller, multi-session controller, strategies, and companion services exist. See [Evidence](evidence.md) for that correction and the absence of a fresh test/runtime result.

## Trading is not one uniformly completed loop

### Generic trading has explicit stops

The generic collect-mail stage pauses before collecting. Active lots require an outcomes callback; without it, processing pauses, and the entrypoint supplies none. Its pricing pass supplies an empty rival set despite the fee/floor/undercut/hold/relist model. Together these prevent describing this route as a fully closed financial loop.

The sector strategy is different. Its own buy → collect-mail → shelter → median-listing → retry-remainder chain is connected in the source findings. The generic mail stop must not be applied to sector trading. Neither path establishes a continuously running cancellation/repricing loop for existing active lots.

### Listing and accounting are different events

SellEngine really manipulates inventory and posts lots, but a posted lot is not proof of sale. The event journal can record own purchases, listings, and outcomes; outcome support does not imply every caller supplies complete data. Treasury reservation, settlement, and equal splitting exist, but production settlement is not wired. Donate reuses splitting, not a complete shared-account reconciliation system.

Atomic local saving is not an atomic transaction spanning the game and disk. Deduplication and identifiers do not by themselves prove exactly-once game actions or complete financial recovery after interruption.

### Guard sets differ by entry path

Standalone sniping has median/manual caps, rank, same-name identity checks, fresh OCR, retargeting, and budget controls. Hotbuy checks candidate freshness, deduplicates, limits attempts, and invokes the sniper, but does not pass every standalone guard. Statements about the standalone path cannot be generalized to all sensor-triggered attempts.

### Some strategies stop at unfinished steps

- **Donate:** pause/count/distribute/sell and optional resume exist, including a hub-sale fallback. Mail-parcel item forwarding reaches an explicit unfinished stop, so end-to-end forwarding is partial.
- **Battle Kit:** expected-value calculation exists separately; the automatic bot role is unsupported, and automatic kit opening is not a delivered feature.
- **Sweep/sellout:** executor modules, previews, and panel/service request signals exist. Core entrypoints lack the worker consumer. A recorded request is not execution, and the buttons are not functioning end-to-end controls. Manual sell-all is a separate connected tool.
- **Player radar:** research only, not a delivered radar feature.

## “Dry” does not mean offline or side-effect-free

The seller's dry mode still moves inventory, splits stacks, and works with the sale form; it skips submission rather than all actions. Sector dry mode still collects mail. Neither is an offline simulator or a guarantee of no game-state effects. This repository intentionally provides no operating recipe for these modes.

## Perception, agents, and recovery need live acceptance

Specialist OCR, icons, anchors, caching, fresh reads, and UI/balance checks are source-described mechanisms, not measured accuracy on current game frames. Agent HMAC messages, process supervisors, resource/stuck watchers, heartbeats, relogin, and escalation are implemented paths, not newly observed recovery or comprehensive security validation.

The supervisor's staggered starts, backoff, and exclusion of stopped/fatal workers establish behavior in the implementation, not capacity or uptime. Fleet handling of locks, timeouts, staged restarts, and busy agents likewise does not establish a supported number of sessions or unattended suitability. Panels tolerate partial data and cache observations; displayed status can be incomplete or stale. Network Telegram controls and reports were not exercised for this rewrite.

## Market observations are not settled transactions

Lotsite consumes delayed market API data. “Fresh” refers to observation freshness relative to that source, not zero latency from the game. Early lot disappearance is a possible-sale heuristic, and expiration/disappearance handling cannot prove settlement between buyer and seller.

Variant histories, distributions, fee-adjusted profit/ROI estimates, and sensor candidate calculations remain market analysis. They must not be presented as the bot's realized proceeds. Conversely, own-operation journal outcomes are not merely the old showcase's assumed resale counters: they are a different record type, with their own integration limits.

History migration, backup, and rollback tools are implemented, but application of migrations and successful restoration were not demonstrated. Craftsite's recipe, batch, fuel, profit, and approximate leveling calculations depend on modeled inputs. Writing a recipe and buy ceilings to bot configuration is a real integration, not proof of completed crafting or sale. Its React/HTML options and the standalone Battle Kit calculator were not given fresh browser acceptance here.

Read-only MCP adapters are bounded developer analysis tools, not an autonomous trading product. Fleet tooling is not a commercial installer, bot license/seat service, or update system.

## Medsite has its own scope and limitations

Medsite is the separate companion SaaS «Медианы Аукциона», not a bot licensing backend. It reads Lotsite data. Public and premium views, including “sales,” inherit the evidentiary limits of that source. Its median is item-wide rather than exact-variant; zero additional tariff delay does not remove source delay or make the feed real-time.

### Access and payments

Account hashing, sessions, expiry extensions, grants, transactional promotion limits, provider confirmation, and idempotent payment/term handling are implementation findings. YooKassa and Telegram Stars operation depends on configuration and external services. No live payment, active subscription population, paid customer, or production deployment was established here. Recurring billing, refunds, and full financial reconciliation are not established features. A payment handler's existence is not evidence that revenue was received.

### Notifications and support

Medsite's Telegram linking, digests, expiry reminders, and admin alerts use bounded retries and global deduplication. They do not provide durable exactly-once delivery to every recipient.

The support backend saves an incoming message before notification and uses a separate limit. The UI is connected, but a known JavaScript scope bug can report failure after a successful save. Backend tests do not cover this frontend fault, and no fresh browser verification was performed. Thus the symptom does not necessarily mean data was lost. Support messages and administration do not amount to a full ticket lifecycle.

### Data and maintenance

Separate account/payment storage, SQLite WAL, request-scoped connections, read-only market access, consistent backups, and retention cleanup describe the service's design and tooling. They do not establish deployed backup schedules, successful recovery drills, privacy compliance, or a comprehensive security audit.

## Claims deliberately not made

No application or private test suite was run for this documentation rewrite, and no CI run was verified. Historical author-recorded test success is not a fresh pass claim. Static test inventory spans many subsystems but does not establish live UI, payment, notification, or deployment behavior.

There are no claims of production readiness, guaranteed profit, realized returns, uptime, performance, capacity, live OCR accuracy, paid-customer adoption, or suitability for unattended use. No permission under game/platform rules is implied. The public repository contains text-only documentation, not code, screenshots, runtime assets, launch instructions, credentials, or account procedures.

See the [feature catalog](features.md) and [architecture](architecture.md) for what is implemented, and the [allowlist](../PUBLIC_ALLOWLIST.md) and [denylist](../PUBLIC_DENYLIST.md) for publication rules. Return to the [overview](../README.md).
