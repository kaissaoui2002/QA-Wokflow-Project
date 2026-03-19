Génère le rapport QA final consolidé avec métriques, bugs et recommandations.

## Instructions

Utilise l'agent `report-generator` pour synthétiser tous les résultats.

**Sources d'entrée :**
- `outputs/execution-results.md` — résultats d'exécution
- `outputs/bugs-found.md` — bugs détectés (si existant)
- `outputs/test-cases.md` — référence des cas planifiés
- `outputs/requirements.md` — référence des exigences (pour couverture)

**Parsing des arguments (`$ARGUMENTS`) :**
- (vide) → rapport complet Markdown
- `summary` → résumé exécutif uniquement (1 page)
- `html` → générer aussi une version HTML basique
- `sprint:NomSprint` → inclure le nom du sprint dans le titre

**Actions à effectuer :**
1. Lire tous les fichiers de résultats disponibles
2. Calculer les métriques : taux d'exécution, taux de succès, répartition par module
3. Compiler la liste des bugs avec leur sévérité
4. Analyser les zones à risque
5. Formuler une recommandation GO / NO-GO claire
6. Générer `outputs/qa-report.md`
7. Générer `outputs/qa-report-summary.md` (résumé exécutif)
8. Si argument `html` : générer `outputs/qa-report.html`

**Règle GO/NO-GO :**
- ❌ NO-GO si : bug(s) critique(s) ouvert(s) OU taux d'échec > 20%
- ⚠️ GO avec réserves si : bugs majeurs non résolus OU taux d'échec 10-20%
- ✅ GO si : aucun bug critique, taux d'échec < 10%

**À la fin**, afficher le résumé et la recommandation directement dans le terminal.

Options : $ARGUMENTS
