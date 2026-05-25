---
name: job-application-kit
description: >
  Generate a tailored application kit from a job description URL and resume, then render
  it as an interactive HTML widget with copy buttons and Drive links.
  Use this skill whenever the user provides a job posting URL (or pasted JD) and asks
  for application materials, a kit, a cover letter, a resume summary, a LinkedIn note,
  or contact research for a role. Also trigger when the user says things like "process
  this job", "build my kit for this role", "generate my application materials", "who
  should I contact for this job", or "write my cover letter and LinkedIn note". Always
  trigger this skill when a job posting URL is present and the user wants any of these
  outputs: contact info, cover letter, resume summary, LinkedIn outreach, or PDFs.
---

# Job Application Kit

This skill produces a full application kit rendered as an interactive HTML widget. The
widget displays all sections with copy buttons and Drive links.

The kit has six parts:

1. Header: [Company Name] — [Job Title]
2. CONTACT (includes contact name, LinkedIn link, and pre-written connection note with copy button)
3. EMAIL OUTREACH (contact's work email as a Gmail compose link + longer outreach email with copy button)
4. COVER LETTER
5. RESUME SUMMARY
6. DOCUMENT TEMPLATES

---

## Setup required before first use

Before running this skill for the first time, answer the following questions so the skill
can be personalized to you. Paste your answers into the About You and Google Drive
templates sections below, replacing the placeholder values.

Questions to answer:

1. What is your full name?
2. What is your professional title or headline (e.g., "Senior Product Designer")?
3. What is the public URL to your resume PDF? (Must be publicly accessible — if you don't
   have one, paste your resume text directly into YOUR_SUMMARY below instead.)
4. What is your LinkedIn profile URL?
5. What is your email address? (Used for the Gmail compose link in email outreach.)
6. What is your website URL? (Used in the email sign-off.)
7. In 3-5 bullet points, describe your professional background. Be specific: include
   named companies, years of experience, measurable outcomes, certifications, and
   anything that makes you stand out. This is the source of truth for all generated content.
8. Do you use a PD (Product Design) and PM (Product Manager) track distinction for
   applications, or do you apply to one type of role only? If two tracks: provide
   separate resume and cover letter Google Doc template file IDs for each. If one track:
   provide one set of template IDs.
9. What is the Google Drive folder ID where cloned docs should be saved?
10. What are the Google Doc template file IDs for your cover letter and resume templates?
    (Each template must contain the placeholder strings `[[cover letter copy]]` and
    `[[resume summary copy]]` respectively. See SETUP.md for instructions.)

---

## About You

```
YOUR_NAME: [your full name]
YOUR_TITLE: [your professional title / headline]
YOUR_EMAIL: [your email address]
YOUR_WEBSITE: [your website URL]
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
YOUR_EMAIL: jordan@example.com
YOUR_WEBSITE: https://jordansmith.com/
YOUR_RESUME_URL: https://jordansmith.com/resume.pdf
YOUR_LINKEDIN_URL: https://www.linkedin.com/in/jordansmith
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

Single-track setup (one role type):
  YOUR_COVER_LETTER_TEMPLATE_ID: [file ID of your cover letter Google Doc template]
  YOUR_RESUME_TEMPLATE_ID: [file ID of your resume Google Doc template]

Two-track setup (PD and PM):
  PD_COVER_LETTER_TEMPLATE_ID: [file ID of PD cover letter template]
  PD_RESUME_TEMPLATE_ID: [file ID of PD resume template]
  PM_COVER_LETTER_TEMPLATE_ID: [file ID of PM cover letter template]
  PM_RESUME_TEMPLATE_ID: [file ID of PM resume template]
```

Templates must contain these exact placeholder strings:
- Cover letter template: `[[cover letter copy]]` where the body paragraphs go
- Resume template: `[[resume summary copy]]` where the professional summary goes

See SETUP.md for instructions on creating your Google Doc templates and finding file IDs.

---

## Step 0 — Determine role track

If you have configured two-track templates (PD and PM above), ask the user one question
before fetching anything:

    Is this role Product Design (PD) or Product Manager (PM) focused?

Wait for the answer. Store the track as either "PD" or "PM". Use it in Step 5 to select
the correct templates and in Step 6 to focus the cover letter and resume summary.

If only one track is configured, skip this step and proceed directly to Step 1.

---

## Step 1 — Fetch the job posting

Use `web_fetch` on the JD URL. Extract:

- Company name (the hiring org, not the job board)
- Exact job title
- Full job description (responsibilities, requirements, qualifications)
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

If found: record their first name and full LinkedIn profile URL. Store as CONTACT_LINKEDIN_URL.

If not found: set CONTACT_LINKEDIN_URL to null.
Then construct the LinkedIn company people page URL. Search for the company's LinkedIn
slug using a query like "[Company Name] LinkedIn company" and extract the slug from the
result (e.g., "linkedin.com/company/acme-corp" → slug is "acme-corp"). Build:

    https://www.linkedin.com/company/[slug]/people/

Store as COMPANY_PEOPLE_URL. If the slug cannot be determined, set COMPANY_PEOPLE_URL
to "https://www.linkedin.com/search/results/people/?keywords=[Company+Name]" as a
fallback, with the company name URL-encoded.

---

## Step 4b — Find the contact's work email

After identifying the contact in Step 4, attempt to find their work email address.
Store the result as CONTACT_EMAIL (string or null).

Try these approaches in order, stopping as soon as an email is found:

1. Web search with Hunter.io pattern:
   Search: "[First Name] [Last Name] [Company Name] email site:hunter.io"
   Or: "[First Name] [Last Name] [Company Name] email contact"

2. Common pattern inference (use only if company domain is known and pattern is
   strongly suggested by public sources):
   Try firstname@company.com, first.last@company.com, firstlast@company.com.
   Only include if you have seen evidence of the pattern from a public source.
   Never fabricate or guess without corroborating evidence.

3. LinkedIn About section or company website contact page:
   Search: "[Company Name] contact email site:[company domain]"

If a confirmed email is found:
- Store as CONTACT_EMAIL.
- Build a Gmail compose URL:
    https://mail.google.com/mail/?view=cm&fs=1&to=[CONTACT_EMAIL]&from=[YOUR_EMAIL]&su=[SUBJECT]&body=[BODY]
  Where [SUBJECT] and [BODY] are URL-encoded. The subject should be:
    "Re: [Job Title] at [Company Name] — [YOUR_NAME]"
  The body field should be left empty (the outreach note will be copied separately).

If no confirmed email is found:
- Set CONTACT_EMAIL to null.
- In the widget, show a subdued note: "Email not found — try Hunter.io or RocketReach
  for [Company Name] domain."

---

## Step 5 — Clone Drive templates

Use Google Drive MCP tools to clone the two matching template files into the Drive folder.
Do this before assembling the kit so the links are ready.

Step 5a — Select template IDs.

Use the template file IDs configured in the Google Drive templates section above.
If two-track setup: use the IDs matching the track from Step 0.
If single-track setup: use YOUR_COVER_LETTER_TEMPLATE_ID and YOUR_RESUME_TEMPLATE_ID.

Do NOT search for template files — use the hardcoded IDs only.

Step 5b — Copy the files.

Use `Google Drive:copy_file` on each file ID. Set the new name to:
    Resume:       [YOUR_NAME] - Resume - [Company Name] - [Job Title]
    Cover Letter: [YOUR_NAME] - Cover Letter - [Company Name] - [Job Title]

If two-track setup, prefix the track:
    [Track] - Resume - [YOUR_NAME] - [Company Name] - [Job Title]
    [Track] - Cover Letter - [YOUR_NAME] - [Company Name] - [Job Title]

Place the copies in: YOUR_FOLDER_ID

Step 5c — Get the links.

Use `Google Drive:get_file_metadata` on each new file. Extract the webViewLink.
Store as RESUME_DRIVE_LINK and COVER_DRIVE_LINK.

If any operation fails, proceed without links and note the failure in the widget.

Step 5d — Open the cloned files in Chrome.

After the links are confirmed, use `mcp__Claude_in_Chrome__navigate` to open each
cloned file in the browser automatically — once for RESUME_DRIVE_LINK and once for
COVER_DRIVE_LINK. This lets the user start editing immediately.

If the Claude in Chrome tool is unavailable or the navigate call fails, skip silently
and proceed to Step 6.

---

## Step 6 — Assemble and render the kit

Render the full kit as an HTML widget using the `show_widget` tool. Use the
loading_messages parameter with 2-3 brief messages.

The widget displays sections in this order: HEADER, CONTACT, EMAIL OUTREACH,
COVER LETTER, RESUME SUMMARY, DOCUMENT TEMPLATES.

### Visual design specification

Typography and color:
- Font stack: -apple-system, BlinkMacSystemFont, 'Inter', 'Segoe UI', sans-serif
- Background: #FAFAFA for the page, #FFFFFF for cards
- Primary text: #111827
- Secondary text: #6B7280
- Accent: #2563EB (blue)
- Border: #E5E7EB (subtle)
- Success green for copied state: #16A34A

Layout:
- Full-width card layout. Each section is a white card with border-radius: 12px,
  a 1px border in #E5E7EB, and padding: 20px 24px.
- Cards have a subtle box-shadow: 0 1px 3px rgba(0,0,0,0.06).
- 16px vertical gap between cards.
- No outer horizontal padding constraints; fill the available width.

Header card:
- Background: linear-gradient(135deg, #1E3A5F 0%, #2563EB 100%)
- White text throughout.
- Company name in 22px bold. Job title below in 15px, opacity 0.85.
- If two-track setup: a small pill badge on the right showing the track (PD or PM)
  in white with a semi-transparent background (rgba(255,255,255,0.2)), 11px font, uppercase.

Section cards (CONTACT, EMAIL OUTREACH, COVER LETTER, RESUME SUMMARY, DOCUMENT TEMPLATES):
- Each card has a section label row at the top: label text in 10px, bold,
  letter-spacing 0.08em, uppercase, color #6B7280.
- A 1px horizontal rule in #F3F4F6 separates the label row from the body.
- Body text at 14px, line-height 1.7, color #111827.

Action controls (Copy button and Open in Drive link):
- Position them in the top-right of the label row, flex-end aligned.
- Copy button: 11px font, font-weight 600, padding 4px 12px, border-radius 6px,
  background #F3F4F6, border: 1px solid #E5E7EB, color #374151, cursor pointer.
  On hover: background #E5E7EB. On click: copy text, change label to "Copied ✓",
  change background to #DCFCE7, color #16A34A, border-color #BBF7D0. Restore after 2s.
- Open in Drive link: 11px font, font-weight 600, color #2563EB, no underline,
  with a small "↗" suffix. On hover: underline.

### Section-by-section content

---

#### HEADER card

Gradient card (see above). Display:
- Company name (large, bold, white)
- Job title (smaller, white, slightly transparent)
- Track badge right-aligned if two-track setup is configured

---

#### EMAIL OUTREACH card

Top row: label "Email Outreach" on the left.

Email address block:
- If CONTACT_EMAIL is found: show it as a clickable button styled in accent blue,
  with a "✉ Open in Gmail ↗" label. The href is the Gmail compose URL from Step 4b.
  Opens in a new tab.
- If CONTACT_EMAIL is null: show in secondary text:
  "Email not found — try Hunter.io or RocketReach for [Company Name] domain."

Divider (1px #F3F4F6) below the email block.

Outreach note block:
- Label: "Email Note" in 10px uppercase secondary text. Copy button on the right.
- Note body: rendered as plain readable text (white-space: pre-wrap), 14px, line-height 1.7.

---

#### CONTACT card

If CONTACT_LINKEDIN_URL is null, show a small "Not found" line in secondary text above
the note, followed by a clickable link using COMPANY_PEOPLE_URL labeled
"Browse [Company Name] employees on LinkedIn ↗", and a small bulleted list of three
manual search actions. Then show the note block below a divider.

Note block:
- Label row: "LinkedIn Note" in 10px uppercase secondary text on the left.
  On the right: Copy button + LinkedIn link (CONTACT_LINKEDIN_URL if found,
  COMPANY_PEOPLE_URL if not), labeled "LinkedIn ↗", opens in new tab.
- Note body rendered as plain readable text (white-space: pre-wrap).

---

#### COVER LETTER card

Controls row: Copy button + Open in Drive link (COVER_DRIVE_LINK).
If COVER_DRIVE_LINK is unavailable, show: "Drive link unavailable" in secondary text.

Body: cover letter text, pre-wrap, 14px, line-height 1.7.

---

#### RESUME SUMMARY card

Controls row: Copy button + Open in Drive link (RESUME_DRIVE_LINK).
Same fallback behavior as cover letter.

Body: summary text, pre-wrap, 14px, line-height 1.7.
Below the summary, add a small character count in secondary text: "[N] / 484 characters"

---

#### DOCUMENT TEMPLATES card

Folder link at top: "Open Drive folder ↗" in accent blue, opens in new tab.

Below, two rows — one per cloned file. Each row has:
- The full file name in 13px font-weight 500.
- A small "Open ↗" link to the right in accent blue, linking to the Drive file.

If Step 5 failed, note this in secondary text and instruct the user to clone manually.

---

Do not use any external CSS frameworks or JS libraries. All styles and scripts inline.

---

### EMAIL OUTREACH:

A warm, direct outreach email — longer and more substantive than the LinkedIn note.
This is meant to be sent from YOUR_EMAIL to the contact's work email.

Length: approximately double the LinkedIn note. Target 500–600 characters of body text
(not counting the greeting or sign-off). Hard ceiling: 700 characters of body text.

Structure:
- Open with: Hi [First Name],
- Body: 3–4 sentences.
  1. State the role applied for and the specific reason this company is compelling
     (one sentence, tied to a real product or company characteristic, not generic interest).
  2. Name one or two specific companies or projects from YOUR_SUMMARY where the user
     solved a similar problem to what this role requires. Be concrete: name the company,
     the problem, and what was done. Draw only from the resume and LinkedIn profile.
  3. Reference one specific credential, shipped product, or measurable outcome from
     YOUR_SUMMARY that directly maps to the role's needs. One sentence.
  4. A direct, low-pressure close: invite a conversation. No asking for a favor or
     expressing hope. Example: "Happy to share more if useful."
- Sign-off:
    Cheers,
    [YOUR_NAME]
    [YOUR_EMAIL]
    [YOUR_WEBSITE]

Writing rules: same as cover letter. Active voice. No filler. No em dashes. No semicolons.
No banned words. No "I'm excited to" or "I hope to hear from you."

---

### CONTACT:

Compose the LinkedIn connection note per these rules:

- Start with: Hi, [FIRST NAME OF CONTACT]
- End with:
    Best,
    [YOUR_NAME]
- If no contact was found, use: Hi, [hiring team] — and flag for the user to fill in.
- Under 300 characters total including greeting and sign-off. Count before writing.
- One or two sentences between greeting and sign-off.
- Mention the specific role applied for.
- Include one specific reason the user is a fit, tied to a real credential or experience.
- No filler, no generic enthusiasm language.

---

### COVER LETTER:

Write the core message only. No beginning salutation. No closing salutation. No "Dear",
no "Sincerely", no "Best regards". Body text only.

If two-track setup is configured, tailor the letter's framing to the track selected in
Step 0 (lead with design strengths for PD, lead with product and builder strengths for PM).
Otherwise, use YOUR_SUMMARY as the source and tailor the letter to the JD.

Shared constraints:
- Under 300 words. Count words before writing. Hard limit.
- Specific, direct, active voice throughout.
- No hedging. "I bring" beats "I believe I bring."
- Open with a specific statement about what the user brings to this role. No warm-up language.
- State one core value proposition as a direct declarative sentence.
- Follow with 2-3 proof points from the resume that match the job's stated needs.
  Use company names and outcomes. No generic claims.
- If Step 3 surfaced LinkedIn-only roles with a clear match to the JD (by industry,
  domain, or function), incorporate the most relevant one as an additional proof point.
  Introduce it naturally. Do not force it if the fit is weak. Use only what the
  LinkedIn profile actually shows.
- Include the top 5 keywords from the JD naturally.
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
  however, harness, exciting, groundbrearding, cutting-edge, remarkable, remains to be seen,
  glimpse into, navigating, landscape, stark, testament, in summary, in conclusion,
  moreover, boost, skyrocketing, opened up, powerful, inquiries, ever-evolving.
- No metaphors, clichés, or generalizations.
- No unnecessary adjectives or adverbs.
- No hashtags.

---

### RESUME SUMMARY:

A professional summary aligned to the role.

Constraints:
- Maximum 484 characters (count characters, not words). Hard limit.
- No "I am a" opener. Lead with the descriptor.
  Example: "Product designer with 10+ years across SaaS and fintech..."
- Mention 2-3 specific strengths from the resume that match the role's requirements.
- Include at least one concrete differentiator — a measurable achievement, a unique
  credential, or something specific that sets the user apart.
- Include the top 5 keywords from the JD naturally.
- Do not pad to hit the limit. A tight 300-character summary beats a padded 484.
- Apply every writing rule from the COVER LETTER section above.

Count characters before finalizing. If over 484, trim.

---

### DOCUMENT TEMPLATES:

Show the Drive folder link and confirm the files cloned in Step 5.

If Step 5 failed, note this and instruct the user to clone the templates manually.

---

## Step 7 — Paste generated content into the cloned Drive files

After the widget is rendered, paste the cover letter and resume summary into their
respective cloned Google Docs. The documents are already open in Chrome from Step 5d.

The placeholder strings in the templates are:
    Cover Letter doc: [[cover letter copy]]
    Resume doc:       [[resume summary copy]]

For each document, use Find & Replace to swap the placeholder for the generated text:

1. Switch to the correct Chrome tab using `mcp__Claude_in_Chrome__switch_browser` or
   identify the tab ID from the context obtained in Step 5d.

2. Open Find & Replace in Google Docs:
   Use `mcp__Claude_in_Chrome__shortcuts_execute` with shortcut "cmd+h" (Mac).

3. Fill in the Find & Replace dialog:
   Use `mcp__Claude_in_Chrome__form_input` to enter the placeholder in the Find field
   and the generated text in the Replace field. Click Replace All.

4. Confirm the replacement with `mcp__Claude_in_Chrome__get_page_text`.

Repeat for the second document.

If any step fails, skip silently and add to the chat:
  "Auto-paste succeeded." or "Auto-paste failed — use the Copy buttons in the kit."

---

## Step 8 — Open LinkedIn and pre-fill the connection note

After the widget is rendered, navigate to the contact's LinkedIn profile and pre-fill
the connection request note so the user only needs to click Send.

Use CONTACT_LINKEDIN_URL from Step 4. If it is null, skip this step silently and note
it in the chat: "LinkedIn contact not found — connect manually via the Browse link in
the kit."

Step 8a — Navigate to the contact's LinkedIn profile.

Use `mcp__Claude_in_Chrome__navigate` to open CONTACT_LINKEDIN_URL in a new Chrome tab.
Create the tab first with `mcp__Claude_in_Chrome__tabs_create_mcp`, then navigate to it.

Step 8b — Click the Connect button.

    document.querySelector('[aria-label*="Connect"]')?.click()

If the button is not immediately visible (may be inside a "More" dropdown), click the
"More" button first:

    document.querySelector('[aria-label*="More actions"]')?.click()

Then retry the Connect button click.

Step 8c — Click "Add a note" in the invitation dialog.

    document.querySelector('[aria-label*="Add a note"]')?.click()

Step 8d — Fill in the note text.

    const ta = document.querySelector('textarea[name="message"]') ||
               document.querySelector('.send-invite__custom-message') ||
               document.querySelector('textarea');
    if (ta) {
      const nativeInputValueSetter = Object.getOwnPropertyDescriptor(
        window.HTMLTextAreaElement.prototype, 'value').set;
      nativeInputValueSetter.call(ta, NOTE_TEXT_HERE);
      ta.dispatchEvent(new Event('input', { bubbles: true }));
    }

Replace NOTE_TEXT_HERE with the full LinkedIn note text from Step 6 (CONTACT section),
as a JS string literal with escaped newlines.

Step 8e — Stop. Do NOT click Send.

Leave the dialog open with the note pre-filled. Tell the user in the chat:
  "LinkedIn note pre-filled for [Contact First Name] at [Company]. Review and click
   Send when ready."

If any step in Step 8 fails, skip silently and add to the chat:
  "LinkedIn auto-fill failed — use the Copy button in the kit and connect manually."

---

## Hard constraints summary

- Cover letter: under 300 words. Count before writing.
- Resume summary: 484 characters or fewer. Count before writing.
- LinkedIn note: under 300 characters total. Count before writing.
- Never invent credentials, companies, dates, or metrics not in the resume or LinkedIn profile.
- Output is an HTML widget via show_widget. No raw plain text output. No markdown. No asterisks.
- Sections in order: HEADER, CONTACT, EMAIL OUTREACH, COVER LETTER, RESUME SUMMARY, DOCUMENT TEMPLATES.
- CONTACT card includes both the contact block and the LinkedIn note block with a copy button.
- COVER LETTER and RESUME SUMMARY each have a Copy button and an Open in Drive link.
- RESUME SUMMARY card shows a character count below the text.
- Widget uses the visual design spec from Step 6: gradient header, card layout, defined color system.
- Top 5 JD keywords must appear in both the cover letter and resume summary.
