---
name: a4-report
description: |
  Generate professional A4 paper style consulting reports and analysis documents in McKinsey/BCG/Bain aesthetic. Creates print-optimized HTML reports that look like consulting deliverables.

  **Unique Features:**
  - A4 paper format (210mm × 297mm), print-to-PDF optimized
  - McKinsey/BCG/Bain consulting firm visual styles
  - CSS-based charts without external dependencies
  - Professional report structure: Executive Summary → Findings → Analysis → Recommendations

  **When to use this skill (Triggers):**
  - "写报告" / "生成报告" / "帮我写一份报告"
  - "麦肯锡风格" / "BCG风格" / "贝恩风格" / "咨询风格"
  - "A4报告" / "打印报告" / "PDF报告"
  - "分析报告" / "市场分析报告" / "竞品分析报告" / "战略报告"
  - "consulting report" / "A4 report" / "professional report" / "business report"
  - "帮我写一份...的分析报告" (当需要专业格式的报告时)

  **NOT this skill (use analysis-finrpt instead):**
  - Financial report parsing/visualization (财报解读) → use analysis-finrpt
  - "财报分析" / "10-K" / "10-Q" → use analysis-finrpt

  **Examples:**
  - "帮我写一份中国新能源汽车市场分析报告"
  - "生成一个麦肯锡风格的战略报告"
  - "Create an A4 format consulting report for market entry strategy"
---

# A4 Report

Generate professional A4 paper style consulting reports with McKinsey/BCG/Bain aesthetic.

## Core Principles

1. **A4 Paper Format** — All pages are exactly 210mm × 297mm (or 595pt × 842pt at 72dpi). Print-optimized, clean margins.
2. **Consulting Aesthetics** — Clean typography, data-driven visuals, strategic use of whitespace, no decorative clutter.
3. **Zero Dependencies** — Single HTML files with inline CSS. Print to PDF in browser.
4. **Structured Sections** — Follow consulting report conventions: Executive Summary → Key Findings → Analysis → Recommendations → Appendix.

---

## 核心改进：图表说明规范

**⚠️ 重要：每个图表必须有完整的文字解读**

每张图表（chart）后面，必须紧跟以下两种说明框：

### 1. 读图指引 (Chart Guide)
放在图表下方，用浅蓝色背景框标识，引导读者如何解读图表：
```html
<div class="chart-guide">
    <strong>📊 读图指引：</strong>
    <ul>
        <li>关注X轴与Y轴的对应关系</li>
        <li>注意颜色的含义（通常深色代表当前期，浅色代表对比期）</li>
        <li>寻找数据中的"转折点"或"异常值"</li>
    </ul>
</div>
```

### 2. 关键洞察 (Key Insights)
用深蓝色左边框的框标识，放在读图指引下方，总结图表传递的核心信息：
```html
<div class="key-insights">
    <strong>💡 关键洞察：</strong>
    <ul>
        <li><strong>趋势判断：</strong>数据呈现XX趋势</li>
        <li><strong>对比发现：</strong>XX指标显著高于/低于预期</li>
        <li><strong>行动启示：</strong>建议决策者关注XX问题</li>
    </ul>
</div>
```

### 图表说明样式

```css
.chart-guide {
    background: #ebf8ff;
    border-left: 4px solid #3182ce;
    padding: 8pt 12pt;
    margin: 6pt 0;
    font-size: 8pt;
    page-break-inside: avoid;
}

.key-insights {
    background: #f0f4f8;
    border-left: 4px solid #2c5282;
    padding: 8pt 12pt;
    margin: 6pt 0;
    font-size: 8pt;
    page-break-inside: avoid;
}

.key-insights strong, .chart-guide strong {
    color: #1a365d;
}

.chart-guide ul, .key-insights ul {
    margin: 4pt 0 0 16pt;
    padding: 0;
}

.chart-guide li, .key-insights li {
    margin-bottom: 2pt;
}
```

