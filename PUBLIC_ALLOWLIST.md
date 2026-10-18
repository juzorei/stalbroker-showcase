# Public material allowlist

[English](PUBLIC_ALLOWLIST.md) | [Русский](PUBLIC_ALLOWLIST.ru.md)

The owner-approved publication scope is the text-only Stalbroker showcase below. It documents the correct project's **18 October 2026** source-review snapshot: trading core, session control, data/web ecosystem, and the separate Medsite companion SaaS. Private source remains private. No executable version, demo, media, or operating guide is included.

## Exact current manifest

Exactly **14 Markdown files** are allowed: seven English documents and seven complete Russian counterparts. The feature catalog is part of this approved rewrite, not permission to add runtime material.

- `README.md`
- `README.ru.md`
- `docs/features.md`
- `docs/features.ru.md`
- `docs/architecture.md`
- `docs/architecture.ru.md`
- `docs/evidence.md`
- `docs/evidence.ru.md`
- `docs/limitations.md`
- `docs/limitations.ru.md`
- `PUBLIC_ALLOWLIST.md`
- `PUBLIC_ALLOWLIST.ru.md`
- `PUBLIC_DENYLIST.md`
- `PUBLIC_DENYLIST.ru.md`

## Allowed content in these documents

- **Product explanation:** Stalcraft trading, shared UI engines, strategies, multi-session control, market data, calculators, dashboards, developer tools, and Medsite, described in original high-level prose.
- **Conceptual architecture:** responsibilities, dependencies, and data/control flow without implementation excerpts, private paths, commands, coordinates, or account procedures.
- **Feature status:** connected, standalone, partial, and research distinctions. A signal writer must not be described as a working worker consumer; a model or calculator must not be promoted to an executed strategy.
- **Evidence summaries:** supplied source-review findings, the test areas identified, explicit provenance limits, and the absence of a fresh application/test/CI verification. Historical success is not current success.
- **Corrections and limitations:** the earlier showcase described a different codebase; its “33 tests” and “resale absent” statements do not describe Stalbroker. Own-operation journal outcomes, listing results, market heuristics, and financial estimates must remain distinct.
- **Service scope:** Medsite is a separate analytics/subscription service consuming read-only Lotsite data, not bot licensing. Payment and account mechanisms may be explained conceptually without access details or deployment claims.

## Review rules for changes

Keep all seven language pairs complete. Every file must have an English/Russian switch; Russian documents link to Russian counterparts except for that deliberate language switch. Use local links to public documents only, and keep this exact manifest synchronized in both languages.

Preserve the specific caveats in [Evidence](docs/evidence.md) and [Limitations](docs/limitations.md), including incomplete generic mail/outcomes, separate sector mail, missing sweep/sellout consumers, Hotbuy guard differences, partial parcel forwarding and settlement, dry-mode side effects, market-sale heuristics, delayed data, and Medsite's known support UI issue. Do not replace these with a generic disclaimer that hides their impact.

New claims require supporting evidence and review. Any additional file, code, media, runtime artifact, external/private reference, or expansion of publication scope requires separate explicit owner approval after content and ownership review. A synthetic image, mock, raw log, or copied snippet is not automatically allowed because it is labeled or redacted; none is in the current manifest.

Apply the [denylist](PUBLIC_DENYLIST.md) before publication. Review must preserve the distinction between source implementation, actual wiring, test inventory, and observed runtime behavior. Return to the [overview](README.md).
