Lance le workflow QA complet de bout en bout : analyse → conception → formatage → import → exécution → rapport.

## Instructions

Orchestre l'ensemble du pipeline QA en séquence en utilisant les agents appropriés à chaque étape.

**Parsing des arguments (`$ARGUMENTS`) :**
- Chemin de fichier (ex: `specs/user-story.md`) → utiliser comme source d'analyse
- `url:https://...` → URL de l'application à tester
- `skip:import` → sauter l'étape d'import Quality Plus
- `only:analyze,design` → n'exécuter que ces étapes
- `module:NomModule` → restreindre à un module spécifique

## Séquence d'exécution

### Étape 1/6 — Analyse des spécifications
**Agent :** `story-analyzer`
- Lire le fichier source fourni en argument (ou demander)
- Extraire les exigences testables
- Produire : `outputs/requirements.md`
- ✋ Pause : afficher les exigences extraites et demander confirmation avant de continuer

### Étape 2/6 — Conception des cas de test
**Agent :** `test-designer`
- Source : `outputs/requirements.md`
- Concevoir les cas de test avec les techniques appropriées
- Produire : `outputs/test-cases.md`
- ✋ Pause : afficher le nombre de cas conçus et demander confirmation

### Étape 3/6 — Formatage pour Quality Plus
**Agent :** `test-formatter`
- Source : `outputs/test-cases.md`
- Transformer en CSV compatible Quality Plus
- Produire : `outputs/test-cases-import.csv`

### Étape 4/6 — Import sur Quality Plus
**Agent :** `quality-plus-importer`
- Source : `outputs/test-cases-import.csv`
- Automatiser l'import via Chrome
- ⚠️ Sauter cette étape si `skip:import` dans les arguments
- ✋ Pause : demander confirmation avant l'upload

### Étape 5/6 — Exécution des tests
**Agent :** `test-executor`
- Source : `outputs/test-cases.md`
- URL : extraite des arguments (`url:...`) ou demandée
- Exécuter dans l'ordre P1 → P2 → P3
- Produire : `outputs/execution-results.md`, `outputs/bugs-found.md`

### Étape 6/6 — Génération du rapport
**Agent :** `report-generator`
- Sources : tous les fichiers `outputs/`
- Produire : `outputs/qa-report.md`, `outputs/qa-report-summary.md`
- Afficher la recommandation GO/NO-GO dans le terminal

## Règles du workflow

- Afficher la progression : `[2/6] Conception des cas de test...`
- Chaque étape peut être relancée indépendamment si elle échoue
- Ne jamais sauter une étape sans le signaler explicitement
- Toujours sauvegarder les artefacts intermédiaires dans `outputs/`
- En cas d'erreur bloquante, arrêter et indiquer clairement l'étape en échec et la correction à apporter

## Résumé final

À la fin du workflow, afficher :
```
═══════════════════════════════════════
  WORKFLOW QA TERMINÉ
═══════════════════════════════════════
  Exigences analysées  : [N] fonctionnalités
  Cas de test conçus   : [N] cas
  Cas exportés         : [N] cas
  Import Quality Plus  : ✅ / ⚠️ / ⏭ sauté
  Résultats exécution  : PASS=[n] FAIL=[n] BLOCKED=[n]
  Bugs détectés        : [n] (Critique=[n] Majeur=[n])
  Recommandation       : ✅ GO / ⚠️ GO avec réserves / ❌ NO-GO
  Rapport              : outputs/qa-report.md
═══════════════════════════════════════
```

Paramètres : $ARGUMENTS
