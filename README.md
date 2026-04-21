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
| ChatGPT | `company-research-report/chatgpt/instructions.md` | Markdown report in chat |
| Copilot | `company-research-report/copilot/instructions.md` | Markdown report in Copilot Chat |
| Gemini | `company-research-report/gemini/instructions.md` | Markdown report in chat or terminal |

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
| ChatGPT | `interview-prep/chatgpt/instructions.md` | Markdown report in chat |
| Copilot | `interview-prep/copilot/instructions.md` | Markdown report in Copilot Chat |
| Gemini | `interview-prep/gemini/instructions.md` | Markdown report in chat or terminal |

---

## How to Install

### Claude
1. Download the `SKILL.md` file from the skill's `claude/` folder
2. Zip it and rename the zip to `[skill-name].skill`
3. Go to Claude Settings and upload the `.skill` file under Skills
4. Trigger it using any phrase listed above

### ChatGPT
1. Open the `instructions.md` file from the skill's `chatgpt/` folder
2. Copy the contents of the Skill Instructions section
3. Paste into a Custom GPT (Configure tab) or a Project's Custom Instructions field
4. Enable Web Search under Capabilities

### GitHub Copilot
1. Open the skill's `copilot/` folder
2. For repo-level use: copy `copilot-instructions.md` to `.github/copilot-instructions.md` in your repo
3. For one-off use: copy the prompt template from `instructions.md` into Copilot Chat

### Gemini
1. Open the `instructions.md` file from the skill's `gemini/` folder
2. For a Gem: go to gemini.google.com, open Gems, click New Gem, paste the Gem Instructions section
3. For AI Studio: paste into the System Instructions field at aistudio.google.com
4. For CLI: `gemini --system-prompt "$(cat gemini/instructions.md)" "your prompt"`

---

## Repo Structure

```
ai-skills-library/
├── README.md
├── company-research-report/
│   ├── claude/
│   │   └── SKILL.md
│   ├── chatgpt/
│   │   └── instructions.md
│   ├── copilot/
│   │   ├── instructions.md
│   │   └── copilot-instructions.md
│   └── gemini/
│       └── instructions.md
└── interview-prep/
    ├── claude/
    │   └── SKILL.md
    ├── chatgpt/
    │   └── instructions.md
    ├── copilot/
    │   ├── instructions.md
    │   └── copilot-instructions.md
    └── gemini/
        └── instructions.md
```

---

## Adding New Skills

Create a new folder at the root level using the skill name. Inside it, create one subfolder per platform: `claude/`, `chatgpt/`, `copilot/`, `gemini/`. Add the appropriate file to each.

For Claude: `SKILL.md` with YAML frontmatter (name, description) and structured markdown instructions.
For all other platforms: `instructions.md` with a How to Use section and the full instructions ready to paste.

---

## Contributing

Pull requests are welcome. If you adapt a skill for a new platform or improve an existing one, open a PR with the updated files and a short description of what changed and why.

---

## License

MIT. Use and adapt these skills freely.
