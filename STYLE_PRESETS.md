# A4 Report Style Presets

Curated consulting firm styles for professional A4 reports. Each preset reflects the visual identity of top-tier management consulting firms.

---

## 1. McKinsey Blue

**Vibe:** Authoritative, executive, classic consulting

**Typography:**
- Headlines: `Playfair Display` (700) — elegant serif for gravitas
- Body: `Source Sans Pro` (400/600) — clean, readable sans-serif
- Data: `IBM Plex Mono` (400) — for numbers and tables

**Colors:**
```css
:root {
    --primary: #1a365d;
    --primary-dark: #0f2444;
    --primary-light: #2c5282;

    --accent: #3182ce;
    --accent-light: #63b3ed;

    --text-primary: #1a202c;
    --text-secondary: #4a5568;
    --text-muted: #718096;

    --bg-white: #ffffff;
    --bg-light: #f7fafc;
    --bg-accent: #ebf4ff;

    --chart-1: #1a365d;
    --chart-2: #2c5282;
    --chart-3: #3182ce;
    --chart-4: #63b3ed;
    --chart-5: #90cdf4;
}
```

**Signature Elements:**
- Deep navy headers with white text
- Clean horizontal rules as section dividers
- Simple bar charts with navy/blue palette
- Minimal ornamentation
- Executive summary box with light blue background

---

## 2. BCG Silver

**Vibe:** Modern, geometric, structured

**Typography:**
- Headlines: `Inter` (700) — modern, precise sans-serif
- Body: `Inter` (400/500) — consistent, highly legible
- Data: `Inter` (500) — tabular figures

**Colors:**
```css
:root {
    --primary: #2d3748;
    --primary-dark: #1a202c;
    --primary-light: #4a5568;

    --accent: #3182ce;
    --accent-alt: #ed8936;
    --silver: #a0aec0;

    --text-primary: #1a202c;
    --text-secondary: #4a5568;
    --text-muted: #a0aec0;

    --bg-white: #ffffff;
    --bg-light: #f7fafc;
    --bg-grid: #edf2f7;

    --chart-1: #2d3748;
    --chart-2: #3182ce;
    --chart-3: #ed8936;
    --chart-4: #38a169;
    --chart-5: #805ad5;
}
```

**Signature Elements:**
- Geometric 2x2 matrices prominently featured
- Grid-based layouts with visible structure
- Orange accent for emphasis and highlights
- Silver/gray palette dominates
- Modular section boxes with subtle borders

---

## 3. Bain Red

**Vibe:** Bold, data-driven, impactful

**Typography:**
- Headlines: `DM Serif Display` (400) — distinctive, confident
- Body: `Work Sans` (400/500) — modern, professional
- Data: `JetBrains Mono` (400) — for key metrics

**Colors:**
```css
:root {
    --primary: #c53030;
    --primary-dark: #9b2c2c;
    --primary-light: #fc8181;

    --accent: #2d3748;
    --accent-slate: #4a5568;

    --text-primary: #1a202c;
    --text-secondary: #4a5568;
    --text-muted: #a0aec0;

    --bg-white: #ffffff;
    --bg-light: #fff5f5;
    --bg-red-accent: #fffaf0;

    --chart-1: #c53030;
    --chart-2: #2d3748;
    --chart-3: #3182ce;
    --chart-4: #38a169;
    --chart-5: #d69e2e;
}
```

**Signature Elements:**
- Bold red accents for key metrics and callouts
- Large, impactful numbers (big number style)
- Waterfall charts for variance analysis
- Strong visual hierarchy with red section markers
- Data tables with red header rows

---

## Font Pairing Quick Reference

| Preset       | Headline Font           | Body Font        | Data Font       |
| ------------ | ----------------------- | ---------------- | --------------- |
| McKinsey Blue | Playfair Display (700)  | Source Sans Pro  | IBM Plex Mono   |
| BCG Silver   | Inter (700)             | Inter            | Inter           |
| Bain Red     | DM Serif Display (400)  | Work Sans        | JetBrains Mono  |

---

## CSS Chart Colors Across Presets

| Chart Color | McKinsey | BCG     | Bain     |
| ----------- | -------- | ------- | -------- |
| 1           | #1a365d  | #2d3748 | #c53030  |
| 2           | #2c5282  | #3182ce | #2d3748  |
| 3           | #3182ce  | #ed8936 | #3182ce  |
| 4           | #63b3ed  | #38a169 | #38a169  |
| 5           | #90cdf4  | #805ad5 | #d69e2e  |

---

## DO NOT USE

**Fonts:** Comic Sans, Papyrus, generic system fonts

**Colors:** Rainbow palettes, neon colors, pastel gradients

**Layouts:** Centered-only content, excessive whitespace, cluttered charts

**Content:** Marketing speak, unsubstantiated claims, vague recommendations

---

## Page Element Sizing

| Element              | McKinsey     | BCG           | Bain           |
| -------------------- | ------------ | ------------- | -------------- |
| Page margin          | 20mm         | 18mm          | 22mm           |
| Section gap          | 24pt         | 20pt          | 28pt           |
| Paragraph spacing    | 8pt          | 6pt           | 10pt           |
| Chart height (max)   | 180pt        | 160pt         | 200pt          |
| Table row height     | 24pt         | 22pt          | 26pt           |
