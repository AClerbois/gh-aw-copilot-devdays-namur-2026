---
description: |
  Ce workflow crée des rapports quotidiens sur l'état du dépôt. Il rassemble l'activité récente
  (issues, PRs, discussions, releases, changements de code) et génère des issues GitHub
  engageantes avec des insights de productivité, des temps forts de la communauté
  et des recommandations pour le projet.

on:
  schedule: daily
  workflow_dispatch:

permissions:
  contents: read
  issues: read
  pull-requests: read

network: defaults

tools:
  github:
    # Dans un dépôt public, `lockdown: false` permet de lire les issues,
    # PRs et commentaires venant de tiers.
    # Dans un dépôt privé, cela n'a pas d'effet particulier.
    lockdown: false
    min-integrity: none # Ce workflow est autorisé à examiner et commenter toutes les issues

safe-outputs:
  mentions: false
  allowed-github-references: []
  create-issue:
    title-prefix: "[rapport-quotidien] "
    labels: [rapport, statut-quotidien]
    close-older-issues: true
source: githubnext/agentics/workflows/daily-repo-status.md@7c7feb61a52b662eb2089aa2945588b7a200d404
---

# Rapport Quotidien du Dépôt

Crée un rapport quotidien positif sur l'état du dépôt sous forme d'issue GitHub.

## Ce qu'il faut inclure

- Activité récente du dépôt (issues, PRs, discussions, releases, changements de code)
- Suivi de progression, rappels des objectifs et points marquants
- État du projet et recommandations
- Prochaines étapes concrètes pour les mainteneurs

## Style

- Sois positif, encourageant et utile 🌟
- Utilise les emojis avec modération pour l'engagement
- Reste concis — adapte la longueur à l'activité réelle

## Processus

1. Rassemble l'activité récente du dépôt
2. Étudie le dépôt, ses issues et ses pull requests
3. Crée une nouvelle issue GitHub avec tes conclusions et insights
