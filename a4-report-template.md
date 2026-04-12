# A4 Report HTML Template

Reference architecture for generating professional A4 print-ready consulting reports.

## Base HTML Structure

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Report Title</title>

    <!-- Google Fonts: Professional Serif + Sans -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Source+Sans+Pro:wght@400;600;700&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">

    <style>
        /* ===========================================
           CSS CUSTOM PROPERTIES (THEME)
           =========================================== */
        :root {
            /* Primary Colors — McKinsey Blue as default */
            --primary: #1a365d;
            --primary-dark: #0f2444;
            --primary-light: #2c5282;
            --accent: #3182ce;
            --accent-light: #63b3ed;

            /* Text */
            --text-primary: #1a202c;
            --text-secondary: #4a5568;
            --text-muted: #718096;

            /* Backgrounds */
            --bg-white: #ffffff;
            --bg-light: #f7fafc;
            --bg-accent: #ebf4ff;

            /* Charts */
            --chart-1: #1a365d;
            --chart-2: #2c5282;
            --chart-3: #3182ce;
            --chart-4: #63b3ed;
            --chart-5: #90cdf4;

            /* Typography Scale */
            --font-serif: 'Playfair Display', 'Noto Serif SC', serif;
            --font-sans: 'Source Sans Pro', 'Noto Sans SC', sans-serif;
            --font-mono: 'IBM Plex Mono', 'JetBrains Mono', monospace;

            /* Spacing */
            --page-margin: 20mm;
            --section-gap: 24pt;
        }

        /* ===========================================
           A4 PAGE SETUP (PRINT)
           =========================================== */
        @page {
            size: A4;
            margin: var(--page-margin);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        /* ⚠️ CRITICAL: Enable background colors in PDF print */
        * {
            print-color-adjust: exact !important;
            -webkit-print-color-adjust: exact !important;
        }

        body {
            font-family: var(--font-sans);
            font-size: 11pt;
            line-height: 1.6;
            color: var(--text-primary);
            background: var(--bg-white);
        }

        /* ===========================================
           PAGE CONTAINER
           =========================================== */
        .page {
            width: 210mm;
            min-height: 297mm;
            padding: var(--page-margin);
            margin: 0 auto;
            background: var(--bg-white);
            position: relative;
        }

        /* ===========================================
           TYPOGRAPHY
           =========================================== */
        h1 {
            font-family: var(--font-serif);
            font-size: 28pt;
            font-weight: 700;
            line-height: 1.2;
            color: var(--primary);
            margin-bottom: 12pt;
        }

        h2 {
            font-family: var(--font-sans);
            font-size: 15pt;
            font-weight: 600;
            color: var(--primary);
            margin-top: 16pt;
            margin-bottom: 8pt;
            padding-bottom: 5pt;
            border-bottom: 2px solid var(--primary);
        }

        h3 {
            font-family: var(--font-sans);
            font-size: 12pt;
            font-weight: 600;
            color: var(--text-primary);
            margin-top: 12pt;
            margin-bottom: 6pt;
        }

        h4 {
            font-family: var(--font-sans);
            font-size: 10pt;
            font-weight: 600;
            color: var(--text-secondary);
            margin-top: 8pt;
            margin-bottom: 4pt;
        }

        p {
            margin-bottom: 8pt;
            text-align: justify;
        }

        /* ===========================================
           EXECUTIVE SUMMARY BOX
           =========================================== */
        .executive-summary {
            background: var(--bg-accent);
            border-left: 4px solid var(--primary);
            padding: 12pt 16pt;
            margin: 10pt 0;
            page-break-inside: avoid;
        }

        .executive-summary h2 {
            margin-top: 0;
            border-bottom: none;
            font-size: 13pt;
        }

        .executive-summary ul {
            margin: 8pt 0;
            padding-left: 16pt;
        }

        .executive-summary li {
            margin-bottom: 5pt;
            font-size: 10pt;
        }

        /* ===========================================
           HIGHLIGHT BOXES
           =========================================== */
        .highlight-negative {
            background: #fed7d7;
            border-left: 4px solid #c53030;
            padding: 10pt 14pt;
            margin: 10pt 0;
            page-break-inside: avoid;
        }

        .highlight-positive {
            background: #c6f6d5;
            border-left: 4px solid #38a169;
            padding: 10pt 14pt;
            margin: 10pt 0;
            page-break-inside: avoid;
        }

        /* ===========================================
           KEY METRICS (Big Number Style)
           =========================================== */
        .metrics-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10pt;
            margin: 10pt 0;
        }

        .metric-card {
            text-align: center;
            padding: 10pt 8pt;
            border: 1px solid #e2e8f0;
            page-break-inside: avoid;
        }

        .metric-card.negative { border-color: #c53030; }
        .metric-card.positive { border-color: #38a169; }

        .metric-value {
            font-family: var(--font-mono);
            font-size: 20pt;
            font-weight: 700;
            color: var(--primary);
        }

        .metric-value.negative { color: #c53030; }
        .metric-value.positive { color: #38a169; }

        .metric-label {
            font-size: 9pt;
            color: var(--text-secondary);
            margin-top: 3pt;
        }

        .metric-change {
            font-family: var(--font-mono);
            font-size: 9pt;
            margin-top: 3pt;
        }

        .metric-change.down { color: #c53030; }
        .metric-change.up { color: #38a169; }

        /* ===========================================
           CHARTS (SVG-Based — REQUIRED FOR PRINT)
           =========================================== */
        .chart-container {
            margin: 10pt 0;
            padding: 12pt;
            border: 1px solid #e2e8f0;
        }

        .chart-title {
            font-size: 10pt;
            font-weight: 600;
            color: var(--text-primary);
            margin-bottom: 8pt;
        }

        /* SVG Charts — REQUIRED for print compatibility */
        .chart-svg {
            width: 100%;
            height: auto;
            print-color-adjust: exact;
            -webkit-print-color-adjust: exact;
        }

        /* Legacy: Remove .bar-chart and related - using SVG now */
        .bar-chart { display: none; }
        .bar-item { display: none; }
        .bar { display: none; }
        .bar-label { display: none; }
        .bar-value { display: none; }

        /* ===========================================
           CHART GUIDE (读图指引) & KEY INSIGHTS (关键洞察)
           =========================================== */
        .chart-guide {
            background: #ebf8ff;
            border-left: 4px solid #3182ce;
            padding: 8pt 12pt;
            margin: 6pt 0;
            font-size: 8pt;
            page-break-inside: avoid;
        }

        .chart-guide strong {
            color: #1a365d;
        }

        .chart-guide ul {
            margin: 4pt 0 0 16pt;
            padding: 0;
        }

        .chart-guide li {
            margin-bottom: 2pt;
        }

        .key-insights {
            background: #f0f4f8;
            border-left: 4px solid #2c5282;
            padding: 8pt 12pt;
            margin: 6pt 0;
            font-size: 8pt;
            page-break-inside: avoid;
        }

        .key-insights strong {
            color: #1a365d;
        }

        .key-insights ul {
            margin: 4pt 0 0 16pt;
            padding: 0;
        }

        .key-insights li {
            margin-bottom: 2pt;
        }

        /* ===========================================
           2x2 MATRIX
           =========================================== */
        .matrix-2x2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            grid-template-rows: 1fr 1fr;
            gap: 2px;
            width: 100%;
            max-width: 400pt;
            height: 300pt;
            margin: 20pt auto;
            border: 2px solid var(--primary);
        }

        .matrix-cell {
            padding: 16pt;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
        }

        .matrix-cell:nth-child(1) { background: #c6f6d5; }
        .matrix-cell:nth-child(2) { background: #fefcbf; }
        .matrix-cell:nth-child(3) { background: #fed7d7; }
        .matrix-cell:nth-child(4) { background: #bee3f8; }

        .matrix-label {
            font-size: 9pt;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5pt;
        }

        /* ===========================================
           TABLES
           =========================================== */
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 10pt 0;
            font-size: 9pt;
            page-break-inside: avoid;
        }

        th {
            background: var(--primary);
            color: white;
            font-weight: 600;
            text-align: left;
            padding: 6pt 8pt;
            print-color-adjust: exact;
            -webkit-print-color-adjust: exact;
        }

        td {
            padding: 5pt 8pt;
            border-bottom: 1px solid #e2e8f0;
        }

        tr {
            page-break-inside: avoid;
        }

        tr:nth-child(even) {
            background: var(--bg-light);
        }

        tr.negative { background: #fed7d7; }
        tr.positive { background: #c6f6d5; }

        /* ===========================================
           PAGE BREAKS
           =========================================== */
        .page-break {
            page-break-before: always;
        }

        .no-break {
            page-break-inside: avoid;
        }

        /* ===========================================
           HEADER & FOOTER (for printing)
           =========================================== */
        .page-header {
            position: fixed;
            top: 10mm;
            left: 20mm;
            right: 20mm;
            font-size: 8pt;
            color: var(--text-muted);
            display: flex;
            justify-content: space-between;
            border-bottom: 0.5px solid #e2e8f0;
            padding-bottom: 6pt;
        }

        .page-footer {
            position: fixed;
            bottom: 10mm;
            left: 20mm;
            right: 20mm;
            font-size: 8pt;
            color: var(--text-muted);
            display: flex;
            justify-content: space-between;
            border-top: 0.5px solid #e2e8f0;
            padding-top: 6pt;
        }

        @media print {
            .page-header,
            .page-footer {
                display: flex;
            }
        }

        @media screen {
            .page-header,
            .page-footer {
                display: none;
            }
        }

        /* ===========================================
           COVER PAGE
           =========================================== */
        .cover-page {
            height: 260mm;
            display: flex;
            flex-direction: column;
            justify-content: center;
            padding: 40mm;
        }

        .cover-title {
            font-family: var(--font-serif);
            font-size: 36pt;
            font-weight: 700;
            color: var(--primary);
            line-height: 1.2;
            margin-bottom: 16pt;
        }

        .cover-subtitle {
            font-size: 16pt;
            color: var(--text-secondary);
            margin-bottom: 40pt;
        }

        .cover-meta {
            font-size: 11pt;
            color: var(--text-muted);
        }

        .cover-meta p {
            margin-bottom: 6pt;
        }

        /* ===========================================
           SECTION DIVIDER
           =========================================== */
        .section-number {
            font-family: var(--font-mono);
            font-size: 48pt;
            font-weight: 700;
            color: var(--primary);
            opacity: 0.15;
            position: absolute;
            top: 20mm;
            right: 20mm;
        }

        /* ===========================================
           LAYOUT: TWO COLUMNS
           =========================================== */
        .two-columns {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12pt;
            margin: 10pt 0;
        }

        /* ===========================================
           LAYOUT: SWOT GRID
           =========================================== */
        .swot-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 8pt;
            margin: 10pt 0;
        }

        .swot-box {
            padding: 8pt;
            border: 1px solid #e2e8f0;
            page-break-inside: avoid;
        }

        .swot-box.strengths { border-left: 4px solid #38a169; }
        .swot-box.weaknesses { border-left: 4px solid #c53030; }
        .swot-box.opportunities { border-left: 4px solid #3182ce; }
        .swot-box.threats { border-left: 4px solid #d69e2e; }

        .swot-title {
            font-size: 9pt;
            font-weight: 700;
            margin-bottom: 6pt;
        }

        .swot-box.strengths .swot-title { color: #38a169; }
        .swot-box.weaknesses .swot-title { color: #c53030; }
        .swot-box.opportunities .swot-title { color: #3182ce; }
        .swot-box.threats .swot-title { color: #d69e2e; }

        .swot-list {
            font-size: 8pt;
            padding-left: 14pt;
            margin: 0;
        }

        .swot-list li { margin-bottom: 3pt; }

        /* ===========================================
           FINDING BOX
           =========================================== */
        .finding-box {
            background: var(--bg-white);
            border: 1px solid #e2e8f0;
            border-left: 4px solid var(--accent);
            padding: 10pt 14pt;
            margin: 8pt 0;
            page-break-inside: avoid;
        }

        .finding-title {
            font-size: 10pt;
            font-weight: 700;
            color: var(--primary);
            margin-bottom: 4pt;
        }

        .finding-evidence {
            font-size: 9pt;
            color: var(--text-secondary);
            margin-bottom: 4pt;
        }

        .finding-implication {
            font-size: 9pt;
            font-weight: 600;
            color: var(--text-primary);
            font-style: italic;
        }

        /* ===========================================
           RECOMMENDATION CARD
           =========================================== */
        .recommendation {
            display: flex;
            gap: 10pt;
            margin: 8pt 0;
            padding: 10pt;
            background: var(--bg-light);
            border-radius: 3px;
            page-break-inside: avoid;
        }

        .recommendation-priority {
            font-family: var(--font-mono);
            font-size: 18pt;
            font-weight: 700;
            color: var(--accent);
            min-width: 36pt;
        }

        .recommendation-content h4 {
            margin-top: 0;
            font-size: 10pt;
            margin-bottom: 3pt;
        }

        .recommendation-content p {
            margin-bottom: 0;
            font-size: 9pt;
        }

        /* ===========================================
           PRINT BUTTON
           =========================================== */
        .print-button {
            position: fixed;
            top: 20px;
            right: 20px;
            background: var(--primary);
            color: white;
            border: none;
            padding: 12pt 24pt;
            font-size: 12pt;
            font-weight: 600;
            cursor: pointer;
            border-radius: 4px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.2);
            z-index: 1000;
        }

        .print-button:hover {
            background: var(--primary-light);
        }

        @media print {
            .print-button {
                display: none;
            }
        }

        /* ===========================================
           SOURCE/CAPTION
           =========================================== */
        .source {
            font-size: 8pt;
            color: var(--text-muted);
            margin-top: 8pt;
            font-style: italic;
        }

        .caption {
            font-size: 9pt;
            color: var(--text-secondary);
            text-align: center;
            margin-top: 8pt;
        }
    </style>
</head>
<body>
    <!-- Print Button -->
    <button class="print-button" onclick="window.print()">
        打印 / Save as PDF
    </button>

    <!-- Page 1: Cover -->
    <div class="page cover-page">
        <h1 class="cover-title">报告标题</h1>
        <p class="cover-subtitle">副标题 / 客户名称</p>
        <div class="cover-meta">
            <p>2026年4月</p>
            <p>机密文件 | Confidential</p>
        </div>
    </div>

    <!-- Page 2: Executive Summary -->
    <div class="page">
        <div class="page-header">
            <span>报告标题</span>
            <span>机密</span>
        </div>

        <h1 style="font-size: 20pt; margin-top: 0;">执行摘要</h1>

        <div class="executive-summary">
            <h2>核心发现</h2>
            <ul>
                <li><strong>发现1:</strong> 具体数据支撑的结论...</li>
                <li><strong>发现2:</strong> 具体数据支撑的结论...</li>
                <li><strong>发现3:</strong> 具体数据支撑的结论...</li>
            </ul>
        </div>

        <div class="page-footer">
            <span>© 2026</span>
            <span>第 <span class="page-num">2</span> 页</span>
        </div>
    </div>

    <!-- Page 3: Table of Contents -->
    <div class="page page-break">
        <div class="page-header">
            <span>报告标题</span>
            <span>机密</span>
        </div>

        <h1 style="font-size: 20pt; margin-top: 0;">目录</h1>

        <div style="display: flex; justify-content: space-between; margin-top: 20pt;">
            <div>
                <p style="margin-bottom: 8pt;"><strong>1. 执行摘要</strong></p>
                <p style="margin-bottom: 8pt;">2. 关键发现</p>
                <p style="margin-left: 20pt; margin-bottom: 6pt;">2.1 发现一</p>
                <p style="margin-left: 20pt; margin-bottom: 6pt;">2.2 发现二</p>
                <p style="margin-left: 20pt; margin-bottom: 8pt;">2.3 发现三</p>
                <p style="margin-bottom: 8pt;"><strong>3. 详细分析</strong></p>
                <p style="margin-bottom: 8pt;"><strong>4. 战略建议</strong></p>
            </div>
            <div style="text-align: right;">
                <p style="margin-bottom: 8pt;">1</p>
                <p style="margin-bottom: 8pt;">2</p>
                <p style="margin-bottom: 6pt;">3</p>
                <p style="margin-bottom: 6pt;">3</p>
                <p style="margin-bottom: 8pt;">4</p>
                <p style="margin-bottom: 8pt;">5</p>
                <p style="margin-bottom: 8pt;">7</p>
            </div>
        </div>

        <div class="page-footer">
            <span>© 2026</span>
            <span>第 <span class="page-num">3</span> 页</span>
        </div>
    </div>

    <!-- Page 4: Key Findings -->
    <div class="page page-break">
        <div class="page-header">
            <span>报告标题</span>
            <span>机密</span>
        </div>

        <h2>关键发现</h2>
        <div class="section-number">01</div>

        <div class="finding-box">
            <div class="finding-title">发现一：市场持续增长但竞争加剧</div>
            <div class="finding-evidence">
                2025年中国高端消费品市场规模达4,200亿元，年增长率12%。然而，头部品牌市场份额从68%下降至61%，新进入者正在蚕食传统巨头领地。
            </div>
            <div class="finding-implication">
                启示：品牌需加速差异化战略，避免陷入价格竞争泥潭。
            </div>
        </div>

        <div class="finding-box">
            <div class="finding-title">发现二：下沉市场成为新增长引擎</div>
            <div class="finding-evidence">
                三四线城市高端消费增速达18%，显著高于一二线城市的8%。下沉市场消费者对品质和品牌的认知度显著提升。
            </div>
            <div class="finding-implication">
                启示：应重新评估渠道策略，加大下沉市场投入。
            </div>
        </div>

        <div class="finding-box">
            <div class="finding-title">发现三：数字化渠道重塑购买路径</div>
            <div class="finding-evidence">
                线上渠道占比已达45%，其中直播电商增长240%。消费者决策路径从传统的"搜索-比较-购买"转变为"种草-体验-拔草"。
            </div>
            <div class="finding-implication">
                启示：营销预算应向数字化倾斜，构建内容营销能力。
            </div>
        </div>

        <div class="page-footer">
            <span>© 2026</span>
            <span>第 <span class="page-num">4</span> 页</span>
        </div>
    </div>

    <!-- Page 5: Charts (SVG-based for print compatibility) -->
    <div class="page page-break">
        <div class="page-header">
            <span>报告标题</span>
            <span>机密</span>
        </div>

        <h2>市场分析</h2>
        <div class="section-number">02</div>

        <!-- SVG Bar Chart: Market Size 2020-2025 -->
        <div class="chart-container">
            <div class="chart-title">图1：高端消费品市场规模（2020-2025）</div>
            <svg class="chart-svg" viewBox="0 0 500 200" xmlns="http://www.w3.org/2000/svg">
                <!-- Y-axis -->
                <line x1="40" y1="20" x2="40" y2="150" stroke="#e2e8f0" stroke-width="1"/>
                <!-- X-axis -->
                <line x1="40" y1="150" x2="480" y2="150" stroke="#e2e8f0" stroke-width="1"/>

                <!-- Y-axis labels -->
                <text x="35" y="25" font-family="IBM Plex Mono, monospace" font-size="8" fill="#718096" text-anchor="end">5,000</text>
                <text x="35" y="55" font-family="IBM Plex Mono, monospace" font-size="8" fill="#718096" text-anchor="end">4,000</text>
                <text x="35" y="85" font-family="IBM Plex Mono, monospace" font-size="8" fill="#718096" text-anchor="end">3,000</text>
                <text x="35" y="115" font-family="IBM Plex Mono, monospace" font-size="8" fill="#718096" text-anchor="end">2,000</text>
                <text x="35" y="145" font-family="IBM Plex Mono, monospace" font-size="8" fill="#718096" text-anchor="end">0</text>

                <!-- Grid lines -->
                <line x1="40" y1="55" x2="480" y2="55" stroke="#e2e8f0" stroke-width="0.5" stroke-dasharray="2,2"/>
                <line x1="40" y1="85" x2="480" y2="85" stroke="#e2e8f0" stroke-width="0.5" stroke-dasharray="2,2"/>
                <line x1="40" y1="115" x2="480" y2="115" stroke="#e2e8f0" stroke-width="0.5" stroke-dasharray="2,2"/>

                <!-- Bars -->
                <rect x="60" y="94" width="50" height="56" fill="#1a365d"/>
                <text x="85" y="88" font-family="IBM Plex Mono, monospace" font-size="9" fill="#1a365d" text-anchor="middle" font-weight="600">2,800</text>
                <text x="85" y="165" font-family="Source Sans Pro, sans-serif" font-size="9" fill="#4a5568" text-anchor="middle">2020</text>

                <rect x="130" y="78" width="50" height="72" fill="#2c5282"/>
                <text x="155" y="72" font-family="IBM Plex Mono, monospace" font-size="9" fill="#2c5282" text-anchor="middle" font-weight="600">3,200</text>
                <text x="155" y="165" font-family="Source Sans Pro, sans-serif" font-size="9" fill="#4a5568" text-anchor="middle">2021</text>

                <rect x="200" y="68" width="50" height="82" fill="#3182ce"/>
                <text x="225" y="62" font-family="IBM Plex Mono, monospace" font-size="9" fill="#3182ce" text-anchor="middle" font-weight="600">3,500</text>
                <text x="225" y="165" font-family="Source Sans Pro, sans-serif" font-size="9" fill="#4a5568" text-anchor="middle">2022</text>

                <rect x="270" y="63" width="50" height="87" fill="#63b3ed"/>
                <text x="295" y="57" font-family="IBM Plex Mono, monospace" font-size="9" fill="#63b3ed" text-anchor="middle" font-weight="600">3,700</text>
                <text x="295" y="165" font-family="Source Sans Pro, sans-serif" font-size="9" fill="#4a5568" text-anchor="middle">2023</text>

                <rect x="340" y="58" width="50" height="92" fill="#90cdf4"/>
                <text x="365" y="52" font-family="IBM Plex Mono, monospace" font-size="9" fill="#90cdf4" text-anchor="middle" font-weight="600">3,900</text>
                <text x="365" y="165" font-family="Source Sans Pro, sans-serif" font-size="9" fill="#4a5568" text-anchor="middle">2024</text>

                <rect x="410" y="48" width="50" height="102" fill="#1a365d"/>
                <text x="435" y="42" font-family="IBM Plex Mono, monospace" font-size="9" fill="#1a365d" text-anchor="middle" font-weight="600">4,200</text>
                <text x="435" y="165" font-family="Source Sans Pro, sans-serif" font-size="9" fill="#4a5568" text-anchor="middle">2025</text>

                <!-- Unit -->
                <text x="480" y="180" font-family="Source Sans Pro, sans-serif" font-size="8" fill="#718096" text-anchor="end">单位：亿元人民币</text>
            </svg>
            <div class="source">数据来源：行业研究估算</div>
        </div>

        <!-- Chart Guide & Key Insights Example -->
        <div class="chart-guide">
            <strong>📊 读图指引：</strong>
            <ul>
                <li>深蓝色柱状图为当年市场规模，柱顶数字为具体金额</li>
                <li>X轴为年份（2020-2025），Y轴为市场规模（亿元）</li>
                <li>关注2020-2025年的整体增长趋势，以及近两年增速是否放缓</li>
            </ul>
        </div>

        <div class="key-insights">
            <strong>💡 关键洞察：</strong>
            <ul>
                <li><strong>趋势判断：</strong>市场规模从2,800亿元增长至4,200亿元，5年CAGR约8.4%，保持稳健增长</li>
                <li><strong>对比发现：</strong>2025年同比增7.7%，较2024年的10.1%增速放缓2.4个百分点</li>
                <li><strong>行动启示：</strong>市场增长动能有所减弱，建议关注消费复苏节奏</li>
            </ul>
        </div>

        <!-- SVG Pie Chart + Bar Chart -->
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20pt;">
            <!-- Pie Chart: Channel Distribution -->
            <div class="chart-container" style="margin: 0;">
                <div class="chart-title">图2：渠道构成（2025）</div>
                <svg class="chart-svg" viewBox="0 0 200 160" xmlns="http://www.w3.org/2000/svg">
                    <circle cx="70" cy="70" r="50" fill="none" stroke="#1a365d" stroke-width="30"
                        stroke-dasharray="172.8 314" stroke-dashoffset="0" transform="rotate(-90 70 70)"/>
                    <circle cx="70" cy="70" r="50" fill="none" stroke="#2c5282" stroke-width="30"
                        stroke-dasharray="94.2 314" stroke-dashoffset="-172.8" transform="rotate(-90 70 70)"/>
                    <circle cx="70" cy="70" r="50" fill="none" stroke="#3182ce" stroke-width="30"
                        stroke-dasharray="47.1 314" stroke-dashoffset="-267" transform="rotate(-90 70 70)"/>
                    <rect x="135" y="25" width="12" height="12" fill="#1a365d"/>
                    <text x="152" y="35" font-family="Source Sans Pro, sans-serif" font-size="9" fill="#1a202c">线下门店</text>
                    <text x="175" y="35" font-family="IBM Plex Mono, monospace" font-size="9" fill="#1a365d" font-weight="600">55%</text>
                    <rect x="135" y="45" width="12" height="12" fill="#2c5282"/>
                    <text x="152" y="55" font-family="Source Sans Pro, sans-serif" font-size="9" fill="#1a202c">传统电商</text>
                    <text x="175" y="55" font-family="IBM Plex Mono, monospace" font-size="9" fill="#2c5282" font-weight="600">30%</text>
                    <rect x="135" y="65" width="12" height="12" fill="#3182ce"/>
                    <text x="152" y="75" font-family="Source Sans Pro, sans-serif" font-size="9" fill="#1a202c">直播电商</text>
                    <text x="175" y="75" font-family="IBM Plex Mono, monospace" font-size="9" fill="#3182ce" font-weight="600">15%</text>
                </svg>
            </div>

            <!-- Bar Chart: Regional Growth -->
            <div class="chart-container" style="margin: 0;">
                <div class="chart-title">图3：区域增速对比（2025）</div>
                <svg class="chart-svg" viewBox="0 0 180 130" xmlns="http://www.w3.org/2000/svg">
                    <line x1="30" y1="15" x2="30" y2="100" stroke="#e2e8f0" stroke-width="1"/>
                    <line x1="30" y1="100" x2="170" y2="100" stroke="#e2e8f0" stroke-width="1"/>
                    <text x="25" y="20" font-family="IBM Plex Mono, monospace" font-size="8" fill="#718096" text-anchor="end">25%</text>
                    <text x="25" y="60" font-family="IBM Plex Mono, monospace" font-size="8" fill="#718096" text-anchor="end">12%</text>
                    <text x="25" y="100" font-family="IBM Plex Mono, monospace" font-size="8" fill="#718096" text-anchor="end">0%</text>
                    <line x1="30" y1="20" x2="170" y2="20" stroke="#e2e8f0" stroke-width="0.5" stroke-dasharray="2,2"/>
                    <line x1="30" y1="60" x2="170" y2="60" stroke="#e2e8f0" stroke-width="0.5" stroke-dasharray="2,2"/>
                    <rect x="45" y="68" width="25" height="32" fill="#a0aec0"/>
                    <text x="57" y="64" font-family="IBM Plex Mono, monospace" font-size="8" fill="#718096" text-anchor="middle">8%</text>
                    <text x="57" y="115" font-family="Source Sans Pro, sans-serif" font-size="8" fill="#4a5568" text-anchor="middle">一线</text>
                    <rect x="80" y="60" width="25" height="40" fill="#a0aec0"/>
                    <text x="92" y="56" font-family="IBM Plex Mono, monospace" font-size="8" fill="#718096" text-anchor="middle">10%</text>
                    <text x="92" y="115" font-family="Source Sans Pro, sans-serif" font-size="8" fill="#4a5568" text-anchor="middle">二线</text>
                    <rect x="115" y="28" width="25" height="72" fill="#3182ce"/>
                    <text x="127" y="24" font-family="IBM Plex Mono, monospace" font-size="8" fill="#3182ce" text-anchor="middle" font-weight="600">18%</text>
                    <text x="127" y="115" font-family="Source Sans Pro, sans-serif" font-size="8" fill="#4a5568" text-anchor="middle">三四线</text>
                    <rect x="150" y="18" width="25" height="82" fill="#1a365d"/>
                    <text x="162" y="14" font-family="IBM Plex Mono, monospace" font-size="8" fill="#1a365d" text-anchor="middle" font-weight="600">22%</text>
                    <text x="162" y="115" font-family="Source Sans Pro, sans-serif" font-size="8" fill="#4a5568" text-anchor="middle">县级</text>
                </svg>
            </div>
        </div>

        <div class="page-footer">
            <span>© 2026</span>
            <span>第 <span class="page-num">5</span> 页</span>
        </div>
    </div>

    <!-- Page 6: Strategic Recommendations -->
    <div class="page page-break">
        <div class="page-header">
            <span>报告标题</span>
            <span>机密</span>
        </div>

        <h2>战略建议</h2>
        <div class="section-number">03</div>

        <div class="recommendation">
            <div class="recommendation-priority">01</div>
            <div class="recommendation-content">
                <h4>加速下沉市场渠道布局</h4>
                <p>在三四线城市开设100家品牌体验店，与当地零售商建立战略合作关系。优先考虑人口超过50万的县级市场。</p>
            </div>
        </div>

        <div class="recommendation">
            <div class="recommendation-priority">02</div>
            <div class="recommendation-content">
                <h4>构建数字化营销能力</h4>
                <p>组建20人内容营销团队，在抖音、小红书建立品牌阵地。2026年数字营销预算占比从15%提升至30%。</p>
            </div>
        </div>

        <div class="recommendation">
            <div class="recommendation-priority">03</div>
            <div class="recommendation-content">
                <h4>差异化产品矩阵</h4>
                <p>针对下沉市场开发专属产品线，定价区间下探20%。同时推出高端限量款维护品牌调性。</p>
            </div>
        </div>

        <div class="metrics-grid" style="margin-top: 30pt;">
            <div class="metric-card">
                <div class="metric-value">+15%</div>
                <div class="metric-label">预计收入增长</div>
            </div>
            <div class="metric-card">
                <div class="metric-value">8-12%</div>
                <div class="metric-label">利润率改善</div>
            </div>
            <div class="metric-card">
                <div class="metric-value">18月</div>
                <div class="metric-label">投资回收期</div>
            </div>
        </div>

        <div class="page-footer">
            <span>© 2026</span>
            <span>第 <span class="page-num">6</span> 页</span>
        </div>
    </div>

    <script>
        // Page number counter
        document.querySelectorAll('.page-num').forEach((el, i) => {
            el.textContent = i + 2; // Start from page 2
        });
    </script>
</body>
</html>
```

## Key Print Features

1. **@page Rule** — Sets exact A4 dimensions
2. **page-break-before/after** — Controls where sections split
3. **page-break-inside: avoid** — Prevents content boxes from splitting across pages
4. **Fixed Headers/Footers** — Print on every page
5. **Screen vs Print** — Hides buttons in print, shows headers/footers

## Print Instructions for Users

When the user clicks "Print / Save as PDF":

1. **Destination** → Select "Save as PDF"
2. **Paper Size** → A4
3. **Orientation** → Portrait
4. **Margins** → Minimum (to maximize content area)
5. **Options** → Check "Background graphics"
6. **Save**

## Chart Implementation Notes

**⚠️ CRITICAL: Two things must be done for proper PDF printing:**

1. **Use SVG for all charts** — NOT CSS divs
2. **Add `print-color-adjust: exact` globally** — or background colors won't print

### ⚠️ The Print Background Color Problem

By default, browsers **DO NOT print background colors and images** even if "Background graphics" is checked. You MUST add `print-color-adjust: exact` to enable background colors in PDF output.

**Required CSS fix — add to your stylesheet:**

```css
/* Enable ALL background colors in PDF print */
* {
    print-color-adjust: exact !important;
    -webkit-print-color-adjust: exact !important;
}
```

This affects:
- Table headers (`<th>`)
- Highlight boxes (`.highlight-positive`, `.highlight-negative`)
- Finding boxes (`.finding-box`)
- KPI cards (`.metric-card`)
- Executive summary boxes
- Chart backgrounds

**⚠️ Without this, even checking "Background graphics" will NOT show colors in PDF!**

### Preventing Page Breaks Inside Content Boxes

To prevent content boxes (highlight boxes, finding boxes, recommendation cards) from being **split across pages**, add `page-break-inside: avoid` to each:

```css
.highlight-negative,
.highlight-positive,
.finding-box,
.recommendation,
.swot-box,
.executive-summary,
.metric-card {
    page-break-inside: avoid;
}
```

**Use `.page-break` class to force page breaks before sections:**
```html
<div class="page page-break">  <!-- This starts on a new page -->
```

**Use `.no-break` class to prevent breaks inside elements:**
```html
<div class="no-break">  <!-- Won't be split across pages -->
```

| Class | Purpose |
|-------|---------|
| `.page-break` | Force page break BEFORE this element |
| `.no-break` | Add `page-break-inside: avoid` |
| `page-break-inside: avoid` | CSS property to prevent splits |

### ✅ CORRECT: SVG Charts

All charts MUST use inline SVG for print compatibility:

```html
<svg class="chart-svg" viewBox="0 0 500 200" xmlns="http://www.w3.org/2000/svg">
    <!-- Bar chart: use <rect> elements -->
    <rect x="60" y="94" width="50" height="56" fill="#1a365d"/>

    <!-- Pie chart: use <circle> with stroke-dasharray -->
    <circle cx="70" cy="70" r="50" fill="none" stroke="#1a365d"
        stroke-width="30" stroke-dasharray="172.8 314"/>

    <!-- Line chart: use <polyline> or <path> -->
    <polyline points="0,100 50,80 100,90" fill="none" stroke="#3182ce"/>
</svg>
```

**SVG advantages:**
- Vector graphics — crisp at any zoom/print resolution
- Native browser print support — guaranteed to render in PDF
- Small file size — no external dependencies
- Accessible — works with screen readers

### CSS Required for SVG Charts

```css
.chart-svg {
    width: 100%;
    height: auto;
    print-color-adjust: exact;
    -webkit-print-color-adjust: exact;
}
```

### Chart Types & SVG Implementation

| Chart Type | SVG Element | Example |
|------------|-------------|---------|
| Bar Chart | `<rect>` | Vertical bars with `height` and `y` positioning |
| Pie/Donut | `<circle>` + `stroke-dasharray` | Circle with dashed stroke trick |
| Line Chart | `<polyline>` or `<path>` | Points connected with stroke |
| Horizontal Bar | `<rect>` | Horizontal bars with `width` |
| Stacked Bar | Multiple `<rect>` | Bars layered on top of each other |

### ❌ WRONG: CSS Charts (Do Not Use)

```css
/* DO NOT USE - Does not print! */
.bar {
    height: 80pt;
    background: var(--chart-1);
}
```

```html
<!-- DO NOT USE - Does not print! -->
<div class="bar" style="height: 80pt;"></div>
```

### Print Testing Checklist

After generating any report with charts:
1. Open HTML in browser
2. File → Print → Save as PDF
3. Verify ALL charts appear in the PDF
4. If charts are missing → Convert to SVG immediately

---

## Additional Components

### Data Audit Markers (for post-audit reports)

When a report has been audited and contains corrections or flagged data:

```css
/* Audit markers for verified data */
.audit-verified {
    position: relative;
    border-bottom: 2px dotted var(--success);
}

/* Audit markers for corrected data */
.audit-corrected {
    background: var(--success-bg);
    padding: 2px 6px;
    border-radius: 4px;
    text-decoration: line-through;
    color: var(--text-muted);
}

.audit-corrected::after {
    content: ' → 修正值';
    background: var(--success-bg);
    color: var(--success);
    font-size: 9pt;
}

/* Audit markers for data needing verification */
.audit-verify {
    background: var(--warning-bg);
    padding: 2px 6px;
    border-radius: 4px;
}

.audit-verify::after {
    content: ' ⚠️';
    color: var(--warning);
}

/* Audit markers for errors */
.audit-error {
    background: var(--danger-bg);
    padding: 2px 6px;
    border-radius: 4px;
    text-decoration: line-through;
}

.audit-error::after {
    content: ' ❌ 错误';
    background: var(--danger-bg);
    color: var(--danger);
    font-size: 9pt;
}
```

### Waterfall Chart (SVG)

```html
<div class="chart-container">
    <div class="chart-title">图4：收入变动分解（2024→2025）</div>
    <svg class="chart-svg" viewBox="0 0 500 180" xmlns="http://www.w3.org/2000/svg">
        <!-- Base line -->
        <line x1="40" y1="100" x2="480" y2="100" stroke="#e2e8f0" stroke-width="1"/>

        <!-- Starting point: 2024 Revenue -->
        <rect x="50" y="60" width="40" height="40" fill="#1a365d"/>
        <text x="70" y="55" font-family="IBM Plex Mono" font-size="9" fill="#1a365d" text-anchor="middle">3,376</text>
        <text x="70" y="115" font-family="Source Sans Pro" font-size="8" fill="#718096" text-anchor="middle">2024</text>

        <!-- Increase: Product A -->
        <rect x="120" y="45" width="40" height="15" fill="#38a169"/>
        <text x="140" y="55" font-family="JetBrains Mono" font-size="8" fill="#38a169" text-anchor="middle">+180</text>
        <line x1="90" y1="60" x2="120" y2="60" stroke="#a0aec0" stroke-dasharray="2,2"/>

        <!-- Decrease: Price pressure -->
        <rect x="190" y="50" width="40" height="10" fill="#c53030"/>
        <text x="210" y="68" font-family="JetBrains Mono" font-size="8" fill="#c53030" text-anchor="middle">-95</text>
        <line x1="160" y1="60" x2="190" y2="60" stroke="#a0aec0" stroke-dasharray="2,2"/>

        <!-- Increase: Volume growth -->
        <rect x="260" y="38" width="40" height="12" fill="#38a169"/>
        <text x="280" y="48" font-family="JetBrains Mono" font-size="8" fill="#38a169" text-anchor="middle">+120</text>
        <line x1="230" y1="60" x2="260" y2="60" stroke="#a0aec0" stroke-dasharray="2,2"/>

        <!-- Increase: New products -->
        <rect x="330" y="25" width="40" height="13" fill="#38a169"/>
        <text x="350" y="35" font-family="JetBrains Mono" font-size="8" fill="#38a169" text-anchor="middle">+168</text>
        <line x1="300" y1="60" x2="330" y2="60" stroke="#a0aec0" stroke-dasharray="2,2"/>

        <!-- Ending point: 2025 Revenue -->
        <rect x="390" y="10" width="40" height="50" fill="#1a365d"/>
        <text x="410" y="5" font-family="IBM Plex Mono" font-size="9" fill="#1a365d" text-anchor="middle">3,649</text>
        <line x1="370" y1="60" x2="390" y2="60" stroke="#a0aec0" stroke-dasharray="2,2"/>
        <text x="410" y="115" font-family="Source Sans Pro" font-size="8" fill="#718096" text-anchor="middle">2025</text>

        <!-- Legend -->
        <rect x="450" y="30" width="10" height="10" fill="#38a169"/>
        <text x="465" y="40" font-family="Source Sans Pro" font-size="8" fill="#4a5568">增加</text>
        <rect x="450" y="50" width="10" height="10" fill="#c53030"/>
        <text x="465" y="60" font-family="Source Sans Pro" font-size="8" fill="#4a5568">减少</text>
    </svg>
</div>
```

### Comparison Table

```html
<table class="comparison-table">
    <thead>
        <tr>
            <th>指标</th>
            <th>2024</th>
            <th>2025</th>
            <th>变动</th>
            <th>趋势</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>收入（亿元）</td>
            <td>3,376</td>
            <td>3,649</td>
            <td class="positive">+8.1%</td>
            <td><span class="trend-up">📈</span></td>
        </tr>
        <tr>
            <td>毛利率</td>
            <td>32.5%</td>
            <td>31.2%</td>
            <td class="negative">-1.3pp</td>
            <td><span class="trend-down">📉</span></td>
        </tr>
        <tr>
            <td>市场份额</td>
            <td>68%</td>
            <td>61%</td>
            <td class="negative">-7pp</td>
            <td><span class="trend-down">📉</span></td>
        </tr>
    </tbody>
</table>

<style>
    .comparison-table td.positive {
        color: #38a169;
        font-weight: 600;
    }
    .comparison-table td.negative {
        color: #c53030;
        font-weight: 600;
    }
    .trend-up { color: #38a169; }
    .trend-down { color: #c53030; }
</style>
```

### KPI Dashboard Card

```html
<div class="kpi-dashboard">
    <div class="kpi-card">
        <div class="kpi-label">收入</div>
        <div class="kpi-value">3,649<span class="kpi-unit">亿</span></div>
        <div class="kpi-change positive">+8.1%</div>
        <div class="kpi-sparkline">
            <svg viewBox="0 0 100 30">
                <polyline points="0,25 20,22 40,20 60,15 80,12 100,8"
                    fill="none" stroke="#38a169" stroke-width="2"/>
            </svg>
        </div>
    </div>
    <div class="kpi-card">
        <div class="kpi-label">毛利率</div>
        <div class="kpi-value">31.2<span class="kpi-unit">%</span></div>
        <div class="kpi-change negative">-1.3pp</div>
        <div class="kpi-sparkline">
            <svg viewBox="0 0 100 30">
                <polyline points="0,10 20,12 40,15 60,14 80,18 100,20"
                    fill="none" stroke="#c53030" stroke-width="2"/>
            </svg>
        </div>
    </div>
</div>

<style>
    .kpi-dashboard {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
        gap: 16px;
        margin: 16px 0;
    }
    .kpi-card {
        background: white;
        border: 1px solid #e2e8f0;
        border-radius: 12px;
        padding: 16px;
        text-align: center;
    }
    .kpi-label {
        font-size: 11px;
        color: #718096;
        text-transform: uppercase;
        letter-spacing: 0.5px;
        margin-bottom: 8px;
    }
    .kpi-value {
        font-family: var(--font-mono);
        font-size: 28px;
        font-weight: 700;
        color: #1a365d;
    }
    .kpi-unit {
        font-size: 14px;
        font-weight: 400;
        color: #718096;
    }
    .kpi-change {
        font-size: 12px;
        font-weight: 600;
        margin-top: 4px;
    }
    .kpi-change.positive { color: #38a169; }
    .kpi-change.negative { color: #c53030; }
    .kpi-sparkline {
        margin-top: 12px;
        height: 30px;
    }
    .kpi-sparkline svg {
        width: 100%;
        height: 100%;
    }
</style>
```

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 2.0 | 2026-04-11 | Added audit markers, waterfall chart, comparison table, KPI dashboard |
| 1.0 | 2026-01-01 | Initial template release |
