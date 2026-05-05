---
name: job-application-kit
description: >
  Generate a tailored application kit from a job description URL and resume, then produce
  three PDFs: a Job Details summary, a filled cover letter, and a filled resume.
  Use this skill whenever the user provides a job posting URL (or pasted JD) and asks
  for application materials, a kit, a cover letter, a resume summary, a LinkedIn note,
  or contact research for a role. Also trigger when the user says things like "process
  this job", "build my kit for this role", "generate my application materials", "who
  should I contact for this job", or "write my cover letter and LinkedIn note". Always
  trigger this skill when a job posting URL is present and the user wants any of these
  outputs: contact info, cover letter, resume summary, LinkedIn outreach, or PDFs.
---

# Job Application Kit

This skill produces a full application kit in two phases:

**Phase 1 — In-chat output** (plain text, appears in the conversation):
1. Header: [Company Name] — [Job Title]
2. CONTACT
3. COVER LETTER
4. RESUME SUMMARY
5. LINKEDIN NOTE

**Phase 2 — PDF files** (created after the in-chat kit):
1. Job Details PDF — company, title, salary, full JD (for your records)
2. Cover Letter PDF — cover letter template cloned from Google Drive, ready to fill
3. Resume PDF — resume template cloned from Google Drive, ready to fill

---

## Setup required before first use

See `SETUP.md` in this folder. You must complete setup before running this skill.

---

## About You

```
YOUR_NAME: [your full name]
YOUR_TITLE: [your professional title / headline]
YOUR_RESUME_URL: [public URL to your resume PDF]
YOUR_LINKEDIN_URL: [your LinkedIn profile URL]
YOUR_SUMMARY: |
  [3-5 bullet points describing your professional identity, key roles, skills,
   certifications, differentiators, and anything that makes you stand out.
   Be specific — named companies, years of experience, measurable outcomes.
   This is the source of truth for cover letter and resume content generation.]
```

Example:
```
YOUR_NAME: Jordan Smith
YOUR_TITLE: Senior Product Designer
YOUR_RESUME_URL: https://yoursite.com/resume.pdf
YOUR_LINKEDIN_URL: https://www.linkedin.com/in/yourhandle
YOUR_SUMMARY: |
  - 10+ years of product design across SaaS, fintech, and healthcare
  - Led design at Acme Corp, Widgets Inc, and StartupCo. Managed teams of up to 6.
  - Strong in design systems, UX research, and 0-to-1 product work
  - Proficient in Figma, Framer, and AI tools including Claude Code and Lovable
  - MBA from Northwestern. Speaker at Config 2024.
```

---

## Google Drive templates

```
YOUR_FOLDER_ID: [Google Drive folder ID where cloned docs will be saved]
YOUR_COVER_LETTER_TEMPLATE_ID: [file ID of your cover letter Google Doc template]
YOUR_RESUME_TEMPLATE_ID: [file ID of your resume Google Doc template]
```

Templates must contain these exact placeholder strings:
- Cover letter template: `[[cover letter copy]]` where the body paragraphs go
- Resume template: `[[resume summary copy]]` where the professional summary goes

See `SETUP.md` for instructions on creating and sharing your templates.

---

## Step 1 — Fetch the job posting

Use `web_fetch` on the JD URL. Extract:

- Company name (the hiring org, not the job board)
- Exact job title
- Full job description (responsibilities, requirements, qualifications)
- Salary / compensation (note "Not specified" if absent)
- Hiring manager or reporting manager name, if listed

If the page is paywalled or the fetch fails, ask the user to paste the JD text.

---

## Step 2 — Fetch the resume

Use `web_fetch` on `YOUR_RESUME_URL`.

Extract all experience, skills, certifications, and project work. This is the source of
truth. Never invent credentials, companies, dates, or metrics not present here.

If the PDF is not fetchable, fall back to `YOUR_SUMMARY` in the About You section above.

---

## Step 3 — Fetch the LinkedIn profile

Use `web_fetch` on `YOUR_LINKEDIN_URL`.

Extract all roles listed on the profile, including any that do not appear in the resume.
For each role not already captured from the resume, note the company name, title, industry,
and any description or context available.

Then compare those roles against the job description. Look for:

- Industry overlap (e.g., healthcare, fintech, retail, education, sports, food/beverage)
- Functional overlap (e.g., B2B SaaS, consumer apps, enterprise software)
- Relevant context (e.g., stakeholder types, product complexity, domain knowledge)

