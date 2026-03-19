# Stricture-QA — Contexte du Projet

## Description
Projet de QA automatisé couvrant le cycle complet : analyse des spécifications → conception des cas de test → import sur Quality Plus → exécution → reporting.

## Workflow QA

```
Lien Jira ou fichier local
        ↓
[/qa-analyze]  → story-analyzer       → requirements.md
        ↓
[/qa-design]   → test-designer        → test-cases.md
        ↓
[/qa-format]   → test-formatter       → test-cases-import.csv / .xlsx
        ↓
[/qa-import]   → quality-plus-importer → Quality Plus (web)
        ↓
[/qa-execute]  → test-executor        → execution-results.md
        ↓
[/qa-report]   → report-generator     → qa-report.md / .html
```

## Commandes disponibles

| Commande | Description |
|---|---|
| `/qa-analyze` | Analyse les user stories ou specs et extrait les exigences testables |
| `/qa-design` | Conçoit les cas de test à partir des exigences |
| `/qa-format` | Formate les cas de test pour l'import Quality Plus |
| `/qa-import` | Importe les cas de test sur Quality Plus via le navigateur |
| `/qa-execute` | Exécute les tests sur l'application cible |
| `/qa-report` | Génère le rapport de résultats |
| `/qa-workflow` | Lance le workflow QA complet de bout en bout |

## Structure des fichiers de travail

```
outputs/
├── requirements.md          ← exigences extraites
├── test-cases.md            ← cas de test conçus
├── test-cases-import.csv    ← format Quality Plus
├── execution-results.md     ← résultats d'exécution
└── qa-report.md             ← rapport final
```

## Configuration Jira

Renseigner `.claude/jira-config.md` avec les paramètres de base :
- `JIRA_BASE_URL` — ex: `https://monentreprise.atlassian.net`
- `JIRA_PROJECT_KEY` — clé du projet (ex: `GEO`)

La récupération se fait via Chrome (déjà connecté à Jira) — aucun token API requis.

**Usage :**
```bash
/qa-analyze https://monentreprise.atlassian.net/browse/GEO-1       # Epic
/qa-analyze https://monentreprise.atlassian.net/browse/GEO-42      # Story
/qa-analyze https://monentreprise.atlassian.net/jira/software/projects/GEO/boards/1  # Sprint
/qa-analyze epics/epics.md                                          # Fichier local (compatible)
```

## Conventions

- Les cas de test suivent le format: ID | Module | Titre | Préconditions | Étapes | Résultat attendu | Priorité
- Priorités: P1 (Critique), P2 (Majeur), P3 (Mineur)
- Statuts d'exécution: PASS | FAIL | BLOCKED | SKIPPED
- Tout artefact généré est sauvegardé dans `outputs/`
