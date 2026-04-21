# AI Skills Library

A collection of reusable AI skills for generating structured company research reports across four platforms: Claude, ChatGPT, GitHub Copilot, and Gemini.

Each skill produces the same core output regardless of platform: a thorough, sourced research report on any company you point it at. The format is adapted to fit how each platform works.

---

## Skills

### Company Research Report

Generates a full research report on any company. Covers founders and leadership backgrounds, product lines and revenue breakdown, major customers and case studies, strategic goals from earnings calls and filings, future growth plans, competitive positioning, funding history, and risks. Includes an executive summary and SWOT analysis.

Trigger phrases:
- "Research [company]"
- "I have a meeting with [company], what do I need to know?"
- "Generate a company report on [company]"
- "I'm interviewing at [company]"
- "Full breakdown on [company]"


---

### Interview Prep Report

Generates a focused, one-page interview prep report by combining the Company Research Report output with a job posting. Tells the candidate exactly where to focus during the interview, what the hiring manager cares about most, how to position their specific background for the role, which questions to ask, and what risks to prepare for.

Designed to run in sequence: generate the Company Research Report first, then feed that output alongside the job posting URL into this skill.

Trigger phrases:
- "Prep me for my interview at [company]"
- "I have an interview for [job title] at [company], help me prepare"
- "What should I focus on for this role? [job URL or description]"
- "How should I position myself for this job?"
- "What does the hiring manager care about most?"
- "Generate interview prep for [job URL]"
---

## Platform Guides

### Claude

**File:** `claude/company-research-report/SKILL.md`

Claude skills use a `.skill` file format. The skill reads the SKILL.md to understand what to do, runs web searches across 17 queries, and produces a formatted PDF with charts and a SWOT table using `reportlab` and `matplotlib`.

**How to install:**
1. Package the skill folder using the skill packaging script or zip the folder and rename it `.skill`
2. Go to Claude Settings and upload the `.skill` file under Skills
3. Trigger it by saying "Research [company]" or any phrase listed above

Output: PDF saved to your outputs folder, presented in chat.

---

### ChatGPT

**File:** `chatgpt/company-research-report/instructions.md`

ChatGPT skills work as Custom GPT instructions or Project instructions.

**How to install (Custom GPT):**
1. Go to [chatgpt.com](https://chatgpt.com) and open **Explore GPTs**
2. Click **Create**
3. Go to the **Configure** tab
4. Paste the contents of the `## Skill Instructions` section into the Instructions field
5. Enable **Web Search** under Capabilities
6. Save and publish (or keep private)

**How to install (Project):**
1. Open or create a Project in ChatGPT
2. Go to Project Settings
3. Paste the instructions into the Custom Instructions field

Output: Structured markdown report in chat.

---

### GitHub Copilot

**Files:**
- `copilot/company-research-report/instructions.md` – full setup guide
- `copilot/company-research-report/copilot-instructions.md` – drop-in file for your repo

**How to install (repo-level):**
1. Copy `copilot-instructions.md` to `.github/copilot-instructions.md` in your repository
2. Copilot Chat will follow these instructions automatically for all users in the repo

**How to use (one-off prompt):**
Copy the prompt template from `instructions.md` into Copilot Chat in VS Code, GitHub.com, or the CLI, filling in the company name.

Output: Structured markdown report in Copilot Chat.

---

### Gemini

**File:** `gemini/company-research-report/instructions.md`

Gemini skills work as Gems, AI Studio system prompts, or CLI system prompts.

**How to install (Gem):**
1. Go to [gemini.google.com](https://gemini.google.com)
2. Open the sidebar and select **Gems**
3. Click **New Gem**
4. Name it `Company Research Analyst`
5. Paste the `## Gem Instructions` section into the instructions field
6. Save

**How to install (AI Studio):**
1. Open [aistudio.google.com](https://aistudio.google.com)
2. Start a new prompt and paste the instructions into the System Instructions field
3. Save as a reusable prompt

**How to install (CLI):**
```bash
gemini --system-prompt "$(cat gemini/company-research-report/instructions.md)" "Research [company]"
```

Output: Structured markdown report in chat or terminal.

---

## Repo Structure

```
ai-skills-library/
├── README.md
├── claude/
│   ├── company-research-report/
│   │   └── SKILL.md
│   └── interview-prep/
│       └── SKILL.md
├── chatgpt/
│   ├── company-research-report/
│   │   └── instructions.md
│   └── interview-prep/
│       └── instructions.md
├── copilot/
│   ├── company-research-report/
│   │   ├── instructions.md
│   │   └── copilot-instructions.md
│   └── interview-prep/
│       ├── instructions.md
│       └── copilot-instructions.md
└── gemini/
    ├── company-research-report/
    │   └── instructions.md
    └── interview-prep/
        └── instructions.md
```

---

## Adding New Skills

To add a new skill, create a folder under each platform directory using the same skill name. Follow the conventions already established in each platform's existing skill folder.

For Claude skills, follow the SKILL.md format with YAML frontmatter (name, description) and a structured markdown body.

For all other platforms, include an `instructions.md` with a How to Use section and the full instructions ready to paste.

---

## Contributing

Pull requests are welcome. If you adapt a skill for a new platform or improve an existing one, open a PR with the updated files and a short description of what changed and why.

---

## License

MIT. Use and adapt these skills freely.
