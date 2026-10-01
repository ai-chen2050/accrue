---
title: Solving Math Formula Exports: High-DPI KaTeX Rasterization and Lossless Document Injection
date: 2026-09-26
summary: Traditional Markdown tools often turn LaTeX formulas into blurry pixelated images or corrupted glyphs during PDF and Word exports. Here is how we engineered a 4x supersampled vector rasterization and OpenXML structure injection pipeline on Flutter mobile.
tags: LaTeX, KaTeX, Export, PDF, Word, Rendering Pipeline
lang: en
order: 3
status: published
---

## Key Takeaway

Academic formulas and mathematical rigor are foundational to serious inquiry. In most note apps, LaTeX formulas look sharp on display, but when exported to PDF or Word (.docx), they degrade into unreadable low-res bitmaps or vanish completely. In Accrue Notes, we designed a **vector rasterization and OpenXML lossless mapping pipeline** that elevates document exports to journal-grade publishing standards.

## The Core Challenges

1. **Mobile Platform Layout Engine Limits**: Mobile frameworks lack built-in MathML or TeX vector layout engines;
2. **Missing Font Glyphs in PDF**: If standard PDF rendering streams lack specialized AMS math symbols, characters render as broken question mark boxes;
3. **Word (.docx) XML Alignment Nuances**: Microsoft Word requires precise baseline descent offsets for inline graphics; otherwise, formulas float uncomfortably above text lines or obscure surrounding words.

## Architecture: Dual-Channel Rasterization Pipeline

We integrated a headless KaTeX engine that triggers an offscreen rendering pass during document generation:

```text
Markdown Source
  ├── Inline Math: $E=mc^2$
  └── Display Math: $$\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}$$
       │
       ▼
[KaTeX Abstract Syntax Tree (AST) & Layout Geometry Measurement]
       │
       ├──► Calculate exact bounding boxes and baseline descent
       │
       ▼
[4x Supersampled High-DPI Offscreen Rasterizer]
       │
       ├──► PDF Export: Generate crisp alpha-channel images scaled to exact point dimensions
       │
       └──► Word Export: Insert native docx inline shapes with wp:inline and baseline shifts
```

## Performance Verification

With this pipeline, a 15-page research report containing over 50 complex matrix and calculus equations compiles to PDF in under 1.2 seconds. Even zoomed to 400% on Retina displays or exported to high-DPI print sheets, formula strokes remain razor-sharp and align harmoniously with running text.
