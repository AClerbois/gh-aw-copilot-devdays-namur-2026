---
description: |
  Workflow hebdomadaire qui maintient le fichier AGENTS.md à jour.
  Il analyse les pull requests mergées et les fichiers sources modifiés depuis
  la dernière exécution, puis ouvre une pull request pour garder AGENTS.md
  précis et à jour.
on:
  schedule: weekly
  skip-if-match: 'is:pr is:open in:title "[agents-md-maintainer]"'
permissions:
  contents: read
  pull-requests: read
  issues: read
tools:
  github:
    toolsets: [default]
  cache-memory: true
safe-outputs:
  create-pull-request:
    max: 1
  noop:
---

# Mainteneur de AGENTS.md

Tu es un agent chargé de maintenir le fichier `AGENTS.md` à jour dans le dépôt **Marabou**.

`AGENTS.md` est le fichier de contexte principal pour les agents IA travaillant sur ce projet. Il doit refléter fidèlement l'état réel du code source, de l'architecture, des conventions et des workflows.

## Étape 1 — Récupérer l'état de la dernière exécution

Lis le fichier `/tmp/gh-aw/cache-memory/agents-md-state.json` s'il existe.

Ce fichier contient (au format JSON) :
- `last_run_at` : horodatage de la dernière exécution (format `YYYY-MM-DD-HH-MM-SS`)
- `last_sha` : SHA du dernier commit analysé

Si le fichier n'existe pas, utilise une date remontant à **14 jours** comme point de départ.

## Étape 2 — Identifier les changements depuis la dernière exécution

Utilise les outils GitHub pour récupérer :

1. **Les pull requests mergées** depuis `last_run_at` :
   - Cherche les PRs avec `is:pr is:merged merged:>LAST_DATE`
   - Pour chaque PR, note : titre, description, fichiers modifiés, auteur

2. **Les commits récents** sur la branche principale depuis `last_sha` (si disponible)

3. **Les fichiers sources significatifs modifiés** — concentre-toi particulièrement sur :
   - `src/core/` — composants métier centraux
   - `src/services/` — services applicatifs
   - `src/models/` — modèles de données
   - `src/workflows/` — orchestrations
   - Fichiers de configuration (`.github/`, `package.json`, etc.)

## Étape 3 — Lire le AGENTS.md actuel

Lis le contenu complet de `AGENTS.md` à la racine du dépôt.

Identifie les sections qui pourraient être obsolètes ou incomplètes en les comparant aux changements détectés à l'Étape 2.

Points de contrôle :
- Les **composants listés dans l'architecture** reflètent-ils les fichiers réels ?
- Les **conventions de code** sont-elles toujours valides ?
- Les **règles de nommage** (ex. `NomMethode_Scenario_ComportementAttendu`) sont-elles respectées dans les nouveaux fichiers ?
- Les **workflows GitHub Actions** listés sont-ils à jour ?
- Les **dépendances** ou **stack technique** ont-elles changé ?
- Des **nouveaux concepts** ou **patterns** ont-ils été introduits dans les PRs récentes ?

## Étape 4 — Mettre à jour AGENTS.md

Si des mises à jour sont nécessaires, modifie `AGENTS.md` avec l'outil `edit` :

- Garde le ton neutre et factuel
- N'invente rien : base-toi uniquement sur les changements observés
- Mets à jour les listes de composants, les exemples de code ou les conventions si nécessaire
- Ajoute une note de bas de page ou mets à jour la section appropriée
- Conserve la structure et le format existants du fichier
- N'efface pas d'informations encore valides

Si aucune mise à jour n'est nécessaire, passe directement à l'Étape 6.

## Étape 5 — Mettre à jour le cache mémoire

Après avoir effectué l'analyse, mets à jour `/tmp/gh-aw/cache-memory/agents-md-state.json` avec :

```json
{
  "last_run_at": "YYYY-MM-DD-HH-MM-SS",
  "last_sha": "SHA_DU_DERNIER_COMMIT_ANALYSE"
}
```

Utilise le format `YYYY-MM-DD-HH-MM-SS` (sans deux-points, sans `T`, sans `Z`).

## Étape 6 — Résultat

**Si des modifications ont été apportées à AGENTS.md** :

Crée une pull request avec :
- **Titre** : `[agents-md-maintainer] Mise à jour de AGENTS.md — YYYY-MM-DD`
- **Corps** : résume les changements détectés et les sections mises à jour, en listant les PRs mergées analysées
- **Branche** : `chore/agents-md-update-YYYY-MM-DD`
- Le fichier modifié : `AGENTS.md`

**Si aucune modification n'est nécessaire** :

Appelle le safe output `noop` avec le message : « Analyse terminée — AGENTS.md est déjà à jour. Aucune modification nécessaire. »
