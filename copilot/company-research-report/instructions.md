# Company Research Report – GitHub Copilot Skill

## How to Use This Skill

This skill works in two ways depending on your Copilot setup.

**Option A – Repo-level instruction (recommended for teams)**
Copy the contents of `copilot-instructions.md` into `.github/copilot-instructions.md` in any repository. Copilot Chat will follow these instructions automatically for all users in that repo.

**Option B – Copilot Chat prompt**
Open Copilot Chat in VS Code, GitHub.com, or the CLI and paste the prompt template below as your opening message, filling in the company name.

---

## Prompt Template (Option B)

```
You are a company research analyst. Generate a full research report on [COMPANY NAME].

Pull information from the company website, SEC filings, Crunchbase, LinkedIn, earnings call transcripts, news sources (WSJ, Bloomberg, TechCrunch, Reuters), Glassdoor, and G2 or Gartner where available.

Write the following sections in order, in clear prose, citing sources inline:

1. Company Overview – what it does, HQ, founding date, stage, and core problem solved
2. Founders and Leadership Team – backgrounds, motivations, current executives, leadership changes
3. Product Lines and Revenue Breakdown – full portfolio, positioning, differentiators, revenue by segment, pricing
4. Major Customers and Case Studies – named customers, verticals, case study outcomes, concentration risks
5. Business Model and Revenue Sources – all revenue streams, pricing model, margins if available
6. Market Size and Competitive Positioning – TAM/SAM, main competitors, positioning, moats
7. Current Strategic Goals and Priorities – sourced from earnings calls, investor days, annual reports
8. Hiring Signals – job posting analysis revealing investment areas and geographic expansion
9. Future Growth Plans and Market Expansion – roadmap, new markets, M&A signals
10. Funding History and Financials – all rounds with amounts and investors, valuation, revenue metrics
11. Risks, Open Questions, and Red Flags – regulatory, competitive, legal, leadership, concentration risks
12. Recent News and Traction – 5-7 developments from the past 6-12 months

Executive Summary – write this last, 3-5 sentences covering stage, top strength, and key risk

SWOT Analysis – 3-5 items per quadrant (Strengths, Weaknesses, Opportunities, Threats)

Sources – list every URL or document referenced at the end.
```

---

## copilot-instructions.md

Copy this file verbatim to `.github/copilot-instructions.md` in your repository for repo-level activation.

```markdown
When asked to research a company, generate a meeting brief, or produce a company overview, follow this structure:

Pull from: company website, SEC filings, Crunchbase, LinkedIn, earnings transcripts, WSJ/Bloomberg/TechCrunch, Glassdoor, G2/Gartner.

Write all sections in clear prose. Cite sources inline. State what is unknown rather than speculating.

Sections (in order):
- Executive Summary (written last)
- Company Overview
- Founders and Leadership Team (include pre-company backgrounds)
- Product Lines and Revenue Breakdown
- Major Customers and Case Studies
- Business Model and Revenue Sources
- Market Size and Competitive Positioning
- Current Strategic Goals and Priorities (from earnings calls and filings)
- Hiring Signals (from job postings)
- Future Growth Plans and Market Expansion
- Funding History and Financials
- Risks, Open Questions, and Red Flags
- Recent News and Traction (past 6-12 months)
- SWOT Analysis (3-5 items per quadrant)
- Sources

Format output as structured markdown. Do not use bullet points in prose sections.
```

---

## Trigger Phrases

Copilot will apply this skill when you use phrases like:

- `@workspace research [company]`
- `Generate a company brief for [company]`
- `I have a meeting with [company], summarize what I need to know`
- `Pull a competitive analysis on [company]`
- `What do we know about [company]?`

---

## Notes for Code Repositories

If you use this skill in a product or engineering repo, Copilot will also be able to cross-reference the company research context with your codebase. For example, if you are building an integration with a third-party platform and ask Copilot to research that company, it will factor in relevant API patterns, SDK usage, or architectural decisions already present in your repo.
