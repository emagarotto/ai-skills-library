---
name: Company Research Report
description: Generate a structured, professional research report on any company and deliver it as a PDF. Use this skill whenever the user provides a company name and wants to learn about it, research it before a meeting or interview, evaluate it as a potential employer, partner, or investment target, or get a comprehensive breakdown of an organization. Trigger on phrases like "research this company", "tell me about [company]", "I have a meeting with [company]", "generate a company report", "give me a breakdown of [company]", "I'm interviewing at [company]", "do a deep dive on [company]", or any time the user wants a thorough overview of an organization. Always produce a PDF as the final output.
---

# Company Research Report Skill

## Purpose

Generate a thorough, sourced research report on any company and deliver it as a professionally formatted PDF. The report covers founders and leadership backgrounds, product lines and revenue breakdown, customers and case studies, strategic goals from earnings calls and filings, future growth plans, competitive positioning, funding history, and risks. It includes an executive summary, a SWOT analysis, and charts where data supports them.

---

## Data Sources to Search

Pull from as many of these as are available and relevant:

- Company website (About, Products, Customers, Careers, Press pages)
- SEC filings (10-K, 10-Q, S-1, 8-K) via sec.gov or direct search
- Crunchbase for funding history, investors, and valuation
- LinkedIn for leadership backgrounds and hiring signals
- Earnings call transcripts (Seeking Alpha, Motley Fool, company IR page)
- News sources: WSJ, Bloomberg, Reuters, TechCrunch, Fortune, Forbes
- Social media: Twitter/X and LinkedIn posts from executives
- Glassdoor for culture and employee sentiment
- G2, Gartner, Capterra for product reviews and competitive positioning
- Industry analyst reports where available (Gartner Magic Quadrant, Forrester Wave)

---

## Research Process

### Step 1: Gather Information

Run web searches across all required topics. Adapt each query to the company name. Fetch full pages where snippets are too thin.

Queries to run:

- `[company] overview history founded headquarters`
- `[company] founders CEO leadership team backgrounds`
- `[company] products services revenue breakdown`
- `[company] major customers case studies`
- `[company] business model pricing revenue streams`
- `[company] total addressable market size`
- `[company] competitors competitive positioning`
- `[company] strategic goals priorities 2024 2025`
- `[company] earnings call transcript latest`
- `[company] SEC filing 10-K annual report`
- `[company] future growth plans market expansion`
- `[company] funding history rounds investors valuation Crunchbase`
- `[company] risks regulatory challenges lawsuits`
- `[company] recent news announcements partnerships`
- `[company] LinkedIn hiring job postings`
- `[company] Glassdoor employee reviews culture`
- `[company] executive LinkedIn Twitter posts`

### Step 2: Synthesize

Write each section in your own words. Do not paste raw search snippets. Prioritize primary sources (company website, SEC filings, earnings call transcripts, press releases) over secondary aggregators. When citing a figure or claim, note the source inline.

### Step 3: Flag Gaps

If a section lacks reliable data (e.g., revenue for a private company, undisclosed funding), state clearly what is unknown and why, rather than speculating.

---

## Report Sections

Write all sections in order using the exact header names below.

### Executive Summary
Write this last, after all other sections are complete. 3-5 sentences covering what the company does, its current stage, its biggest strength, and one key risk or open question. Render this in a shaded box at the top of the report body.

### 1. Company Overview
What the company does, where it is headquartered, when it was founded, its current stage (startup, growth, public, enterprise), and the core problem it solves. Include any defining context about why it exists and what market shift it responds to.

### 2. Founders and Leadership Team
Who started the company and their professional backgrounds before founding it (prior companies, roles, education). What motivated them to start the company. Current CEO and key executives with titles and backgrounds. Note significant leadership changes, departures, or gaps on the team.

### 3. Product Lines and Revenue Breakdown
The full product portfolio with a description of each line. How each product is positioned and who it targets. Key differentiators versus alternatives. Revenue contribution by product line or segment where disclosed. Any notable recent launches, pivots, or deprecations. Pricing tiers if available.

### 4. Major Customers and Case Studies
Named customers where publicly disclosed. Industry verticals and company sizes served. Published case studies with measurable outcomes (cost savings, efficiency gains, revenue impact). Any customer concentration risks. Reference logo walls or customer lists from the company website.

### 5. Business Model and Revenue Sources
How the company makes money across all revenue streams. Pricing model (subscription, usage-based, transactional, professional services, etc.). Gross margin or unit economics if reported. Secondary revenue sources such as licensing, data, marketplace take rates, or advertising. Whether revenue is recurring or transactional.

