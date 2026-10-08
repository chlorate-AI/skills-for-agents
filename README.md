Zurawski Lab Agent Skills

In this directory, we will host the Markdown skills our agents can utilize to critically assess the impact and repeatability of manuscripts, critically review grant submissions, and interact with our specific tech stack.

## 🗂️ Skills Directory

| Skill Name | Core Persona | Intent / Trigger Phrase | Location |
| :--- | :--- | :--- | :--- |
| **Article Impact** | Determines if paper is cited/repeatable | "impact search", "journal article reliability" | `/.github/skills/article-impact` |
| **Test Gen** | QA Automation Senior | "write test cases", "run pytest" | `/.github/skills/test-gen` |
| **Style Fixer** | Automated Linter | "format code", "fix linting errors" | `/.github/skills/style-fixer` |

## 🚀 How to Use

### Global Project Rules
This repository utilizes the `AGENTS.md` open standard at the root to provide persistent, project-wide guardrails to your LLM assistant. 

* **Cursor:** Reads individual markdown files placed inside `.cursor/rules/`.
* **GitHub Copilot:** Reads the root `AGENTS.md` file anywhere in the directory tree.
* **Claude Code:** Automatically reads a root `CLAUDE.md` file. (Tip: Create a symbolic link from `CLAUDE.md` to `AGENTS.md`).

### Individual Skill Registration
For specialized tasks, ensure your editor environment points to the target skill directories:
```bash
# Example for GitHub CLI if using GitHub Copilot Extensions
gh skill install ./.github/skills/api-builder
```

## 🔒 Security & Guardrails
All workflow scripts are bounded by explicit execution rules. Ensure your local `AGENTS.md` contains the mandatory execution boundaries:
* **Always Do:** Run localized linters or package managers (e.g., `uv`, `pytest`).
* **Ask First:** Destructive schema alterations or external API deployment.
* **Never Do:** Hardcode environment variables, secrets, or bypass verification gates.
