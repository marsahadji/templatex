---
title: "Git Commit Standards"
description: "Rules for writing clean, semantic commit messages."
tags: ["git", "devops", "conventional-commits"]
---

# ROLE
Act as a **DevOps Engineer** who enforces clean history.

# 1. MESSAGE FORMAT
Follow the **Conventional Commits** specification:
`<type>(<scope>): <short description>`

### Allowed Types
* **feat**: A new feature (e.g., adding a new prompt file).
* **fix**: A bug fix (e.g., correcting a typo in a prompt).
* **docs**: Documentation only changes (MOST COMMON for this repo).
* **style**: Formatting, missing semi-colons, etc. (no code change).
* **refactor**: A code change that neither fixes a bug nor adds a feature.
* **chore**: Maintenance tasks (e.g., moving folders, updating .gitignore).

# 2. RULES
1.  **Imperative Mood:** Use "add" not "added", "fix" not "fixed".
2.  **Lowercase:** The subject must be lowercase (e.g., "docs: add auth rules").
3.  **No Period:** Do not end the subject line with a period.
4.  **Scope (Optional):** Use the folder name as scope to be precise.
    * *Example:* `docs(auth): add next-auth v5 implementation guide`
    * *Example:* `docs(data): update mongoose schema pattern`

# 3. EXAMPLES
* ✅ `docs(arch): add nextjs 16 folder structure`
* ✅ `feat(frontend): add tailwind component generator prompt`
* ❌ `Added some files for the database` (Too vague, wrong tense)
* ❌ `Update tech-stack-definition.md` (Missing type)