---

## Report Structure

Every professional consulting report follows this hierarchy:

```
1. Cover Page
   - Report title (bold, clear)
   - Subtitle/client name
   - Date
   - Firm logo placeholder

2. Executive Summary (1 page)
   - Key结论 (3-5 bullet points)
   - Strategic recommendations overview
   - Expected impact

3. Table of Contents
   -自动生成目录

4. Key Findings (2-4 pages)
   - Finding 1: Title + evidence + implication
   - Finding 2: Title + evidence + implication
   - Finding 3: Title + evidence + implication

5. Detailed Analysis (variable)
   - Data visualizations
   - Charts and graphs
   - Framework analyses (2x2 matrices, waterfall charts)

6. Strategic Recommendations (1-2 pages)
   - Specific, actionable recommendations
   - Prioritized by impact/effort

7. Appendix (if needed)
   - Data tables
   - Methodology notes
   - Source references
```

---

## Content Density Guidelines

**⚠️ Fill the page.** Reports that look half-empty waste space. Target **95% screen density** — content should nearly fill the entire A4 page.

### Recommended Content Per Page

| Section Type | Recommended Content |
|-------------|-----------------|
| Executive Summary | 5-6 bullets + 4 KPI cards + 2 highlight boxes |
| Key Findings | 3 finding boxes (side-by-side + 1 below) |
| Analysis | 1 chart + chart-guide + key-insights (stacked vertically) |
| Recommendations | 4-5 recommendation cards |
| Tables | 6-8 rows maximum + 1 summary paragraph |
| SWOT/Grid | 4 quadrants + 2 highlight boxes |

### When to Combine Elements

- **Chart + Guide:** Always stack vertically — chart on top, guide below, insights at bottom
- **Chart + Table:** Use side-by-side only if both are compact; otherwise stack
- **Two finding boxes:** Use `.two-columns` + add a third below
- **Multiple highlight boxes:** Stack 2-3 per page

### Rule of Thumb

> **95% density rule:** Content should fill ~95% of screen space. If there's visible empty space at the bottom of a section, add more content or reduce spacing.

### Common Mistakes

| Mistake | Result | Fix |
|---------|--------|-----|
| Chart without explanation | Reader confused | Add chart-guide + key-insights |
| 85% density | Slightly empty | Add more finding boxes, stack highlight boxes |
| Chart alone on page | Wasted space | Add explanation boxes below |
| Too much spacing | Empty-looking | Reduce margin/padding |

### CSS Classes for Layout

```css
.two-columns { display: grid; grid-template-columns: 1fr 1fr; gap: 12pt; }
.swot-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8pt; }
.metrics-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 12pt; }
```

---

## Phase 1: Content Discovery

**必须先确认以下信息，才能开始生成报告：**

### 首要问题：汇报对象（Audience）

**必须首先询问（header: "汇报对象"）：**

```
这份报告的主要受众是谁？这决定了报告的语言深度、数据详略和建议措辞。

选项：
1. 管理层 / C-Suite（CEO/CFO/COO）
   - 语言专业简洁，结论先行，数字导向
   - 减少基础概念解释，直击决策要点

2. 董事会 / 投资者 / 股东
   - 强调投资回报、风险评估、战略价值
   - 关注ROE、现金流、市值管理等指标

3. 业务负责人 / 中层管理者
   - 需要更多操作层面的分析和可执行建议
   - 可以包含更多背景说明

4. 战略规划部 / 咨询顾问
   - 最详尽的数据和最严谨的框架分析
   - 需要完整的假设和推导过程

5. 客户 / 外部合作方
   - 强调价值主张和合作亮点
   - 减少内部信息的披露

6. 内部团队 / 新人培训
   - 需要更多概念解释和背景铺垫
   - 术语需要标注定义
```

### 标准问题（可以一起问）

