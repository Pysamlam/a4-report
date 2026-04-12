# A4 Report — Consulting-Grade Reports for Claude Code
> Generate professional A4 consulting reports in McKinsey / BCG / Bain style — zero design skills required, zero dependencies, print-to-PDF in seconds.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Claude Code](https://img.shields.io/badge/Claude%20Code-skill-blueviolet)
![Zero Dependencies](https://img.shields.io/badge/dependencies-zero-brightgreen)

**English** | [中文](README_CN.md) | [日本語](README_JA.md)

---

## What It Does

**A4 Report** is a Claude Code skill that turns your topic or data into a polished, print-ready consulting report. The output is a **single self-contained HTML file** — no Node.js, no Python, no build tools. Open in browser → Print → Save as PDF.

**Typical use cases:**
- Market analysis & competitive intelligence
- Strategic planning & feasibility studies
- Business reviews & board presentations
- Client proposals & due diligence summaries

---

## Quick Start

### Step 1 — Install

**Option A: Manual**
```bash
mkdir -p ~/.claude/skills/a4-report
cp SKILL.md STYLE_PRESETS.md a4-report-template.md ~/.claude/skills/a4-report/
```

### Step 2 — Invoke

Type `/a4-report` in Claude Code, then describe what you need:

```
/a4-report

帮我写一份中国新能源汽车市场分析报告，面向董事会，标准版。
```

```
/a4-report

Write a competitive intelligence report on the top 3 cloud providers,
McKinsey style, 10-15 pages, for internal strategy review.
```

### Step 3 — Get Your Report

Claude will guide you through a brief Q&A, generate the HTML file, and open it automatically. Print to PDF from your browser.

---

## How It Works — The 7-Phase Workflow

```
Phase 1: Content Discovery    → Audience, report type, purpose, length
Phase 2: Style Selection      → Preview 3 styles or pick directly
Phase 3: Report Generation    → Full HTML with inline CSS, zero deps
Phase 4: Chart Enhancement    → Add chart-guide + key-insights to every chart
Phase 5: Delivery             → Open in browser, ready to print
Phase 6: PDF Export (opt.)    → Step-by-step browser print guide
Phase 7: Data Audit (auto)    → Validates every number against source data
```

The skill asks exactly what it needs — no more, no less — then generates the complete report without interruption.

---

## Usage Guide

### Basic Usage — Topic Only

The simplest case: give a topic, choose a style, get a report.

```
/a4-report

Write a market entry report for Southeast Asia's quick commerce sector.
```

Claude will ask:
1. **Audience** — Who will read this? (C-Suite / Board / Business team / Consultant)
2. **Report Type** — Market analysis / Competitive intel / Strategic plan / etc.
3. **Purpose** — Investment decision / Board deck / Client proposal / etc.
4. **Length** — Brief (5-8 pages) / Standard (10-15 pages) / Comprehensive (20+)
5. **Style** — McKinsey Blue / BCG Silver / Bain Red (preview or direct pick)

### Advanced Usage — With Source Data

Upload or reference a data file and the skill activates **automatic data audit** (Phase 7):

```
/a4-report

基于附件的Excel数据，帮我写一份美团2025年财务复盘报告，
面向管理层，麦肯锡风格，标准版。
```

After generation, Phase 7 automatically:
- Extracts every number from the report
- Cross-checks against your source file
- Flags suspected hallucinations ⚠️ and confirmed errors ❌
- Shows accuracy rate and offers to auto-fix issues

**Sample audit output:**
```
╔══════════════════════════════════════════════════╗
║              🔍  数据审计开始                     ║
╠══════════════════════════════════════════════════╣
║  报告文件: meituan-review-2025.html              ║
║  源数据文件: data.xlsx                           ║
╚══════════════════════════════════════════════════╝

✅ 已验证:    12 项
⚠️ 疑似幻觉:   2 项  (需要人工确认)
❌ 数据错误:   1 项  (需立即修正)

📊 准确率: 80%
```

### Style Selection

Three presets, each capturing a distinct consulting firm aesthetic:

| Style | Look & Feel | Best For |
|-------|------------|----------|
| **McKinsey Blue** | Deep navy + white, serif headlines (Playfair Display) | Executive presentations, formal reports |
| **BCG Silver** | Charcoal + geometric layouts, clean sans-serif (Inter) | Structured analysis, strategy decks |
| **Bain Red** | Bold red accents, impactful numbers (DM Serif Display) | Data-heavy reports, performance reviews |

When you choose "Show me previews," Claude generates three single-page HTML previews side by side so you can compare before committing.

### Trigger Phrases

The skill activates on any of these:

**Chinese:** 写报告 / 生成报告 / 帮我写一份报告 / 麦肯锡风格 / BCG风格 / 贝恩风格 / A4报告 / 分析报告 / 市场分析报告 / 竞品分析报告 / 战略报告

**English:** write a report / consulting report / A4 report / market analysis / competitive intelligence / strategic report / business report

---

## Key Features

### Zero-Dependency Output
Every report is a **single HTML file** with all CSS inline. No npm, no Python, no build step. Works on any machine with a browser.

### Chart Annotation System
Every chart automatically includes:
- **📊 读图指引 (Chart Guide)** — explains axes, colors, and what to look for
- **💡 关键洞察 (Key Insights)** — trend judgment, comparisons, action implications

No more charts that readers stare at without understanding.

### Print-Optimized Layout
- Exact A4 format: 210mm × 297mm
- `@page { size: A4; }` media queries for perfect PDF rendering
- Smart page breaks — no section headers stranded at page bottom
- Background graphics preserved in print mode

### Audience-Aware Content
Choose your audience upfront and the report adapts:
- **C-Suite** → conclusion-first, data-driven, decision-focused
- **Board / Investors** → ROE, cash flow, strategic value
- **Business teams** → operational detail, executable recommendations
- **External clients** → value proposition, partnership highlights

### Consulting-Grade Structure
Every report follows the standard consulting hierarchy:
1. Cover Page
2. Executive Summary (3-5 key findings)
3. Table of Contents
4. Key Findings (title + evidence + implication)
5. Detailed Analysis (charts, frameworks, data)
6. Strategic Recommendations (prioritized, actionable)
7. Appendix (data tables, methodology)

---

## Printing to PDF

1. Open the generated HTML in Chrome or Safari
2. Press `Cmd+P` (Mac) or `Ctrl+P` (Windows)
3. Destination → **Save as PDF**
4. Paper size → **A4**
5. Enable **Background graphics**
6. Save

The report includes a print button (打印 / Save as PDF) for convenience.

---

## File Structure

```
a4-report-main/
├── SKILL.md                  # Core workflow — always loaded
├── STYLE_PRESETS.md          # 3 consulting styles — loaded at Phase 2
├── a4-report-template.md     # A4 HTML architecture — loaded at Phase 3
├── scripts/
│   ├── audit-checklist.md    # Data audit guide — loaded at Phase 7
│   └── export-pdf.sh         # PDF export reference
└── .claude-plugin/
    ├── marketplace.json
    └── plugins/a4-report/
```

The skill uses **progressive disclosure** — only the files needed for the current phase are loaded, keeping context lean and generation fast.

---

## Not This Skill?

| Need | Use Instead |
|------|------------|
| Parse & visualize an earnings report (10-K, 10-Q, 年报) | `analysis-finrpt` |
| Quick slide deck or presentation | `frontend-slides` |

---

## Requirements

- [Claude Code](https://claude.ai/claude-code) CLI
- Modern browser (Chrome / Safari / Firefox) for PDF export

---

## License

MIT — Taste is all you need.