Flag any LinkedIn-only roles where there is a clear match. Use them in the cover letter
only. Do not invent or embellish beyond what the profile shows.

If the LinkedIn fetch fails, proceed without it and note this at the end of the kit.

---

## Step 4 — Research the hiring manager

Search for the hiring manager or the person this role reports to. Use web_search with
queries like:

    "[Job Title] manager [Company Name] LinkedIn"
    "[Company Name] Head of [Department] LinkedIn"
    "[Company Name] VP [Department]"

Try at minimum two distinct queries before concluding not found.

If found: record their first name and LinkedIn profile URL.
If not found: state "Not found" and provide 2-3 specific actions the user can take (see
CONTACT section rules below).

---

## Step 5 — Identify the top 5 keywords

Before writing any content, scan the full job description and identify the 5 most important
keywords or phrases — the terms that appear repeatedly, are listed as requirements, or
define the core focus of the role. List them. These must appear naturally in both the
cover letter body and the resume summary.

---

## Step 6 — Generate content

Generate all three pieces of content before outputting anything. Count words and characters
before writing each one.

### Cover letter body

Write the core message only. No salutation. No closing. Body text only. The template
already contains the salutation and sign-off.

Constraints:
- Under 200 words. Count words before writing. Hard limit.
- Specific, direct, active voice throughout.
- No hedging. "I bring" beats "I believe I bring."
- Open with a specific statement about what the user brings to this role. No warm-up language.
- State one core value proposition as a direct declarative sentence.
- Follow with 2-3 proof points from the resume that match the job's stated needs.
  Use company names and outcomes. No generic claims.
- If Step 3 surfaced LinkedIn-only roles with a clear match, incorporate the most relevant
  one as an additional proof point. Only use what the profile actually shows.
- Include all 5 keywords from Step 5 naturally.
- Close with one forward-looking sentence about what the user brings to this specific role.
- Match the tone of the posting: casual startup vs. formal enterprise.

Writing rules (apply every one, then review before finalizing):
- Active voice throughout.
- No em dashes anywhere. Connect ideas with a period or a comma.
- No semicolons.
- No "In conclusion", "In closing", "Furthermore", "Moreover", "However", "Hence".
- No "Not just X, but also Y" constructions.
- No "I am writing to apply" or "I am excited to" openers.
- Banned words: can, may, just, that, very, really, literally, actually, certainly,
  probably, basically, could, maybe, delve, embark, enlightening, esteemed, shed light,
  craft, crafting, imagine, realm, game-changer, unlock, discover, skyrocket, abyss,
  not alone, in a world where, revolutionize, disruptive, utilize, utilizing, dive deep,
  tapestry, illuminate, unveil, pivotal, intricate, elucidate, hence, furthermore, realm,
  however, harness, exciting, groundbreaking, cutting-edge, remarkable, remains to be seen,
  glimpse into, navigating, landscape, stark, testament, in summary, in conclusion,
  moreover, boost, skyrocketing, opened up, powerful, inquiries, ever-evolving.
- No metaphors, clichés, or generalizations.
- No unnecessary adjectives or adverbs.
- No hashtags.

### Resume summary

A professional summary aligned to the role.

Constraints:
- Maximum 484 characters (count characters, not words). Hard limit.
- Third person or tight first-person. No "I am a" opener. Lead with the descriptor.
  Example: "Product designer with 10+ years across SaaS and fintech..."
- Mention 2-3 specific strengths from the resume that match the role's requirements.
- Include at least one concrete differentiator — a measurable achievement, a unique
  credential, or something specific that sets this person apart.
- Include all 5 keywords from Step 5 naturally.
- Do not pad to hit the limit. A tight 300-character summary beats a padded 484.
- Apply every writing rule from the cover letter section above.

Count characters before finalizing. If over 484, trim.

### LinkedIn note

A connection request note mentioning the application and why the user is a fit.

Structure:
- Start with: Hi, [FIRST NAME OF CONTACT]
- End with: Best, [YOUR_NAME]
- If no contact was found, address it to the hiring team and flag it for the user to fill in.

Constraints:
- Total character count (including greeting and sign-off) must be under 300 characters.
  Count characters before writing. Hard limit.
- One or two sentences between greeting and sign-off.
- Mention the specific role applied for.
- Include one specific reason the user is a fit, tied to a real credential or experience.
- No filler, no generic enthusiasm language.