**Question 1 — Report Type** (header: "报告类型"):
What kind of report do you need? Options:
- Market Analysis Report / 市场分析报告
- Competitive Intelligence Report / 竞品分析报告
- Strategic Planning Report / 战略规划报告
- Business Review / 业务复盘报告
- Feasibility Study / 可行性研究报告
- Financial Analysis / 财务分析报告
- Custom Topic / 自定义主题

**Question 2 — Purpose** (header: "报告目的"):
What will this report be used for? Options:
- Investment Decision / 投资决策参考
- Board Presentation / 董事会汇报
- Internal Review / 内部复盘会议
- Client Proposal / 客户提案
- Due Diligence / 尽职调查
- Strategic Planning / 战略规划

**Question 3 — Length** (header: "报告篇幅"):
How detailed should this be? Options:
- Brief (5-8 pages) / 简洁版
- Standard (10-15 pages) / 标准版
- Comprehensive (20+ pages) / 详细版

**Question 4 — Style Preference** (header: "风格偏好"):
Which consulting firm's style? Options:
- McKinsey Blue / 麦肯锡蓝 — Deep navy + white, serif headlines
- BCG Silver / BCG银灰 — Charcoal + accent blue, geometric layouts
- Bain Red / 贝恩红 — Dark slate + bold red accents, data-forward
- Custom / 自定义 — Let me specify

---

## Phase 2: Style Selection

### Step 2.1: Style Path

Ask (header: "风格选择"):
How would you like to choose the style?

- "Show me previews" (recommended) — Generate 3 style previews
- "I know what I want" — Select from preset list directly

**If direct selection:** Show preset picker and skip to Phase 3. Available presets are defined in [STYLE_PRESETS.md](STYLE_PRESETS.md).

### Step 2.2: Generate 3 Style Previews

Generate 3 distinct single-page HTML previews showing:
- Cover page aesthetic
- Typography and colors
- Overall consulting feel

| Style              | Recommended For                        |
| ------------------ | -------------------------------------- |
| McKinsey Blue      | Serious, executive, formal            |
| BCG Silver         | Modern, geometric, structured          |
| Bain Red           | Bold, data-driven, impactful           |

Save previews to `.claude-design/report-previews/` (style-a.html, style-b.html, style-c.html).

Open each preview automatically for the user.

### Step 2.3: User Picks

Ask (header: "风格"):
Which style preview do you prefer? Options: Style A / Style B / Style C / Mix elements

If "Mix elements", ask for specifics.

---

## Phase 3: Generate Report

Generate the full report using content from Phase 1 and style from Phase 2.

**Before generating, read these supporting files:**

- [a4-report-template.md](a4-report-template.md) — HTML architecture for A4 print
- [STYLE_PRESETS.md](STYLE_PRESETS.md) — Consulting firm style specifications

**Key requirements:**

- Single self-contained HTML file, all CSS inline
- Use A4 print media queries: `@page { size: A4; margin: 20mm; }`
- Use Google Fonts — professional serif + sans combinations
- Add page breaks: `page-break-before: always`, `page-break-after: avoid`
- Include print button for PDF export
- Add header/footer with page numbers
- All charts should be print-optimized (no interactive elements required)
- **⚠️ Every chart MUST be followed by chart-guide and key-insights boxes**

### Source Data Handling (for later audit)

**如果用户提供 了源数据文件，在生成报告时必须：**

1. **记录数据文件位置** — 保存源数据路径（如 `data/source.xlsx`）
2. **标注数据引用** — 在报告的数据点旁标注来源字段名
3. **保留原始数值** — 记录报告中使用的每一个数值，以便后续审计

这样在Phase 7审计时可以快速定位和验证每个数据点。

---

## Phase 4: Content Enhancement

### Charts & Visualizations

For data-heavy reports, include these consulting-standard visualizations:

