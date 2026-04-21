---
name: company-research-report
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

### Page Setup
Use `SimpleDocTemplate` with `letter` pagesize. Margins: 0.75 inches on all sides. Register a `onFirstPage` / `onLaterPages` canvas callback for the footer.

### Typography
- Report title: 24pt Helvetica-Bold
- Section headers: 14pt Helvetica-Bold, primary color (#1B3A6B)
- Body text: 10pt Times-Roman, leading 14
- Captions: 9pt Helvetica italic
- Muted labels: 9pt Helvetica, color #555555

### Color Palette
- Primary: #1B3A6B (dark navy)
- Accent: #2D7DD2 (blue)
- Light background: #F4F6F9
- Text: #1A1A1A
- Muted: #555555
- SWOT green: #2E7D32
- SWOT red: #C62828
- SWOT blue: #1565C0
- SWOT orange: #E65100

### Cover Page
Page 1 only. Include:
- Company name as the title in primary color
- "Research Report" as subtitle in accent color
- Date generated (formatted as Month DD, YYYY)
- A horizontal rule in accent color below the subtitle
- A one-line company tagline or descriptor if found during research

### Executive Summary Block
On page 2, before Section 1. Render inside a `Table` with a light background (#F4F6F9) and a 2pt left border in accent color. Label it "Executive Summary" in bold above the box.

### Charts
Generate with `matplotlib`. Save each chart as a PNG to `/tmp/` then embed using ReportLab's `Image` flowable. Set `width` to fit within the page margins (approximately 6.5 inches). Set `height` proportionally.

Charts to produce where data is available:

1. Funding History Bar Chart
   - X-axis: round name (Seed, Series A, Series B, etc.)
   - Y-axis: amount raised in $M
   - Bar color: accent color
   - Title: "[Company] Funding History"

2. Revenue Growth Chart (if multi-year data is available)
   - X-axis: year
   - Y-axis: revenue in $M or ARR in $M
   - Line chart with markers
   - Title: "[Company] Revenue Growth"

3. Competitive Positioning Matrix (if sufficient data)
   - 2x2 scatter plot
   - X-axis: relative market share (low to high)
   - Y-axis: growth rate (low to high)
   - Plot the company and its top 3-5 competitors as labeled bubbles
   - Title: "Competitive Positioning"

If data for a chart is insufficient, skip that chart and note it briefly in the relevant section.

### SWOT Table
Render as a 2x2 `Table` using `TableStyle`. Each quadrant has a colored header row and white cell body.

| Strengths (green #2E7D32) | Weaknesses (red #C62828) |
| Opportunities (blue #1565C0) | Threats (orange #E65100) |

Header text: 10pt Helvetica-Bold, white. Body text: 9pt Times-Roman. Cell padding: 8pt.

### Page Footer
On every page after the cover. Left: company name in muted color. Right: "Page N" in muted color. Draw using the canvas callback, not as a flowable.

### File Naming
Save the final PDF to:
`/mnt/user-data/outputs/[company-slug]-research-report.pdf`

Where `[company-slug]` is the company name in lowercase with hyphens (e.g., `stripe-research-report.pdf`, `openai-research-report.pdf`).

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