Count characters. If over 300, trim.

---

## Step 7 — Output the in-chat kit

Output in plain text, exactly in this order. Use no markdown formatting, no asterisks,
no headers beyond the section labels themselves.

```
[Company Name] — [Job Title]

TOP 5 KEYWORDS:
1. [keyword]
2. [keyword]
3. [keyword]
4. [keyword]
5. [keyword]

CONTACT:
[contact output]

COVER LETTER:
[cover letter body]

RESUME SUMMARY:
[resume summary]

LINKEDIN NOTE:
[linkedin note]
```

CONTACT format:
- If found: Name: [Full Name] / LinkedIn: [URL]
- If not found: "Not found." followed by 2-3 specific search actions for the user.

---

## Step 8 — Create the Job Details PDF

```bash
pip3 install reportlab -q
python3 - <<'EOF'
from reportlab.lib.pagesizes import letter
from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer
from reportlab.lib.styles import getSampleStyleSheet
from reportlab.lib.units import inch
import os

output_path = os.path.expanduser("~/Downloads/Job Details - COMPANY - JOB TITLE.pdf")
doc = SimpleDocTemplate(output_path, pagesize=letter,
    rightMargin=inch, leftMargin=inch, topMargin=inch, bottomMargin=inch)
styles = getSampleStyleSheet()
story = []
story.append(Paragraph("COMPANY — JOB TITLE", styles['Title']))
story.append(Spacer(1, 12))
story.append(Paragraph("Salary: SALARY", styles['Normal']))
story.append(Spacer(1, 12))
story.append(Paragraph("JOB DESCRIPTION", styles['Normal']))
doc.build(story)
print(f"Saved: {output_path}")
EOF
```

Replace COMPANY, JOB TITLE, SALARY, and JOB DESCRIPTION with actual values.
Newlines in the description should be converted to `<br/>` tags for ReportLab.
Save to `~/Downloads/`.

---

## Step 9 — Clone both templates via Drive MCP

Clone both templates in parallel using the Drive MCP `copy_file` tool.

Cover letter:
- `fileId`: `YOUR_COVER_LETTER_TEMPLATE_ID`
- `name`: `Cover Letter - YOUR_NAME - COMPANY - JOB TITLE`
- `parentId`: `YOUR_FOLDER_ID`

Resume:
- `fileId`: `YOUR_RESUME_TEMPLATE_ID`
- `name`: `Resume - YOUR_NAME - COMPANY - JOB TITLE`
- `parentId`: `YOUR_FOLDER_ID`

Record both file IDs returned by the tool.

---

## Step 10 — Hand off to user for manual fill and PDF export

Present the following to the user in the chat:

Your cloned docs are ready. For each one:
1. Open the link
2. Find the placeholder text (`[[cover letter copy]]` or `[[resume summary copy]]`)
3. Select it and paste the content below in its place
4. File > Download > PDF Document (.pdf)

**Cover Letter**
Link: https://docs.google.com/document/d/COVER_LETTER_DOC_ID/edit

Paste this in place of `[[cover letter copy]]`:
[cover letter body — all paragraphs, separated by blank lines]

**Resume**
Link: https://docs.google.com/document/d/RESUME_DOC_ID/edit

Paste this in place of `[[resume summary copy]]`:
[resume summary text]

---

## Step 11 — Confirm

Confirm in the chat:

- Job Details PDF saved to `~/Downloads/Job Details - COMPANY - JOB TITLE.pdf`
- Cover letter and resume cloned and links provided above
- Cover letter word count and resume summary character count
- Any keyword gaps noticed between the JD and what was included

---

## File naming rules

- Replace characters invalid in file names (`/`, `:`, `?`, `*`, `"`, `<`, `>`, `|`) with a hyphen.
- Trim trailing spaces or hyphens from each segment.
- Keep exact casing from the job posting.

---

## Hard constraints summary

- Cover letter body: under 200 words. Count before writing.
- Resume summary: 484 characters or fewer. Count before writing.
- LinkedIn note: under 300 characters total. Count before writing.
- Never invent credentials, companies, dates, or metrics not in the resume or LinkedIn profile.
- In-chat output is plain text. No markdown formatting. No asterisks.
- Section labels appear exactly as: CONTACT:, COVER LETTER:, RESUME SUMMARY:, LINKEDIN NOTE:
- All 5 keywords must appear in both the cover letter and resume summary.
