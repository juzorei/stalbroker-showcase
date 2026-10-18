# Stalbroker

[English](README.md) | [Русский](README.ru.md)

Stalbroker is a modular Python system for Stalcraft auction automation: finding purchases, moving inventory, posting items for resale, coordinating Windows sessions, and recovering interrupted work. Around that core are market-data services, calculators, operator dashboards, and a separate subscription analytics product, **Medsite — «Медианы Аукциона»**. The interesting engineering is how these pieces connect: reusable UI engines do the physical work, strategies decide what to trade or craft, and journals and supervisors keep track of execution.

This repository documents the private implementation at the **18 October 2026** snapshot. It contains public, bilingual technical writing, not executable software or an operating guide. Implementation and integration statuses come from the supplied source-review findings; no application, private test suite, or live session was run for this rewrite.

## Trading through a real interface

The buyer handles inexpensive single items and packs using per-unit prices, budgets, fresh screen reads, and interface/balance checks. Purchases feed an event journal, while inter-account reservations coordinate competing work. Recognition is specialized for auction rows, digits, quantities, balances, inventory icons, and interface anchors, with content caching and explicit fresh reads where stale observations matter.

The seller is a substantial engine, not a proposed feature. It finds inventory icons, carries stacks into the listing form, splits portions, returns leftovers, and sends listing series with price, term, quota, and cooldown handling. Trading, sector, crafting, donation, and manual sell-all paths reuse it. Posting a lot is still different from observing a completed sale.

A pricing model accounts for fees, floors, undercutting, holding, and relisting. The generic trading path does not complete the whole financial cycle: it pauses before mail collection, and active lots need an outcomes callback that its entrypoint does not supply. It also passes an empty rival set to pricing. These are specific integration gaps, not evidence that selling is absent.

## Strategies built on shared engines

- **Sector trading** combines item sectors, Lotsite medians, fresh market API quotes, screen/rank checks, and capital/margin constraints. Its own chain buys, collects mail, returns to shelter, lists at the median, and retries unlisted remainder. It does not inherit the generic path's mail pause.
- **Standalone sniping** combines a dynamic median ceiling with manual caps, rank and identity checks, fresh OCR, retargeting, and budgets. A Hotbuy sensor adapter invokes the sniper with freshness, deduplication, and attempt limits, but does not forward every standalone guard.
- **Crafting** connects material purchases, shelter/station interaction, crafting, selling, and remainder debt, distinguishing energy, material, and window failures. An automatic Battle Kit role is unsupported; the calculator is a separate tool.
- **Donation** coordinates pausing, counting, distribution, selling, and optional resumption. A hub-sale fallback exists, but item forwarding through mail parcels stops at an explicit unfinished step.

## One controller, multiple sessions

A Python “brain” delegates capture, input, and clipboard work to a separate standard-library/WinAPI “hands” agent over HMAC-signed messages. The main assembly connects buyer, seller, mail, trader or crafter, reservations, scheduling, recovery, and Telegram, and starts in **IDLE**.

Per-account supervision provides staggered starts, state/command exchange, restart backoff, and no automatic restart of stopped or fatal workers. Shelter invitations and acceptance are wired. Recovery includes escalation, resource and stuck watchers, worker heartbeats, and a relogin service. Treasury reservation, settlement, and equal-split logic exist, but production settlement is not connected; donation reuses the split calculation.

Telegram exposes start/stop, items, prices, limits, status, reports, screenshots, account summaries, and worker starts. A local FastAPI dashboard and web panels add account telemetry and work assignment. Sweep/sellout previews and request signals exist, but core entrypoints have no worker consumer for them: they are not working end-to-end buttons. Manual sell-all is a distinct connected tool.

## Market data and companion products

**Lotsite** presents current lots, variant histories, distributions, and fee-adjusted profit/ROI estimates. Its poller handles pagination, parallel ingestion, stable lot identities, first-seen tracking, and history deduplication. Early disappearance is a possible-sale heuristic, not a confirmed transaction; upstream data is delayed.

**Craftsite** calculates recipes, batches, fuel, and approximate leveling economics, and can assign recipes and buy ceilings to the bot. A standalone **Battle Kit calculator** models expected value. Bounded read-only SQLite and market API MCP adapters support analysis, while fleet tooling handles Windows provisioning and session lifecycle rather than commercial installation or licensing.

**Medsite** is a separate companion SaaS in the same private repository. It consumes read-only Lotsite data and offers public catalog pages plus premium market, sales, search, and journal views. Its accounts, subscriptions, YooKassa and Telegram Stars payments, promotions, notifications, and administration belong to that service—not to a bot-license system. Zero tariff delay does not make its source real-time.

## Evidence and further reading

An earlier showcase described a different codebase. Its “33 tests” and “resale absent” statements do not describe Stalbroker. This rewrite replaces those claims, without turning source inspection into a live acceptance result. Own-trade journal outcomes are also distinct from market estimates.

- [Feature catalog](docs/features.md) — 25 grouped capabilities and integration status
- [Architecture](docs/architecture.md) — components, dependencies, and interrupted flows
- [Evidence](docs/evidence.md) — claim provenance and test inventory, without a fresh pass claim
- [Limitations](docs/limitations.md) — incomplete connections, dry-mode effects, and known issues
- [Publication allowlist](PUBLIC_ALLOWLIST.md) · [Publication denylist](PUBLIC_DENYLIST.md)
