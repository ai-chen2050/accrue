---
title: Why Local-First and On-Device SQLite: Defending Data Sovereignty in the Age of LLMs
date: 2026-09-20
summary: While most modern note-taking apps push user data to centralized clouds, we chose a pure on-device architecture powered by SQLite and local Markdown. Here is our engineering rationale for achieving millisecond bi-directional link lookups, entity graph traversals, and zero-cost privacy in an offline-first environment.
tags: Local-First, Architecture, SQLite, Bi-directional Notes, Privacy
lang: en
order: 1
status: published
---

## Key Takeaway

**Thoughts and cognitive assets are irreplaceable digital possessions.** From day one, Accrue Notes made an uncompromising commitment: no centralized user databases, no proxy relay backends. All notes, bi-directional link topologies, entity indexes, and vector embeddings are stored 100% on your local device within SQLite and Markdown files. Cloud LLMs are accessed directly via BYOK (Bring Your Own API Key), ensuring complete transparency with zero telemetry intermediaries.

## The Problem with Cloud-Centric Note Tools

When architecting Accrue Notes, we scrutinized prevailing market solutions:

1. **Vulnerability of Centralized Services**: Server outages or sudden policy pivots can lock your thoughts away overnight. When subscriptions lapse, users often face paywalled exports or proprietary format lock-ins;
2. **Severe Privacy Hazards**: Mainstream "AI notes" demand that users upload personal journals, research briefs, and confidential memos to multi-tenant cloud clusters. Even with promised encryption, internal mishandling or unauthorized training on user data remains an ongoing risk;
3. **Latency and Offline Breakdowns**: High-speed trains, flights, or flaky Wi-Fi leave cloud notes frozen in infinite loading spinners or trigger corrupted sync merge conflicts, derailing deep focus.

## Architectural Trade-Off: SQLite Engine + Markdown Mirror

We evaluated three architectural paths:

| Approach | Advantages | Disadvantages | Decision |
| :--- | :--- | :--- | :--- |
| **Pure Loose Markdown Files** | Human-readable, directly editable by external editors | Bi-directional lookups and graph traversals become painfully slow beyond 5,000 notes | Used strictly for export & multi-device sync |
| **Single Local SQLite Database** | Millisecond SQL indexing, ACID transactions, instant graph walks | Difficult for everyday users to inspect single notes in file managers | Core runtime storage engine |
| **SQLite Engine + Markdown Mirror Sync** | **Combines SQLite's sub-millisecond query speed with open portability** | Requires atomic writes and dual persistence state synchronization | **Selected Architecture** |

With this dual-layer design, SQLite maintains optimized virtual tables for `notes`, `entities`, `links`, and `backlinks`, augmented by FTS5 full-text indexing and vector caches. Even with collections exceeding 10,000 notes, `[[WikiLink]]` auto-completions respond in under 3 milliseconds.

## Lessons Learned: Private Conflict-Free Sync

Our greatest engineering hurdle was multi-device synchronization without centralized servers. Rather than running a costly, privacy-compromising WebSocket server, we leveraged native private iCloud Drive containers and WebDAV. To resolve offline parallel edits without duplicate copies, we implemented a lightweight diff-based patching mechanism based on logical clocks and paragraph-level hashes, achieving seamless silent reconciliation.

## What's Next

We are optimizing vector quantization to compress multi-million-word knowledge embeddings into under 50MB of local smartphone storage.