### 6. Market Size and Competitive Positioning
Total addressable market (TAM), serviceable addressable market (SAM), and the segment the company targets. Main competitors and how the company positions against each one. Where it wins and where it loses. Structural advantages or moats (network effects, proprietary data, switching costs, brand, regulatory). Reference analyst frameworks (Gartner Magic Quadrant, Forrester Wave) if available.

### 7. Current Strategic Goals and Priorities
What the company is focused on right now based on earnings calls, investor day presentations, annual reports, and executive interviews. Key stated priorities. Markets it is entering or exiting. Products it is building or winding down. Partnerships it is forming.

### 8. Hiring Signals
What current and recent job postings reveal about where the company is investing. Focus on engineering, product, sales, and leadership roles. Note geographic expansion signals. Source from LinkedIn, the company careers page, and job boards.

### 9. Future Growth Plans and Market Expansion
Where the company plans to grow based on public statements, roadmap disclosures, and analyst coverage. New geographies, verticals, or customer segments it is targeting. Public product roadmap items. M&A activity or acquisition history that signals strategic direction.

### 10. Funding History and Financials
Full funding history: round names, amounts, dates, and lead investors. Last known valuation. For public companies: revenue, ARR, gross margin, net income or loss, and year-over-year growth from the most recent filings. For private companies: disclosed revenue ranges, ARR estimates from press, or growth metrics. IPO or exit history if applicable.

### 11. Risks, Open Questions, and Red Flags
Regulatory, competitive, financial, or operational risks. Legal issues, lawsuits, or investigations. Leadership instability or key-person risk. Customer concentration or dependency. Anything in the news, on Glassdoor, or in public filings that raises questions. Distinguish clearly between confirmed facts and signals.

### 12. Recent News and Traction
5-7 notable developments from the past 6-12 months with approximate dates. Cover funding rounds, product launches, partnerships, customer wins, leadership changes, and controversies. Include revenue milestones, user growth, or other traction metrics if publicly disclosed.

### SWOT Analysis
A four-quadrant analysis based on all research above.

Strengths: Internal advantages the company has today.
Weaknesses: Internal limitations or gaps.
Opportunities: External conditions the company is positioned to benefit from.
Threats: External forces that could hurt the company.

Write 3-5 items per quadrant as short, direct statements. Render as a colored 2x2 table in the PDF (see PDF Output Instructions).

---

## PDF Output Instructions

Use `reportlab` and `matplotlib`. Install if needed:

```bash
pip install reportlab matplotlib --break-system-packages
```

---

### Accessibility Requirements (WCAG AA)

These rules are non-negotiable and apply to every element in the PDF.

**Contrast ratios:**
- Body text (under 18pt): minimum 4.5:1 contrast ratio against background
- Large text (18pt bold or 24pt regular and above): minimum 3:1 contrast ratio
- All chart labels, axis text, and captions: minimum 4.5:1
- SWOT header text (white on color): verify each header color meets 4.5:1 against white text
  - Green #2E7D32 on white text: passes at 5.1:1
  - Red #C62828 on white text: passes at 5.4:1
  - Blue #1565C0 on white text: passes at 6.9:1
  - Orange #E65100 on white text: passes at 3.8:1 — use #BF360C instead for AA compliance
- Never use color as the only means of conveying information. Every color-coded element must also use a text label, pattern, or shape.

**Text minimums:**
- Body text: minimum 10pt. Never go below 9pt even when compressing to fit one page.
- Captions and footnotes: minimum 8pt.

**Alt text for all non-text content:**
- Every chart embedded in the PDF must include a one-sentence plain-text description immediately below it as a caption. Example: "Bar chart showing Intelligems funding history across four rounds totaling $22M from 2021 to 2025."
- The SWOT table must include a text summary paragraph above it: "The following table summarizes the company's internal strengths and weaknesses alongside external opportunities and threats."
- Every visual callout block (executive summary box, sidebar) must be readable as plain text without relying on its visual styling.

**Reading order:**
- Content must flow in logical reading order: cover, executive summary, sections 1-12, SWOT, sources.
- Do not use absolute positioning or canvas drawString for body content. Use ReportLab flowables (Paragraph, Table, Spacer) so reading order is preserved in the document structure.
- Use canvas drawString only for page headers and footers.

**Document metadata:**
Set the following on the PDF canvas before saving:
```python
canvas.setTitle("[Company] Research Report")
canvas.setAuthor("Company Research Report Skill")
canvas.setSubject("Company Research and Competitive Analysis")
```

---

### Type System

Use a modern, professional sans-serif and serif pairing.

**Primary font (headings):** Helvetica-Bold
**Body font:** Helvetica (not Times-Roman — cleaner on screen and print)
**Accent font:** Helvetica-Oblique for captions and pull quotes

