# Analyse des Exigences — EPIC-003 : [GEO Module] Category View Dashboard

**Source analysée :** https://onclusive.atlassian.net/browse/DIGIMIND-18640
**Epic Key :** CATEGORY-001
**Date :** 2026-03-18
**Analyste :** story-analyzer
**Product Area :** AI Presence
**Epics liés :** EPIC-004 (Overview), EPIC-002 (Actions Center), EPIC-005 (Sidebar Navigation)

---

## Résumé

Le **Category View Dashboard** fournit une vue unifiée des performances d'une marque dans une catégorie produit spécifique (ex: "Electric Vehicles"). Il combine 3 dimensions d'analyse : Visibility (SOV), Competitive (Win Rate), et Perception (Sentiment). L'utilisateur principal est le PR & Communications Manager. Le dashboard est accessible via les items de la sidebar (dots colorés), avec URL parameter `?view=category&categoryId=N`. Il supporte jusqu'à 5 providers LLM et plusieurs marchés.

---

## Fonctionnalités Identifiées

---

### F-001 — Category View Header & Filtres (Feature 1 — Story CATEGORY-001-001)

- **Description :** Header affichant le nom de la catégorie, un sélecteur de marché, et des toggles LLM pour filtrer l'ensemble du dashboard.
- **Critères d'acceptation :**
  - CA-001 : Header affiche : nom de la catégorie avec color dot correspondant, dropdown market selector (si multi-marché), toggles LLM (jusqu'à 5).
  - CA-002 : Sélection d'un marché → toutes les sections du dashboard filtrent sur ce marché uniquement.
  - CA-003 : Sélection "Gemini only" → tous les métriques recalculés avec les données Gemini uniquement.
- **Règles métier :**
  - Marché par défaut : "All Markets".
  - Max 5 providers LLM en simultané.
  - Le filtre marché affecte toutes les sections (matrix, questions, perception, sources).
- **Préconditions :** Analyse complétée pour la catégorie. L'utilisateur navigue via la sidebar.
- **Cas limites détectés :**
  - Rapport single-market → market selector masqué ou affiché en lecture seule ?
  - LLM avec données partielles → toggle disponible mais métriques incomplets
  - Tous les LLM désactivés → état vide ou toggle bloqué ?

---

### F-002 — Brand Prioritization Matrix (Feature 2 — Story CATEGORY-001-002)

- **Description :** Scatter plot SVG positionnant les marques selon leur SOV (X) et leur Win Rate / Competitiveness (Y). Visualisation du paysage compétitif en un coup d'œil.
- **Critères d'acceptation :**
  - CA-004 : Matrix affiche : X-axis = Share of Voice (0-100%), Y-axis = Competitiveness / Win Rate (0-100%), grid lines aux midpoints (quadrants), entité cible + top 4 compétiteurs par pays (classés par SOV).
  - CA-005 : Formule SOV : `visibility × (2 / (avgPosition + 1))`.
  - CA-006 : Absence de données compétitives (pas de questions competitive) → brand dots affichés à Y=0 (pas de Win Rate), matrix toujours utilisable pour comparaison SOV.
  - CA-007 : Chaque brand = cercle avec logo + SOV ring (épaisseur proportionnelle), entité cible highlightée avec bordure bleue.
  - CA-008 : Échec du logo service → cercle avec initiales (lettermark fallback).
  - CA-009 : Rapport multi-marché + hover sur un dot → market flags affichant les marchés de présence de la marque.
  - CA-010 : Mode "All Markets" → chaque pays sélectionne ses propres top 4 compétiteurs depuis les rankings filtrés par LLM.
- **Règles métier :**
  - Limité à : entité + top 4 compétiteurs par pays.
  - Matrix SVG responsive.
  - SOV calculé même sans données compétitives (Y=0 dans ce cas).
- **Préconditions :** Données visibility disponibles. Données competitive optionnelles.
- **Cas limites détectés :**
  - AvgPosition = 0 → SOV = Visibility × 2 (formule correcte mais valeur extrême)
  - Marque non mentionnée par les LLMs → absente de la matrix ou affichée à (0,0) ?
  - Moins de 4 compétiteurs disponibles → matrix avec moins de dots
  - Entité exactement ex-aequo avec un compétiteur → position chevauchée

---

### F-003 — 5 Metric Cards (contenu épic — DoD)

- **Description :** 5 cartes KPI affichées sous le header : SOV, Visibility, Avg Position, LLM Choice, Sentiment.
- **Critères d'acceptation :**
  - CA-011 : Les 5 cartes s'affichent : SOV, Visibility, Avg Position, LLM Choice, Sentiment.
  - CA-012 : Les valeurs se recalculent lors du changement de filtre marché ou LLM.
- **Préconditions :** Analyse complétée.
- **Cas limites détectés :**
  - Données partielles (1 seul LLM) → métriques affichés avec indication de couverture limitée ?

---

### F-004 — Perception Summary Banner (Feature 3 — Story CATEGORY-001-003)

- **Description :** Bannière AI-generated résumant la perception de la marque dans cette catégorie. Design avec icône Sparkles et dégradé.
- **Critères d'acceptation :**
  - CA-013 : Bannière affiche : fond dégradé (blue-50 → purple-50, border blue-200), icône Sparkles (blue-500), texte AI-generated.
  - CA-014 : Changement de marché → bannière mise à jour avec le résumé per-market per-category correspondant.
  - CA-015 : Summaries non disponibles (rapports anciens) → fallback vers **Key Insight Banner** (règle-based, métriques contextuels).
- **Règles métier :**
  - Summaries récupérés via `GET /api/reports/:id/perception-summary`.
  - Fallback obligatoire pour les rapports qui n'ont pas de summaries AI.
- **Préconditions :** Rapport complété. Endpoint perception-summary accessible.
- **Cas limites détectés :**
  - Endpoint perception-summary en erreur (500) → fallback Key Insight Banner ou message d'erreur ?
  - Summary vide (string vide retourné) → afficher fallback ou bannière vide ?
  - Market "All Markets" sélectionné → quel summary afficher (global ou premier marché) ?

---

### F-005 — Brand Rankings Table (contenu épic — DoD)

- **Description :** Tableau des marques classées par SOV pour cette catégorie, affiché après la matrix.
- **Critères d'acceptation :**
  - CA-016 : Tableau affiché après la Brand Prioritization Matrix.
  - CA-017 : Colonnes : Brand, SOV %, Visibility %, Avg Position, Win Rate.
  - CA-018 : Valeurs recalculées au changement de filtre marché ou LLM.
- **Préconditions :** Données visibility disponibles.
- **Cas limites détectés :**
  - Win Rate = N/A si pas de données compétitives → colonne affichée avec "-" ou masquée ?

---

### F-006 — Sentiment & Key Concepts (TopConceptsChart — DoD)

- **Description :** Section affichant les topics de sentiment et concepts-clés pour cette catégorie, affichée après Brand Rankings.
- **Critères d'acceptation :**
  - CA-019 : Section TopConceptsChart affichée après Brand Rankings Table.
  - CA-020 : Topics et concepts-clés de sentiment affichés pour la catégorie courante.
  - CA-021 : Mise à jour au changement de filtre marché ou LLM.
- **Préconditions :** Données perception disponibles.

---

### F-007 — Unified Questions Table — Visibility + Competitive (Feature 4 — Story CATEGORY-001-004)

- **Description :** Tableau combiné des questions Visibility et Competitive avec barre de favorabilité, filtres et side panel.
- **Critères d'acceptation :**
  - CA-022 : Favorability filter affiche labels texte uniquement : "Favorable", "Split", "Not Favorable".
  - CA-023 : Filtre "Not Favorable" → uniquement les questions où la marque n'est pas classée #1 (visibility) ou n'a pas gagné (competitive).
  - CA-024 : Colonnes : icône type (visibility/competitive), texte de la question, winner/themes (avec indicateur "Split" si LLMs en désaccord), market flag (si multi-marché).
  - CA-025 : Clic sur une ligne → side panel avec : texte complet de la question, ranking complet par LLM (top entités avec badges de rang), liens sources, contexte marché.
  - CA-026 : Barre de favorabilité résumée dans le header collapsible du tableau.
- **Règles métier :**
  - "Split" = LLMs ne s'accordent pas sur le gagnant.
  - Side panel = vue détaillée per-LLM.
  - Filtrage mémoïsé pour les grands ensembles de questions (performance).
- **Préconditions :** Questions visibility et/ou competitive analysées.
- **Cas limites détectés :**
  - 0 questions "Not Favorable" → message "No results" ou filtre désactivé ?
  - Question avec un seul LLM → pas d'indicateur "Split" possible
  - Split exact 50/50 (ex: 2 LLMs pour brand A, 2 pour brand B) → critère de split à préciser

---

### F-008 — Perception Questions Table (Feature 5 — Story CATEGORY-001-005)

- **Description :** Tableau des questions de perception avec filtre sentiment et side panel de réponses LLM.
- **Critères d'acceptation :**
  - CA-027 : Sentiment filter affiche : Positive, Mixed, Negative.
  - CA-028 : Tableau affiche : texte de la question, indicateur sentiment, badge LLM.
  - CA-029 : Clic sur une ligne → side panel avec : réponses brutes LLM par provider, thèmes/topics extraits, citations sources.
- **Préconditions :** Questions perception analysées.
- **Cas limites détectés :**
  - Aucune question "Negative" → filtre désactivé ou message "No negative perceptions" ?
  - LLM avec réponse vide → side panel affiche "(No response)" ?
  - Question de perception avec sentiment "Mixed" sur certains LLMs, "Positive" sur d'autres → classification globale ?

---

### F-009 — Sentiment Distribution Chart (Feature 6 — Story CATEGORY-001-006)

- **Description :** Barre horizontale montrant la répartition Positive / Mixed / Negative du sentiment pour cette catégorie.
- **Critères d'acceptation :**
  - CA-030 : Barre horizontale affiche 3 segments : vert (positive), orange (mixed), rouge (negative).
  - CA-031 : Largeurs des segments proportionnelles aux comptages.
  - CA-032 : Mise à jour au changement de filtre marché ou LLM.
- **Préconditions :** Données perception avec comptages sentiment disponibles.
- **Cas limites détectés :**
  - 100% positive → segments mixed et negative absents ou affichés à 0px ?
  - 0 question de perception → chart masqué ou vide ?

---

### F-010 — AI Citation Sources — viewContext='category' (Feature 7 — Story CATEGORY-001-007)

- **Description :** Analyse des sources citées par les LLMs dans cette catégorie : stacked bar chart (11 types), tableau des domaines prioritaires, lignes expandables.
- **Critères d'acceptation :**
  - CA-033 : Stacked bar chart : distribution des types de sources (11-category taxonomy), légende cliquable pour filtrer par type, comptages par type.
  - CA-034 : Tableau domaines : colonnes Domain (favicon), Source Type (badge coloré), Priority (score bar : Rouge ≥70, Amber 50-69, Blue 30-49, Slate <30), Citations (count), Impact Area (icônes Eye=visibility/blue, Trophy=competitive/amber).
  - CA-035 : `viewContext='category'` → affiche uniquement Visibility Gaps + Competitive Losses (pas Reputation Issues — déplacé dans EPIC-002 Actions Center).
  - CA-036 : Clic expand sur une ligne → panels : Visibility Gaps (border bleue), Competitive Losses (border ambre), LLM Citations (badges par LLM).
  - CA-037 : Lignes expandées → section "Cited URLs" : jusqu'à 6 items (favicon, titre lisible, domain/path, logos LLM provider, badge source type). Bouton "View All" si > 6 URLs → modal scrollable.
- **Règles métier :**
  - 11 catégories de types de source.
  - Score Priority : Rouge ≥70 / Amber 50-69 / Blue 30-49 / Slate <30.
  - viewContext='category' ≠ viewContext='overview' (scope différent).
- **Préconditions :** Données de citation disponibles pour la catégorie.
- **Cas limites détectés :**
  - Domaine sans favicon → icône générique.
  - 0 Competitive Losses pour un domaine → panel "Competitive Losses" masqué ou vide ?
  - Modal "View All" avec des centaines d'URLs → pagination nécessaire ?
  - Domain row avec priority score = 70 exactement → Rouge ou Amber ? (border case)

---

### F-011 — Multi-Market Support (Feature 8 — Story CATEGORY-001-008)

- **Description :** Filtrage par marché appliqué à toutes les sections du dashboard.
- **Critères d'acceptation :**
  - CA-038 : Market selector dropdown affiche tous les marchés du rapport + "All Markets".
  - CA-039 : Sélection d'un marché → toutes les sections filtrent : matrix, questions (unified + perception), sources, métriques.
  - CA-040 : Exemple : rapport avec 3 marchés (US, Germany, Japan) → dropdown avec 4 options (3 + All Markets).
- **Règles métier :**
  - "All Markets" = vue agrégée (chaque pays contribue avec ses propres top 4 compétiteurs pour la matrix).
- **Préconditions :** Rapport avec ≥ 2 marchés.
- **Cas limites détectés :**
  - Rapport single-market → market selector non affiché (comportement attendu mais non explicité)
  - Marché sans données pour cette catégorie → toutes les sections vides

---

### F-012 — Analysis Pending State (Feature 9 — Story CATEGORY-001-009)

- **Description :** État d'attente affiché quand l'analyse d'une catégorie n'est pas encore complète.
- **Critères d'acceptation :**
  - CA-041 : Analyse non complète → affiche : icône Clock, titre "Analysis Pending", description "Analysis for {category} is in progress", indicateur de progression si disponible.
- **Préconditions :** Rapport en cours de traitement.
- **Cas limites détectés :**
  - Analyse en erreur (FAILED) → même état "Pending" ou état d'erreur dédié ?
  - Analyse partiellement complète (certaines dimensions OK, d'autres en cours) → afficher les données disponibles ou tout masquer ?

---

## Hors Scope (Out of Scope)

Les éléments suivants sont **explicitement exclus** de cet epic :
- Comparaison cross-categories
- Graphiques d'évolution historique (Trend charts)
- Alertes automatiques
- Export / Download
- Section "Improvement areas" → déplacée dans EPIC-002 Actions Center

---

## Ambiguïtés et Points d'Attention

| ID | Description | Impact |
|---|---|---|
| AMB-001 | Rapport single-market : market selector affiché en lecture seule ou masqué ? | Moyen |
| AMB-002 | Tous les LLM toggles désactivés : état vide, message d'erreur, ou blocage du toggle ? | Haut |
| AMB-003 | Endpoint `perception-summary` en erreur (500) : fallback Key Insight Banner ou message d'erreur visible ? | Haut |
| AMB-004 | Summary "All Markets" : quel résumé afficher — global ou premier marché disponible ? | Moyen |
| AMB-005 | Indicateur "Split" : critère exact non défini (ex: majorité vs 50/50 strict) | Moyen |
| AMB-006 | Domain priority score = 70 exactement : classé Rouge (≥70) ou Amber (50-69) ? Borne inclusive non précisée | Bas |
| AMB-007 | Analyse catégorie en état FAILED : même écran "Analysis Pending" ou écran d'erreur dédié ? | Moyen |
| AMB-008 | Analyse partiellement complète (ex: visibility OK, competitive en cours) : afficher données partielles ou tout masquer ? | Haut |

---

## Matrice de Couverture Suggérée

| Fonctionnalité | Priorité | Nombre de cas estimé |
|---|---|---|
| F-001 — Header & Filtres LLM/Marché | P1 | 7 |
| F-002 — Brand Prioritization Matrix | P1 | 10 |
| F-003 — 5 Metric Cards | P1 | 5 |
| F-004 — Perception Summary Banner | P2 | 5 |
| F-005 — Brand Rankings Table | P2 | 4 |
| F-006 — Sentiment & Key Concepts | P2 | 3 |
| F-007 — Unified Questions Table | P1 | 9 |
| F-008 — Perception Questions Table | P2 | 6 |
| F-009 — Sentiment Distribution Chart | P2 | 4 |
| F-010 — AI Citation Sources | P2 | 8 |
| F-011 — Multi-Market Support | P1 | 5 |
| F-012 — Analysis Pending State | P3 | 3 |
| **TOTAL** | | **~69 cas** |

---

## Stories Enfants Détectées

| Ticket Jira | À explorer |
|---|---|
| DIGIMIND-18766 | https://onclusive.atlassian.net/browse/DIGIMIND-18766 |
| DIGIMIND-18767 | https://onclusive.atlassian.net/browse/DIGIMIND-18767 |
| DIGIMIND-18768 | https://onclusive.atlassian.net/browse/DIGIMIND-18768 |
| DIGIMIND-18769 | https://onclusive.atlassian.net/browse/DIGIMIND-18769 |
| DIGIMIND-18770 | https://onclusive.atlassian.net/browse/DIGIMIND-18770 |
| DIGIMIND-18771 | https://onclusive.atlassian.net/browse/DIGIMIND-18771 |
| DIGIMIND-18772 | https://onclusive.atlassian.net/browse/DIGIMIND-18772 |
| DIGIMIND-18773 | https://onclusive.atlassian.net/browse/DIGIMIND-18773 |
| DIGIMIND-18774 | https://onclusive.atlassian.net/browse/DIGIMIND-18774 |
| DIGIMIND-18775 | https://onclusive.atlassian.net/browse/DIGIMIND-18775 |
| DIGIMIND-19063 | https://onclusive.atlassian.net/browse/DIGIMIND-19063 |
