# GitHub Agentic Workflow — Copilot DevDays 2026

> **GitHub Copilot DevDays Namur — 7 avril 2026**
> Bureaux d'Eocene, Namur, Belgique
> 🎟️ [Inscription à l'événement](https://luma.com/ebdbymfu)

---

## Session

**GitHub Agentic Workflow**

Présentée par **Adrien Clerbois**
*Microsoft MVP Belgique — Microsoft Foundry & Developer Technologies (DevOps : Azure DevOps & GitHub)*

Cette session explore **[GitHub Agentic Workflows](https://github.github.com/gh-aw/)** — un projet GitHub Next / Microsoft Research permettant d'automatiser un repository via des fichiers Markdown simples qui pilotent des agents IA (Copilot, Claude, Codex…) dans GitHub Actions, avec des garde-fous de sécurité intégrés.

> ⚠️ **GitHub Agentic Workflows est actuellement en développement précoce (*early development*)** et peut changer significativement. Son utilisation nécessite une supervision humaine attentive.

---

## Structure du repository

```
.
├── slides/
│   └── GitHub Copilot Dev Days - Agentic Workflows.pptx
└── examples/             # à venir — exemples live de la session
```

---

## Qu'est-ce que GitHub Agentic Workflows ?

**GitHub Agentic Workflows** est un projet [GitHub Next](https://githubnext.com/) / [Microsoft Research](https://www.microsoft.com/en-us/research/) qui permet d'automatiser un repository via de simples fichiers Markdown. Ces fichiers décrivent en langage naturel ce que l'agent doit faire ; le framework se charge de les exécuter dans GitHub Actions en pilotant un agent IA (Copilot, Claude, Codex…) avec des garde-fous de sécurité intégrés.

### Fonctionnement

| Couche | Rôle |
|---|---|
| **Fichier `.aw/*.md`** | Décrit la tâche en langage naturel (déclencheur, permissions, instructions) |
| **Agent IA** | Lit le contexte du repository et produit un *artifact* structuré — il ne peut rien écrire directement |
| **Job d'exécution** | Lit l'artifact et applique uniquement les actions explicitement autorisées |
| **Threat detection** | Scan IA anti-prompt-injection avant toute écriture |
| **Firewall réseau** | Trafic sortant filtré via liste blanche — aucune exfiltration possible |

### Exemple de workflow (rapport quotidien)

```markdown
---
on:
  schedule: daily
permissions:
  contents: read
  issues: read
  pull-requests: read
safe-outputs:
  create-issue:
    title-prefix: "[team-status] "
    labels: [report, daily-status]
    close-older-issues: true
---

## Daily Issues Report

Crée un rapport de statut quotidien sous forme d'issue GitHub.

### Ce qu'il doit contenir
- Activité récente (issues, PRs, discussions, releases)
- Suivi des objectifs et points saillants
- Recommandations et prochaines étapes
```

---

## Démarrage rapide

```bash
# Installer le CLI gh-aw
gh extension install github/gh-aw

# Initialiser un workflow dans un repository existant
gh aw init

# Déclencher manuellement un workflow
gh aw run <nom-du-workflow>
```

> Consulte le [Quick Start officiel](https://github.github.com/gh-aw/setup/quick-start/) pour l'installation complète.

---

## Créer un workflow via prompt

La façon la plus rapide de créer un agentic workflow est de soumettre un prompt à un agent IA — que ce soit depuis l'interface web GitHub, VS Code Agent Mode, ou n'importe quel agent de code.

### Depuis l'interface web GitHub

Si tu as accès à GitHub Copilot, tu peux créer et modifier des Agentic Workflows directement depuis github.com. Cette méthode est moins interactive qu'un agent de code, mais elle permet de passer d'une idée à un workflow fonctionnel en quelques minutes.

Colle l'un des prompts suivants dans Copilot Chat de ton repository (exemples : Issue Triage, Activity Report, Documentation Updater, **AGENTS.md Maintainer**) :

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md

The purpose of the workflow is to run weekly and maintain the AGENTS.md file: review merged pull requests and updated source files since the last run, then open a pull request that keeps AGENTS.md accurate and current.
```

> ⚠️ Lors du premier run dans un nouveau repository, le workflow échouera probablement car les secrets ne sont pas encore configurés. L'agent devrait détecter les tokens manquants et créer une issue avec les instructions de configuration.

### Depuis VS Code / Claude / Codex / Copilot

Lance ton agent de code dans le contexte du repository et soumets le prompt suivant en adaptant la dernière ligne à ton besoin :

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md
The purpose of the workflow is <décris ici l'objectif du workflow>.
```

L'agent créera un fichier `.github/workflows/<nom>.md` et son fichier compilé `.lock.yml` associé, et proposera souvent une pull request.

---

### Exemple : AGENTS.md Maintainer

Ce workflow maintient automatiquement le fichier `AGENTS.md` du repository — le fichier de référence qui décrit les conventions et le contexte du projet aux agents IA qui travaillent dessus.

**Prompt à utiliser :**

```
Create a workflow for GitHub Agentic Workflows using https://raw.githubusercontent.com/github/gh-aw/main/create.md
The purpose of the workflow is to maintain the AGENTS.md file: review the repository
structure, conventions, and recent changes, then keep the AGENTS.md file up to date
so that coding agents always have accurate context about the project.
```

**Ce que le workflow fait concrètement :**

- Analyse la structure du repository, les fichiers de configuration et les conventions de code
- Compare avec le contenu actuel de `AGENTS.md`
- Propose une pull request avec les mises à jour nécessaires

**Déclencheurs typiques :**

```markdown
---
on:
  schedule: weekly
  push:
    branches: [main]
    paths:
      - '**.md'
      - 'package.json'
      - '*.config.*'
permissions:
  contents: read
safe-outputs:
  create-pull-request:
    title-prefix: "[agents] "
    labels: [documentation, agents]
---
```

> 📖 Référence complète : [Creating Workflows](https://github.github.com/gh-aw/setup/creating-workflows/)

---

## Ressources

- [GitHub Agentic Workflows — site officiel](https://github.github.com/gh-aw/)
- [GitHub Agentic Workflows — repository](https://github.com/github/gh-aw)
- [Article de blog GitHub](https://github.blog/ai-and-ml/automate-repository-tasks-with-github-agentic-workflows/)
- [Documentation GitHub Copilot](https://docs.github.com/fr/copilot)
- [Personnalisation Copilot — instructions & prompt files](https://docs.github.com/fr/copilot/customizing-copilot)
- [Model Context Protocol](https://modelcontextprotocol.io)

---

## À propos du speaker

**Adrien Clerbois** est Microsoft MVP Belge en Developer Technologies (DevOps — Azure DevOps & GitHub) et Microsoft Foundry.
Passionné par l'expérience développeur, l'automatisation et l'ingénierie assistée par l'IA.

- GitHub : [@AClerbois](https://github.com/AClerbois)

---

*Licence MIT — n'hésite pas à réutiliser et adapter les exemples.*
