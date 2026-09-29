---
title: Engineering Hybrid RAG: When Semantic Vectors Meet Knowledge Graph Entities
date: 2026-09-24
summary: Relying solely on vector embeddings overlooks precise entity definitions, while simple keyword matching lacks semantic intuition. Here is how Synapse Note implements hybrid graph-vector scoring on mobile devices, and why white-box AI reasoning is non-negotiable.
tags: Hybrid RAG, Knowledge Graph, Vector Search, Thinking Models, White-Box AI
lang: en
order: 2
status: published
---

## Key Takeaway

**Black-box chatbots are the antithesis of rigorous thinking.** In knowledge inquiries, we refuse to accept generative hallucinations that pretend to know the answer. Synapse Note employs a custom **Hybrid RAG (Semantic Vectors + Entity Graph Topology)** pipeline, exposing the complete AI thinking process and source citation quotes directly to the user.

## The Pitfalls of Naive Vector Search

Most conventional AI note tools simply run generic vector embeddings across text chunks and dump the top results into an LLM context window:

1. **Entity Blindness**: When notes link `[[Occam's Razor]]` with `[[First Principles]]`, vector search often retrieves paragraphs sharing superficial vocabulary while missing the exact canonical definition;
2. **Lack of Logical Auditability**: When asked a strategic multi-hop question, standard models return plausible-sounding generalities. Users cannot verify which specific notes were referenced, making hallucinations dangerous in decision-making.

## Our Approach: Dual-Engine Hybrid Retrieval

```text
[User Inquiry / Research Report Topic]
       │
       ├──► Vector Engine: Local embedding cosine similarity recall (Top-K)
       │
       └──► Graph Engine: Extract [[Entities]], traverse 1st & 2nd-degree bi-directional links
               │
               ▼
       [Reranking & Context Filter with Graph-Topology Weighting]
               │
               ▼
       [White-Box Prompt: Enforce <thinking> chain-of-thought & [Ref] quotes]
               │
               ▼
       [Streaming UI: Real-time collapsible thinking pill + verifiable citations]
```

## Why White-Box Thinking Matters

In our latest release, the knowledge QA pipeline makes reasoning steps fully auditable. As the model synthesizes your knowledge base, every deduction step—
*"First extracting Taleb's definition of payoff convexity from [[Antifragility Notes]]..."*
*"Next cross-referencing inverted arguments in [[Munger Latticework]]..."*
streams live inside a collapsible `[🧠 Explored in Depth]` capsule. Once complete, it folds neatly into a clean, authoritative executive summary that you can inspect at any level of depth.
