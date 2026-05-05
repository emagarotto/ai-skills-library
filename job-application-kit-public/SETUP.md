# Job Application Kit — Setup Guide

This skill generates a tailored cover letter, resume summary, LinkedIn note, and contact
research for any job posting. Setup takes about 10 minutes and only happens once.

---

## What you need

- Claude Code (claude.ai/code) with the Google Drive connector enabled
- A Google account
- A resume hosted at a public URL (or paste your resume text into the skill)
- A LinkedIn profile

---

## Step 1 — Create your Google Doc templates

You need two Google Docs: one for your cover letter and one for your resume. These are
the master templates the skill clones for each application.

### Cover letter template

1. Create a new Google Doc.
2. Design your cover letter layout: your name, contact info, date, salutation, and sign-off.
3. Where the body paragraphs should go, type exactly: `[[cover letter copy]]`
   This is the placeholder the skill replaces with the generated content.
4. Style `[[cover letter copy]]` with the font, size, and color you want the body text
   to appear in. The skill preserves whatever formatting is on that placeholder.

### Resume template

1. Create a new Google Doc.
2. Design your resume layout: your name, contact info, experience, skills, etc.
3. Where your professional summary should go, type exactly: `[[resume summary copy]]`
4. Style `[[resume summary copy]]` with the font, size, and color you want.

---

## Step 2 — Get your template file IDs

Each Google Doc has a unique ID in its URL:

    https://docs.google.com/document/d/FILE_ID_IS_HERE/edit

Copy the file ID for each template.

---

## Step 3 — Create a Drive folder for output files

Create a Google Drive folder where cloned docs will be saved for each application.
Get its folder ID from the URL:

    https://drive.google.com/drive/folders/FOLDER_ID_IS_HERE

---

## Step 4 — Connect Google Drive to Claude

In Claude Code, open Settings > Connectors and enable Google Drive. Authorize with the
Google account that owns your templates and folder.

---

## Step 5 — Fill in the skill

Open `claude/SKILL.md` and replace every placeholder in the **About You** and
**Google Drive templates** sections:

| Placeholder | Replace with |
|---|---|
| `YOUR_NAME` | Your full name |
| `YOUR_TITLE` | Your professional headline |
| `YOUR_RESUME_URL` | Public URL to your resume PDF |
| `YOUR_LINKEDIN_URL` | Your LinkedIn profile URL |
| `YOUR_SUMMARY` | 3-5 bullets about your background |
| `YOUR_FOLDER_ID` | The folder ID from Step 3 |
| `YOUR_COVER_LETTER_TEMPLATE_ID` | Cover letter template file ID from Step 2 |
| `YOUR_RESUME_TEMPLATE_ID` | Resume template file ID from Step 2 |

---

## Step 6 — Test it

Give Claude a job posting URL and say "build my application kit for this role."

The skill will:
1. Fetch and parse the job description
2. Fetch your resume and LinkedIn profile
3. Research the hiring manager
4. Generate a cover letter, resume summary, and LinkedIn note in the chat
5. Create a Job Details PDF in `~/Downloads/`
6. Clone your templates in Google Drive with the company and job title in the filename
7. Give you the doc links and the content to paste, ready for PDF export

---

## Tips

- The more detail you put in `YOUR_SUMMARY`, the better the generated content.
  Include specific companies, outcomes, numbers, and differentiators.
- If your resume PDF isn't publicly accessible, paste your resume text directly into
  `YOUR_SUMMARY` instead.
- The skill researches the hiring manager automatically. If it finds one, the LinkedIn
  note is addressed to them by first name.
- The cover letter template should only contain the salutation ("Dear [Company] Hiring
  Team,"), the placeholder, and your sign-off. The skill writes the body.

---

## Credit

Built by Ezio Magarotto. Share freely.
LinkedIn: https://www.linkedin.com/in/eziomagarotto