| Chart Type          | Use Case                              |
| ------------------- | ------------------------------------- |
| Bar Chart           | Comparative analysis, market share    |
| Line Chart          | Trend analysis, time series           |
| 2x2 Matrix          | Strategic positioning, priority grids |
| Waterfall Chart     | Variance analysis, build-ups         |
| Sankey Diagram      | Flow analysis, process mapping       |
| Donut Chart         | Composition analysis, segmentation    |
| Heat Map            | Performance comparison, risk assessment|

Use CSS-based charts (no external libraries) for zero-dependency output.

### Required Chart Structure

Every chart section MUST follow this structure:

```html
<!-- 1. Chart Container -->
<div class="chart-container">
    <div class="chart-title">图表标题（清晰描述数据内容）</div>
    <svg class="chart-svg">...SVG code...</svg>
</div>

<!-- 2. Chart Guide (读图指引) -->
<div class="chart-guide">
    <strong>📊 读图指引：</strong>
    <ul>
        <li>说明图表的基本读法（如：颜色含义、坐标轴含义）</li>
        <li>指出需要特别关注的数据点</li>
        <li>解释数据的来源和口径</li>
    </ul>
</div>

<!-- 3. Key Insights (关键洞察) -->
<div class="key-insights">
    <strong>💡 关键洞察：</strong>
    <ul>
        <li><strong>趋势判断：</strong>数据呈现什么趋势</li>
        <li><strong>对比发现：</strong>与预期或对比基准的差异</li>
        <li><strong>行动启示：</strong>对决策者的启示</li>
    </ul>
</div>
```

### Example: Revenue Trend Chart

```html
<!-- Chart -->
<div class="chart-container">
    <div class="chart-title">图1：美团收入增长趋势（2023-2025）</div>
    <svg class="chart-svg" viewBox="0 0 400 150">
        <!-- SVG bar chart code -->
    </svg>
</div>

<!-- Chart Guide -->
<div class="chart-guide">
    <strong>📊 读图指引：</strong>
    <ul>
        <li>深蓝色柱状图为当年收入，浅蓝色为同比增长</li>
        <li>Y轴左轴为收入金额（亿元），右轴为同比增速（%）</li>
        <li>关注2024-2025年增速的明显放缓趋势</li>
    </ul>
</div>

<!-- Key Insights -->
<div class="key-insights">
    <strong>💡 关键洞察：</strong>
    <ul>
        <li><strong>趋势判断：</strong>收入增速从2024年的18.6%骤降至2025年的8.1%，回落10.5个百分点</li>
        <li><strong>对比发现：</strong>8.1%的增速低于市场一致预期的10%，显示核心业务增长乏力</li>
        <li><strong>行动启示：</strong>管理层需重新评估2026年增长目标，并加大新业务突破力度</li>
    </ul>
</div>
```

### Frameworks

Include consulting-standard frameworks when relevant:
- SWOT Analysis
- Porter's Five Forces
- BCG Growth-Share Matrix
- McKinsey 7S Framework
- PESTEL Analysis

---

## Phase 5: Delivery

1. **Open** — Use `open [filename].html` to launch in browser
2. **Print to PDF** — Guide user to print (Cmd/Ctrl+P) and select "Save as PDF"
3. **Summarize** — Tell the user:
   - File location, style name, page count
   - Report audience (based on their selection)
   - How to print: File → Print → Save as PDF
   - How to customize: CSS variables in `:root` for colors, font links for typography
   - Recommended print settings: A4 paper, no margins scaling, background graphics ON

### Auto-Proceed to Phase 7

**⚠️ 重要：完成交付后，必须检查是否需要自动进入Phase 7数据审计**

在完成Phase 5交付时，**必须判断是否应该自动进入数据审计**：

| 条件 | 动作 |
|-----|------|
| 用户提供了源数据文件 | **立即自动进入Phase 7**，先完成数据审计再交付 |
| 用户未提供源数据 | 跳过Phase 7，直接完成交付 |

