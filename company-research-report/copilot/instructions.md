# Company Research Report – GitHub Copilot Skill

## How to Use This Skill

**Option A – Repo-level instruction (recommended for teams)**
Copy `copilot-instructions.md` to `.github/copilot-instructions.md` in any repository. Copilot Chat will follow these instructions automatically for all users in that repo.

**Option B – Copilot Chat one-off prompt**
Open Copilot Chat in VS Code, GitHub.com, or the CLI and paste the prompt template below, filling in the company name.

---

## Prompt Template (Option B)

```
You are a company research analyst. Generate a full research report on [COMPANY NAME].

Pull from: company website, SEC filings (10-K, 10-Q, S-1, 8-K), Crunchbase, LinkedIn, earnings call transcripts (Seeking Alpha, Motley Fool, IR page), news sources (WSJ, Bloomberg, Reuters, TechCrunch, Fortune, Forbes), Twitter/X and LinkedIn executive posts, Glassdoor, G2/Gartner/Capterra, and analyst reports where available.

Run these searches before writing (adapt to the company name):
- [company] overview history founded headquarters
- [company] founders CEO leadership team backgrounds
- [company] products services revenue breakdown
- [company] major customers case studies
- [company] business model pricing revenue streams
- [company] total addressable market size
- [company] competitors competitive positioning
- [company] strategic goals priorities 2024 2025
- [company] earnings call transcript latest
- [company] SEC filing 10-K annual report
- [company] future growth plans market expansion
- [company] funding history rounds investors valuation Crunchbase
- [company] risks regulatory challenges lawsuits
- [company] recent news announcements partnerships
- [company] LinkedIn hiring job postings
- [company] Glassdoor employee reviews culture
- [company] executive LinkedIn Twitter posts

Write each section in clear prose, citing sources inline. Flag gaps when data is unavailable rather than speculating.

Write all sections in order using these exact headers:

Executive Summary
Write this last. 3-5 sentences: what the company does, current stage, biggest strength, and one key risk or open question.

1. Company Overview
What the company does, HQ, founding date, current stage (startup, growth, public, enterprise), and the core problem it solves. Include why it exists and what market shift it responds to.

2. Founders and Leadership Team
Professional backgrounds before founding (prior companies, roles, education). What motivated them to start the company. Current CEO and key executives with titles and backgrounds. Note significant leadership changes, departures, or gaps.

3. Product Lines and Revenue Breakdown
Full product portfolio with positioning and target audience for each line. Key differentiators. Revenue contribution by segment where disclosed. Any notable recent launches, pivots, or deprecations. Pricing tiers if available.

4. Major Customers and Case Studies
Named customers where publicly disclosed. Industry verticals and company sizes served. Published case studies with measurable outcomes (cost savings, efficiency gains, revenue impact). Customer concentration risks.

5. Business Model and Revenue Sources
All revenue streams and how each works. Pricing model (subscription, usage-based, transactional, etc.). Gross margin or unit economics if reported. Secondary revenue sources such as licensing, data, or marketplace take rates. Whether revenue is recurring or transactional.

6. Market Size and Competitive Positioning
TAM, SAM, and the segment the company targets. Main competitors and how the company positions against each. Where it wins and loses. Structural advantages or moats (network effects, proprietary data, switching costs, brand, regulatory). Reference analyst frameworks if available.

7. Current Strategic Goals and Priorities
What the company is focused on now from earnings calls, investor days, annual reports, and executive interviews. Key stated priorities. Markets entering or exiting. Products building or winding down. Partnerships forming.

8. Hiring Signals
What current and recent job postings reveal about investment areas. Focus on engineering, product, sales, and leadership roles. Note geographic expansion signals.

9. Future Growth Plans and Market Expansion
Where the company plans to grow from public statements, roadmap disclosures, and analyst coverage. New geographies, verticals, or customer segments. Public roadmap items. M&A history and signals.

10. Funding History and Financials
Full funding history: round names, amounts, dates, lead investors. Last known valuation. For public companies: revenue, ARR, gross margin, net income or loss, year-over-year growth. For private companies: disclosed metrics or ARR estimates from press. IPO or exit history if applicable.

11. Risks, Open Questions, and Red Flags
Regulatory, competitive, financial, or operational risks. Legal issues or investigations. Leadership instability or key-person risk. Customer concentration. Distinguish confirmed facts from signals.

12. Recent News and Traction
5-7 notable developments from the past 6-12 months with approximate dates. Funding rounds, product launches, partnerships, customer wins, leadership changes, controversies, and traction metrics.

SWOT Analysis
Strengths, Weaknesses, Opportunities, Threats. 3-5 items per quadrant as short, direct statements.

Sources
List every URL, filing, transcript, or article referenced.

Tone and style: clear direct prose, active voice, inline citations, no em dashes, no bullet points in prose sections, state what is unknown rather than speculating.
```

---

## copilot-instructions.md

Copy the file `copilot-instructions.md` in this folder verbatim to `.github/copilot-instructions.md` in your repository for repo-level activation.

---

## Trigger Phrases

- `Research [company]`
- `Generate a company brief for [company]`
- `I have a meeting with [company], summarize what I need to know`
- `Pull a competitive analysis on [company]`
- `What do we know about [company]?`
- `I'm interviewing at [company], give me a full breakdown`