| Element | Font | Size | Weight | Color |
|---|---|---|---|---|
| Cover title | Helvetica-Bold | 28pt | Bold | Primary #1B3A6B |
| Cover subtitle | Helvetica | 14pt | Regular | Accent #2D7DD2 |
| Cover date/tagline | Helvetica | 10pt | Regular | Muted #555555 |
| Section number | Helvetica-Bold | 9pt | Bold | Accent #2D7DD2 |
| Section header | Helvetica-Bold | 13pt | Bold | Primary #1B3A6B |
| Body text | Helvetica | 10pt | Regular | Text #1A1A1A |
| Body leading | — | 15pt | — | — |
| Bullet text | Helvetica | 10pt | Regular | Text #1A1A1A |
| Caption / alt text | Helvetica-Oblique | 8.5pt | Oblique | Muted #555555 |
| Footer text | Helvetica | 8pt | Regular | Muted #555555 |
| Executive summary | Helvetica | 10pt | Regular | Text #1A1A1A |
| Pull quote | Helvetica-Bold | 11pt | Bold | Primary #1B3A6B |

---

### Color Palette

All colors verified at WCAG AA contrast on white backgrounds unless noted.

| Role | Hex | Usage |
|---|---|---|
| Primary | #1B3A6B | Section headers, cover title, pull quotes |
| Accent | #2D7DD2 | Rules, borders, section numbers, links |
| Light background | #F4F6F9 | Executive summary block, callout boxes |
| Text | #1A1A1A | All body text |
| Muted | #555555 | Captions, footers, dates |
| SWOT Strengths | #2E7D32 | Header row only, white text on top |
| SWOT Weaknesses | #C62828 | Header row only, white text on top |
| SWOT Opportunities | #1565C0 | Header row only, white text on top |
| SWOT Threats | #BF360C | Header row only, white text on top (AA compliant replacement for #E65100) |
| Chart primary | #2D7DD2 | Bar fills, line strokes |
| Chart secondary | #1B3A6B | Comparison bars or secondary data series |
| Chart background | #FFFFFF | Plot area background |
| Chart gridlines | #E0E0E0 | Horizontal gridlines only |

---

### Spacing System

Use consistent vertical rhythm throughout. Define these as constants in the Python script:

```python
SPACE_XS  = 4   # Between caption and next element
SPACE_SM  = 8   # Between bullet items
SPACE_MD  = 14  # Between paragraphs
SPACE_LG  = 20  # Between sections
SPACE_XL  = 32  # After cover elements, before first section
```

---

### Cover Page

Page 1 only. No page number on the cover.

Layout from top to bottom:
1. Top rule: 4pt horizontal line in accent color, full width, at top margin
2. Vertical spacer: SPACE_XL
3. Company name: 28pt Helvetica-Bold, primary color, left-aligned
4. "Research Report" label: 14pt Helvetica, accent color, left-aligned, SPACE_SM below company name
5. Horizontal rule: 1pt in accent color, full width, SPACE_SM below subtitle
6. Company tagline or one-line descriptor: 10pt Helvetica, muted color, SPACE_SM below rule
7. Date generated: 10pt Helvetica, muted color, formatted as "April 21, 2026"
8. Bottom rule: 4pt horizontal line in primary color, full width, at bottom margin

---

### Executive Summary Block

Immediately after the cover, before Section 1.