**判断逻辑示例：**
```
如果用户说 "基于xxx数据写报告" 或 上传了CSV/Excel/PDF文件
→ 报告生成后自动进入Phase 7数据审计
→ 完成审计后再进行Phase 5交付

如果用户只是说 "写一份关于xxx的报告"（无数据源）
→ 直接进行Phase 5交付
→ Phase 7仅在用户主动要求时执行
```

**自动审计流程：**
```
报告生成完成
    ↓
检测到源数据文件
    ↓
自动进入Phase 7数据审计
    ↓
审计完成并修复问题后
    ↓
再进行Phase 5正式交付
```

---

## Phase 6: PDF Export (Optional)

After delivery, **ask the user:** _"Would you like me to export this report as a PDF file?"_

If yes, guide them through browser print:
1. Open the HTML in browser
2. File → Print (or Cmd/Ctrl+P)
3. Destination → Save as PDF
4. More settings → Paper Size: A4
5. Options → Check "Background graphics"

---

## Phase 7: Data Audit (Automatic) ⭐

**⚠️ 重要变更：数据审计现已自动执行，不再等待用户询问！**

报告生成完成后，如果用户提供过原始数据文件，系统将**自动**启动数据审计流程，对报告中的数据进行校验。

### Auto-Trigger Conditions

**以下情况将自动触发Phase 7数据审计：**

| 触发条件 | 说明 |
|---------|------|
| 用户提供了源数据文件 | CSV、Excel、PDF、TXT等格式的数据文件 |
| 用户指定了数据来源 | 如"基于xxx数据"、"从附件获取" |
| 报告包含具体数字 | 金额、百分比、增长率等可量化指标 |

### Audit Modes

| 模式 | 触发条件 | 说明 |
|-----|---------|------|
| **自动模式 (Auto)** | 用户提供源数据 | 生成报告后自动运行完整审计 |
| **手动模式 (Manual)** | 用户未提供源数据 | 仅当用户主动询问时执行 |

**如果用户提供了源数据 → 报告生成后自动进入Phase 7审计**
**如果用户未提供源数据 → Phase 7仅作为可选功能保留**

---

### Step 7.1: Print Audit Header

Output directly to terminal:

```
╔══════════════════════════════════════════════════════════════════════════════╗
║                              🔍  数据审计开始                                ║
╠══════════════════════════════════════════════════════════════════════════════╣
║  报告文件: [report.html]                                                     ║
║  源数据文件: [source.xlsx]                                                   ║
║  审计时间: 2026-04-12 14:30                                                  ║
╚══════════════════════════════════════════════════════════════════════════════╝
```

---

### Step 7.2: Extract & List Audit Items

Parse the report and list all data points to verify. Print each item with its status:

```
📊 正在提取数据点...

[待验证]  1. 执行摘要 > 全年收入: 3,649亿元
[待验证]  2. 执行摘要 > YoY增长: +8.1%
[待验证]  3. 关键发现1 > 市场规模: 4,200亿元
[待验证]  4. 关键发现1 > 增长率: 12%
[待验证]  5. 表格 > Q4收入: 892亿元
...
```

---

### Step 7.3: Validate & Mark Progress (with strikethrough)

For each validation, print the result directly. Completed items get strikethrough:

```
🔍 正在逐项验证...

[验证中]  1. 执行摘要 > 全年收入: 3,649亿元
          └─ 查找源数据: 364,854,746千元...找到 ✓
[完成~~]  2. 执行摘要 > YoY增长: +8.1%
          └─ 计算验证: (3649-3376)/3376=8.08% ✓

[验证中]  3. 关键发现1 > 市场规模: 4,200亿元
          └─ 查找源数据: 未找到直接字段，估算值？ ⚠️

[完成~~]  4. 关键发现1 > 增长率: 12%
          └─ 计算验证: (4200-3750)/3750=12% ✓

[错误✗]   5. 表格 > 市场份额: 68%
          └─ 查找源数据: 源文件无此字段 ❌ 疑似幻觉
```

