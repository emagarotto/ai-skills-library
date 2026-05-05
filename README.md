# AI Skills Library

A collection of reusable AI skills for Claude, ChatGPT, GitHub Copilot, and Gemini.

Each skill folder contains platform-specific versions of the same skill. Pick your platform, grab the file, and follow the install steps below.

---

## Skills

### company-research-report

Generates a full research report on any company. Covers founders and leadership backgrounds, product lines and revenue breakdown, major customers and case studies, strategic goals from earnings calls and filings, future growth plans, competitive positioning, funding history, and risks. Includes an executive summary and SWOT analysis.

Trigger phrases:
- "Research [company]"
- "I have a meeting with [company], what do I need to know?"
- "Generate a company report on [company]"
- "I'm interviewing at [company]"
- "Full breakdown on [company]"

| Platform | File | Output |
|----------|------|--------|
| Claude | `company-research-report/claude/SKILL.md` | PDF with charts and SWOT table |
| ChatGPT | `company-research-report/chatgpt/company-research-report.md` | Markdown report in chat |
| Copilot | `company-research-report/copilot/company-research-report.md` | Markdown report in Copilot Chat |
| Gemini | `company-research-report/gemini/company-research-report.md` | Markdown report in chat or terminal |

---

### interview-prep

Generates a focused, one-page interview prep report. Takes a job posting URL and company research as inputs. Tells the candidate exactly where to focus, what the hiring manager cares about most, how to position their background, which questions to ask, and what risks to prepare for.

Run company-research-report first, then feed that output into this skill alongside the job posting URL.

Trigger phrases:
- "Prep me for my interview at [company]"
- "I have an interview for [job title] at [company], help me prepare"
- "What should I focus on for this role? [job URL or description]"
- "How should I position myself for this job?"
- "What does the hiring manager care about most?"

| Platform | File | Output |
|----------|------|--------|
| Claude | `interview-prep/claude/SKILL.md` | One-page PDF |
| ChatGPT | `interview-prep/chatgpt/interview-prep.md` | Markdown report in chat |
| Copilot | `interview-prep/copilot/interview-prep.md` | Markdown report in Copilot Chat |
| Gemini | `interview-prep/gemini/interview-prep.md` | Markdown report in chat or terminal |

---

### job-application-kit-public

Generates a full tailored application kit from a job posting URL. Fetches the job description, your resume, and your LinkedIn profile. Researches the hiring manager. Identifies the top 5 keywords from the JD. Produces a cover letter body, resume summary, and LinkedIn connection note — all constrained to exact character and word limits.

On Claude: also creates a Job Details PDF and clones your Google Doc cover letter and resume templates in Drive with the company and role in the filename, ready for you to paste the generated content and export to PDF.

All personal info is replaced by placeholders. Drop in your own name, resume URL, LinkedIn URL, background bullets, and Google Drive template IDs to make it yours. Setup takes about 10 minutes.

Trigger phrases:
- "Process this job: [URL]"
- "Build my application kit for this role"
- "Generate my cover letter for [URL]"
- "Who should I contact at [company]?"
- "Write my cover letter and LinkedIn note for this job"

See `job-application-kit-public/SETUP.md` for the full setup guide.

| Platform | File | Output |
|----------|------|--------|
| Claude | `job-application-kit-public/claude/SKILL.md` | In-chat kit + Job Details PDF + cloned Drive templates |
| ChatGPT | `job-application-kit-public/chatgpt/job-application-kit-public.md` | In-chat kit (plain text) |
| Copilot | `job-application-kit-public/copilot/job-application-kit-public.md` | In-chat kit (plain text) |
| Gemini | `job-application-kit-public/gemini/job-application-kit-public.md` | In-chat kit (plain text) |

---

## How to Install

### Claude
1. Download the `SKILL.md` file from the skill's `claude/` folder
2. Zip it and rename the zip to `[skill-name].skill`
3. Go to Claude Settings and upload the `.skill` file under Skills
4. Trigger it using any phrase listed above

### ChatGPT
1. Open the skill's file from the `chatgpt/` folder
2. Copy the contents of the Skill Instructions section
3. Paste into a Custom GPT (Configure tab) or a Project's Custom Instructions field
4. Enable Web Search under Capabilities

### GitHub Copilot
1. Open the skill's file from the `copilot/` folder
2. For repo-level use: copy the contents to `.github/copilot-instructions.md` in your repo
3. For one-off use: paste the prompt directly into Copilot Chat

### Gemini
1. Open the skill's file from the `gemini/` folder
2. For a Gem: go to gemini.google.com, open Gems, click New Gem, paste the Gem Instructions section
3. For AI Studio: paste into the System Instructions field at aistudio.google.com
4. For CLI: `gemini --system-prompt "$(cat gemini/[skill-name].md)" "your prompt"`

---

## Repo Structure

```
ai-skills-repo/
├── README.md
├── company-research-report/
│   ├── claude/
│   │   └── SKILL.md
│   ├── chatgpt/
│   │   └── company-research-report.md
│   ├── copilot/
│   │   └── company-research-report.md
│   └── gemini/
│       └── company-research-report.md
├── interview-prep/
│   ├── claude/
│   │   └── SKILL.md
│   ├── chatgpt/
│   │   └── interview-prep.md
│   ├── copilot/
│   │   └── interview-prep.md
│   └── gemini/
│       └── interview-prep.md
├── job-application-kit/
│   ├── claude/
│   │   └── SKILL.md
│   ├── chatgpt/
│   │   └── job-application-kit.md
│   ├── copilot/
│   │   └── job-application-kit.md
│   └── gemini/
│       └── job-application-kit.md
└── job-application-kit-public/
    ├── SETUP.md
    ├── claude/
    │   └── SKILL.md
    ├── chatgpt/
    │   └── job-application-kit-public.md
    ├── copilot/
    │   └── job-application-kit-public.md
    └── gemini/
        └── job-application-kit-public.md
```

---

## Adding New Skills

Create a new folder at the root level using the skill name. Inside it, create one subfolder per platform: `claude/`, `chatgpt/`, `copilot/`, `gemini/`. Add the appropriate file to each.

For Claude: `SKILL.md` with YAML frontmatter (name, description) and structured markdown instructions.
For all other platforms: name the file after the skill (e.g., `company-research-report.md`) with a How to Use section and the full instructions ready to paste.

---

## Contributing

Pull requests are welcome. If you adapt a skill for a new platform or improve an existing one, open a PR with the updated files and a short description of what changed and why.

---

## License

MIT. Use and adapt these skills freely.
