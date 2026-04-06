---
name: gh-aw
description: 'GitHub Agentic Workflows (gh-aw) skill. Use when: creating a new agentic workflow, updating an existing workflow, debugging workflow failures, analyzing gh-aw logs, upgrading workflows to a new gh-aw version, creating a shared/reusable workflow component, triaging issues with a workflow, labeling pull requests automatically, designing automation with gh aw, compiling workflows, fixing deprecated gh-aw fields.'
argument-hint: 'Describe what you want to do: create, update, debug, upgrade, or create a shared workflow'
---

# GitHub Agentic Workflows (gh-aw)

This skill guides the creation, update, debugging, and management of **GitHub Agentic Workflows (gh-aw)** in this repository.

## When to Use

- Create a new agentic workflow (`gh aw new`)
- Modify or improve an existing workflow
- Debug a failing workflow or analyze its logs
- Upgrade workflows to a new gh-aw version
- Create a shared/reusable workflow component

---

## Procedure

### Step 1: Read the official instructions

Fetch and read the main instructions file from:

```
https://raw.githubusercontent.com/github/gh-aw/main/create.md
```

This file contains the complete guide with sub-prompts to load depending on the task.

> **ROOT** = `https://raw.githubusercontent.com/github/gh-aw/main`

### Step 2: Identify the task and load the appropriate sub-prompt

| Task | Sub-prompt file |
|------|----------------|
| Create a new workflow | `ROOT/.github/aw/create-agentic-workflow.md` |
| Update an existing workflow | `ROOT/.github/aw/update-agentic-workflow.md` |
| Debug / analyze logs | `ROOT/.github/aw/debug-agentic-workflow.md` |
| Upgrade to a new version | `ROOT/.github/aw/upgrade-agentic-workflows.md` |
| Create a shared component | `ROOT/.github/aw/create-shared-agentic-workflow.md` |

Fetch the corresponding sub-prompt file and **read all its instructions before taking any action**.

### Step 3: Check / install gh-aw

```bash
gh aw version
```

If not installed:
```bash
curl -sL https://raw.githubusercontent.com/github/gh-aw/main/install-gh-aw.sh | bash
```

If already installed, upgrade:
```bash
gh extension upgrade aw
```

### Step 4: Execute according to the loaded sub-prompt

Follow the sub-prompt instructions exactly. If anything is unclear, ask the user for clarification.

### Step 5: Review created/modified files

```bash
git status
```

Expected files for a workflow:
- `.github/workflows/<workflow-name>.md`
- `.github/workflows/<workflow-name>.lock.yml`
- `.gitattributes` (must contain `.github/workflows/*.lock.yml linguist-generated=true merge=ours`)

### Step 6: Commit and push

```bash
git add .gitattributes .github/workflows/<workflow-name>.md .github/workflows/<workflow-name>.lock.yml
git commit -m "Add/update agentic workflow: <workflow-name>"
git push
```

If the default branch is protected, create a pull request instead.

---

## Quick Reference

```bash
# Create a new workflow
gh aw new <workflow-name>

# Compile workflows
gh aw compile [workflow-name]

# View workflow logs
gh aw logs [workflow-name]

# Audit a run
gh aw audit <run-id>

# Fix deprecations
gh aw fix --write
gh aw compile --validate
```

---

## Repository Context

This repository uses `gh-aw` to automate workflows for the fictional **Marabou** project (cult of the Sacred Pizza). Existing workflows are in `.github/workflows/`. The gh-aw configuration is in `.github/aw/`.