---

### Step 7.4: Final Summary

After all validations, print summary table:

```
════════════════════════════════════════════════════════════════════════════════
                                   📋 审计结果汇总
════════════════════════════════════════════════════════════════════════════════

  ✅ 已验证:     12 项
  ⚠️ 疑似幻觉:    2 项  (需要人工确认)
  ❌ 数据错误:    1 项  (需立即修正)
  🔍 无法验证:    3 项  (源数据中未找到)

────────────────────────────────────────────────────────────────────────────────
                                   📊 准确率: 75%
════════════════════════════════════════════════════════════════════════════════
```

---

### Step 7.5: Detailed Findings

Print detailed list of issues:

```
════════════════════════════════════════════════════════════════════════════════
                                   ⚠️ 需要关注的问题
════════════════════════════════════════════════════════════════════════════════

【疑似幻觉 - 需人工确认】
  1. 第5页-发现2 > Q4单季亏损161亿元
     └─ 源数据未提供Q4分部损益，建议核实数据来源

  2. 第6页 > 新业务亏损扩大79%
     └─ 计算基数183亿待确认，请核实2024年新业务亏损数据

【数据错误 - 需修正】
  3. 第X页-表格 > 市场份额68%
     └─ 源数据中无此字段，纯属虚构，建议删除或修正为61%

【无法验证 - 建议添加来源注释】
  4. 第4页 > 行业排名TOP3
     └─ 源数据无此字段，建议标注数据来源

════════════════════════════════════════════════════════════════════════════════
```

---

### Step 7.6: Ask for Fix

```
┌─────────────────────────────────────────────────────────────────────────────┐
│  审计完成！是否需要修复这些问题？                                            │
│                                                                             │
│  1. [自动修复]  自动修正所有可计算的错误                                     │
│  2. [选择性修复] 逐项选择要修复的内容                                        │
│  3. [生成报告]  在报告中高亮标记问题项（PDF保持原样）                        │
│  4. [跳过]     保持原样，不做修改                                           │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

### Terminal Output Format Reference

Use this format for audit output:

```bash
# Header box
echo "╔════════════════════════════════════════════════════════════════╗"
echo "║  🔍 数据审计开始                                                ║"
echo "╚════════════════════════════════════════════════════════════════╝"

# Pending item
echo "[待验证]  1. 执行摘要 > 全年收入: 3,649亿元"

# In progress (with spinner animation)
echo -n "[验证中]  2. 执行摘要 > YoY增长: +8.1%  "
echo "└─ 查找源数据..."

# Completed with strikethrough
echo "[完成~~]  2. 执行摘要 > YoY增长: +8.1%"
echo "          └─ 计算验证: 8.08% ✓"

# Warning
echo "[⚠️ 疑似]  3. 第5页 > Q4亏损161亿元"
echo "          └─ 源数据未提供Q4分部数据"

# Error
echo "[❌ 错误]  4. 第X页 > 市场份额68%"
echo "          └─ 源数据无此字段，疑似虚构"
```

### ANSI Colors for Terminal (Optional)

```bash
# Colors
GREEN='\033[0;32m'    # Verified
YELLOW='\033[1;33m'   # Warning
RED='\033[0;31m'      # Error
BLUE='\033[0;34m'     # In progress
NC='\033[0m'          # No Color

# Strikethrough (using Unicode)
echo -e "${GREEN}[完成~~] 数据项 ${NC}"

# Example with color
echo -e "${GREEN}✓ 已验证${NC}: 全年收入 3,649亿元"
echo -e "${YELLOW}⚠️ 疑似${NC}: Q4亏损161亿元 (需确认)"
echo -e "${RED}✗ 错误${NC}: 市场份额68% (源数据无此字段)"
```

---

### Quick Audit Flow (Summary)

```
1. 打印审计头部信息
2. 列出所有待验证数据点
3. 逐项验证，每项打印：
   - 验证中状态
   - 验证结果 (✓/⚠️/✗)
   - 发现详情