Render as a `Table` with:
- Background: #F4F6F9
- Left border: 3pt solid accent color (#2D7DD2)
- Padding: 12pt all sides
- Label "Executive Summary" above the box in 11pt Helvetica-Bold, primary color
- Body text: 10pt Helvetica, leading 15, text color #1A1A1A
- SPACE_LG below the block before Section 1 begins

---

### Section Headers

Each section header follows this pattern:
1. Section number badge: 9pt Helvetica-Bold, accent color (#2D7DD2), inline before the title
2. Section title: 13pt Helvetica-Bold, primary color (#1B3A6B)
3. Rule: 0.75pt horizontal line, accent color, full width, SPACE_XS below title
4. SPACE_MD before body text begins

Example: "1. Company Overview" where "1." renders in accent and "Company Overview" renders in primary.

---

### Callout Blocks

Use for key data points, notable quotes from executives, or single high-impact facts found during research.

Render as a `Table` with:
- Left border: 3pt solid primary color (#1B3A6B)
- Background: white
- Padding: 10pt left, 8pt top/bottom, 6pt right
- Text: 11pt Helvetica-Bold, primary color
- Use sparingly: maximum 2 callout blocks per report

---

### Charts

Generate with `matplotlib`. Apply these style rules to every chart before saving.

**Global chart style:**
```python
import matplotlib.pyplot as plt
import matplotlib as mpl

mpl.rcParams.update({
    'font.family': 'sans-serif',
    'font.sans-serif': ['Arial', 'Helvetica', 'DejaVu Sans'],
    'font.size': 10,
    'axes.titlesize': 12,
    'axes.titleweight': 'bold',
    'axes.titlecolor': '#1B3A6B',
    'axes.labelsize': 10,
    'axes.labelcolor': '#1A1A1A',
    'axes.edgecolor': '#E0E0E0',
    'axes.linewidth': 0.8,
    'axes.facecolor': '#FFFFFF',
    'figure.facecolor': '#FFFFFF',
    'xtick.color': '#555555',
    'ytick.color': '#555555',
    'xtick.labelsize': 9,
    'ytick.labelsize': 9,
    'grid.color': '#E0E0E0',
    'grid.linewidth': 0.6,
    'grid.axis': 'y',
})
```

**Chart dimensions:** width 6.5 inches, height 3.2 inches. Save to `/tmp/` as PNG at 150 DPI.

**Alt text caption:** immediately below every embedded chart, render a one-sentence plain-text description in 8.5pt Helvetica-Oblique, muted color (#555555).

**Chart 1: Funding History Bar Chart**
- X-axis: round name (Seed, Series A, etc.) in 9pt, muted color
- Y-axis: amount raised in $M, label "Amount Raised ($M)"
- Bars: fill color #2D7DD2, edge color #1B3A6B, linewidth 0.5, bar width 0.55
- Data labels: amount in $M centered above each bar, 9pt bold, primary color
- Title: "[Company] Funding History", 12pt bold, primary color
- No top or right spine
- Alt text caption: "Bar chart showing [company] funding history by round."

**Chart 2: Revenue Growth Chart** (if multi-year data is available)
- X-axis: year
- Y-axis: revenue or ARR in $M
- Line: color #2D7DD2, linewidth 2, markers circle, markersize 6, markerfacecolor white, markeredgecolor #2D7DD2
- Fill under line: #2D7DD2 at 10% opacity
- Title: "[Company] Revenue Growth", 12pt bold, primary color
- No top or right spine
- Alt text caption: "Line chart showing [company] revenue growth from [year] to [year]."

**Chart 3: Competitive Positioning Matrix** (if sufficient data)
- Scatter plot with labeled bubbles for the company and top 3-5 competitors
- X-axis: relative market share (low to high), label "Relative Market Share"
- Y-axis: relative growth rate (low to high), label "Relative Growth Rate"
- Subject company bubble: color #1B3A6B, size 180, zorder 5
- Competitor bubbles: color #2D7DD2 at 60% opacity, size 120
- Labels: 9pt, offset slightly above each bubble, primary color for subject company, muted for competitors
- Light quadrant lines at 0.5/0.5 intersection: #E0E0E0, linewidth 0.8, dashed
- Note below chart: "Note: positions estimated from available public data."
- Alt text caption: "Scatter chart showing competitive positioning of [company] versus key competitors by market share and growth rate."

---

### SWOT Table

Render as a 2x2 `Table` using `TableStyle`.

Before the table, add this paragraph in 10pt Helvetica, body color:
"The following table summarizes the company's internal strengths and weaknesses alongside external opportunities and threats."

Table layout:
- Top-left: Strengths, header #2E7D32
- Top-right: Weaknesses, header #C62828
- Bottom-left: Opportunities, header #1565C0
- Bottom-right: Threats, header #BF360C

Each quadrant:
- Header row: 10pt Helvetica-Bold, white text, 8pt padding
- Body: 9pt Helvetica, text color #1A1A1A, white background, 8pt padding
- Items as short bullet statements using → prefix
- Grid lines: 0.5pt, color #E0E0E0

---

### Page Footer

On every page after the cover. Draw using canvas callback, not as a flowable.

- Left: company name, 8pt Helvetica, muted color (#555555)
- Center: skill name "Company Research Report", 8pt Helvetica, muted color
- Right: "Page N of M", 8pt Helvetica, muted color
- Top border of footer: 0.5pt rule in #E0E0E0 across full width

---

### File Naming

Save to:
`/mnt/user-data/outputs/[company-slug]-research-report.pdf`

Where `[company-slug]` is the company name in lowercase with hyphens (e.g., `stripe-research-report.pdf`).

After saving, use `present_files` to deliver the PDF to the user.

---

## Tone and Style

- Write in clear, direct prose.
- Use active voice.
- Avoid filler phrases and generalizations.
- State what is known and what is not.
- Keep each section tight: enough to be useful, not so long it becomes noise.
- Do not use em dashes. Use commas, periods, or semicolons.
- Do not use bullet points in prose sections. Use short paragraphs.
- Bullet points are acceptable only in the SWOT quadrants.