4. 完成后打印汇总统计
5. 列出问题清单
6. 询问用户修复方式
```

---

## Supporting Files

| File                        | Purpose                                      | When to Read          |
| --------------------------- | -------------------------------------------- | --------------------- |
| [a4-report-template.md](a4-report-template.md) | A4 HTML structure and print CSS     | Phase 3 (generation)  |
| [STYLE_PRESETS.md](STYLE_PRESETS.md)       | 3 consulting firm style presets      | Phase 2 (style selection) |
| [scripts/export-pdf.sh](scripts/export-pdf.sh) | Browser-based PDF export guidance   | Phase 6 (export)      |
| [scripts/audit-checklist.md](scripts/audit-checklist.md) | Data audit checklist & guide | Phase 7 (audit) |

---

## Design Guidelines

### Typography

| Element          | Font                          | Size      | Weight |
| ---------------- | ----------------------------- | --------- | ------ |
| Report Title     | Playfair Display / Noto Serif | 32-36pt   | 700    |
| Section Header   | Noto Sans / Source Sans      | 18-20pt   | 600    |
| Subsection       | Noto Sans / Source Sans       | 14-16pt   | 600    |
| Body Text        | Noto Sans / Source Sans      | 10-11pt   | 400    |
| Caption/Source   | Noto Sans / Source Sans      | 8-9pt     | 400    |
| Table Header     | Noto Sans / Source Sans      | 9-10pt    | 600    |
| Table Body       | Noto Sans / Source Sans      | 9-10pt    | 400    |

### Colors (McKinsey-Style Palette)

```css
:root {
    /* Primary */
    --primary-navy: #1a365d;
    --primary-dark: #0f2444;
    --primary-light: #2c5282;

    /* Accent */
    --accent-blue: #3182ce;
    --accent-silver: #718096;

    /* Neutrals */
    --text-primary: #1a202c;
    --text-secondary: #4a5568;
    --text-muted: #a0aec0;

    /* Backgrounds */
    --bg-white: #ffffff;
    --bg-light: #f7fafc;
    --bg-chart: #edf2f7;

    /* Charts */
    --chart-1: #2c5282;
    --chart-2: #3182ce;
    --chart-3: #63b3ed;
    --chart-4: #90cdf4;
}
```

### Print Optimization

```css
/* A4 Page Setup */
@page {
    size: A4;
    margin: 20mm 15mm;
}

/* Avoid page breaks inside these */
.no-break {
    page-break-inside: avoid;
}

/* Force page breaks before these */
.break-before {
    page-break-before: always;
}
```

---

## Content Quality Standards

**Write like a top-tier consultant:**

1. **结论先行** — Lead with the key finding/recommendation
2. **数据支撑** — Every claim backed by evidence
3. **逻辑清晰** — MECE structure (Mutually Exclusive, Collectively Exhaustive)
4. **Actionable** — Specific, not vague recommendations
5. **简洁有力** — No jargon, no fluff

**Headline Formula:**
> [Key Finding/Recommendation] + [Evidence/Context] + [Implication/Stakes]

Example:
> "中国高端消费品市场预计年增12%，头部品牌应加速布局下沉渠道以捕获新增消费人群。"

---

## Anti-Patterns (Avoid These)

- ❌ Generic "In today's rapidly changing world..." opener
- ❌ More than 6 bullet points per section
- ❌ Decorative elements that add no information
- ❌ Colorful charts without clear takeaway
- ❌ Vague recommendations ("should consider improving...")
- ❌ Mixing hierarchical levels in lists
- ❌ Chart without explanation — readers won't understand the significance
- ❌ Report without knowing the audience — language/depth may be wrong
