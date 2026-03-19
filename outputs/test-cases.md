# Cas de Test — EPIC-003 : Category View Dashboard

**Source :** outputs/requirements.md
**Epic :** CATEGORY-001 (DIGIMIND-18640)
**Date :** 2026-03-18
**Concepteur :** test-designer
**Total cas :** 69

---

## Module : HEADER — F-001 Category View Header & Filtres

---

## HEADER-001 — Affichage initial du header en mode multi-marché

| Champ | Valeur |
|---|---|
| **ID** | HEADER-001 |
| **Module** | Header & Filtres |
| **Fonctionnalité** | F-001 — Category View Header & Filtres |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Rapport complété avec ≥ 2 marchés. Catégorie "Electric Vehicles" configurée avec color dot. 3 providers LLM actifs. L'utilisateur est connecté et navigue via la sidebar. |

**Étapes :**
1. Naviguer vers le Category View Dashboard via la sidebar (clic sur le dot coloré de la catégorie "Electric Vehicles").
2. Observer le header affiché.

**Données de test :**
- Catégorie : Electric Vehicles (dot coloré = bleu)
- Marchés disponibles : US, Germany, Japan
- Providers LLM actifs : ChatGPT, Gemini, Perplexity

**Résultat attendu :**
Le header affiche : (1) le nom "Electric Vehicles" avec le dot coloré correspondant, (2) un dropdown market selector avec les options "All Markets", "US", "Germany", "Japan" — valeur par défaut "All Markets", (3) 3 toggles LLM (ChatGPT, Gemini, Perplexity) tous activés par défaut.

**Critère d'acceptation couvert :** CA-001

---

## HEADER-002 — Affichage du header avec 5 providers LLM (maximum)

| Champ | Valeur |
|---|---|
| **ID** | HEADER-002 |
| **Module** | Header & Filtres |
| **Fonctionnalité** | F-001 — Category View Header & Filtres |
| **Type** | Limite |
| **Priorité** | P1 |
| **Préconditions** | Rapport configuré avec exactement 5 providers LLM. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer le nombre de toggles LLM affichés dans le header.

**Données de test :**
- Providers LLM : ChatGPT, Gemini, Perplexity, Claude, Copilot (5 providers)

**Résultat attendu :**
Les 5 toggles LLM sont tous affichés et activés. Aucun toggle supplémentaire n'est présent. L'interface ne déborde pas visuellement.

**Critère d'acceptation couvert :** CA-001

---

## HEADER-003 — Filtrage du dashboard par sélection de marché

| Champ | Valeur |
|---|---|
| **ID** | HEADER-003 |
| **Module** | Header & Filtres |
| **Fonctionnalité** | F-001 — Category View Header & Filtres |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Rapport multi-marché complété (US, Germany, Japan). Dashboard affiché en mode "All Markets". |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Ouvrir le dropdown market selector.
3. Sélectionner "Germany".
4. Observer les sections : Brand Prioritization Matrix, 5 Metric Cards, Brand Rankings Table, Questions Tables, Sources.

**Données de test :**
- Marché sélectionné : Germany

**Résultat attendu :**
Toutes les sections du dashboard (matrix, metric cards, brand rankings, unified questions, perception questions, sentiment chart, sources) se recalculent et affichent uniquement les données du marché "Germany". Le dropdown indique "Germany" comme valeur sélectionnée.

**Critère d'acceptation couvert :** CA-002

---

## HEADER-004 — Filtrage du dashboard par sélection d'un seul LLM (Gemini)

| Champ | Valeur |
|---|---|
| **ID** | HEADER-004 |
| **Module** | Header & Filtres |
| **Fonctionnalité** | F-001 — Category View Header & Filtres |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Rapport avec 3 providers LLM actifs. Dashboard affiché avec tous les LLM activés. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Dans le header, désactiver les toggles ChatGPT et Perplexity (laisser uniquement Gemini activé).
3. Observer les métriques SOV, Visibility, Avg Position, Win Rate dans toutes les sections.

**Données de test :**
- LLM désactivés : ChatGPT, Perplexity
- LLM actif : Gemini

**Résultat attendu :**
Tous les métriques du dashboard (5 cards, matrix, rankings, questions tables) sont recalculés en utilisant uniquement les données Gemini. Les valeurs changent pour refléter uniquement la source Gemini.

**Critère d'acceptation couvert :** CA-003

---

## HEADER-005 — Rapport single-market : comportement du market selector

| Champ | Valeur |
|---|---|
| **ID** | HEADER-005 |
| **Module** | Header & Filtres |
| **Fonctionnalité** | F-001 — Category View Header & Filtres |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Rapport configuré avec un seul marché (US uniquement). |

**Étapes :**
1. Naviguer vers le Category View Dashboard d'un rapport single-market.
2. Observer la présence et l'état du market selector dans le header.

**Données de test :**
- Nombre de marchés : 1 (US seulement)

**Résultat attendu :**
Le market selector est soit masqué (non affiché) soit affiché en lecture seule indiquant "US". Dans les deux cas, aucune interaction de filtrage par marché n'est disponible. (Ambiguïté AMB-001 — à confirmer avec l'équipe produit.)

**Critère d'acceptation couvert :** CA-001

---

## HEADER-006 — Désactivation de tous les toggles LLM

| Champ | Valeur |
|---|---|
| **ID** | HEADER-006 |
| **Module** | Header & Filtres |
| **Fonctionnalité** | F-001 — Category View Header & Filtres |
| **Type** | Négatif |
| **Priorité** | P1 |
| **Préconditions** | Dashboard affiché avec au moins 2 LLM activés. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Désactiver un à un tous les toggles LLM jusqu'à ce qu'aucun ne soit actif.
3. Observer le comportement de l'interface au moment où le dernier toggle est désactivé.

**Données de test :**
- Désactiver séquentiellement : ChatGPT → Gemini → Perplexity

**Résultat attendu :**
Soit (a) le dernier toggle LLM ne peut pas être désactivé (blocage de l'interaction), soit (b) un message d'état vide s'affiche. Le système ne plante pas et ne reste pas dans un état indéfini. (Ambiguïté AMB-002 — comportement à préciser.)

**Critère d'acceptation couvert :** CA-003

---

## HEADER-007 — LLM avec données partielles : toggle disponible

| Champ | Valeur |
|---|---|
| **ID** | HEADER-007 |
| **Module** | Header & Filtres |
| **Fonctionnalité** | F-001 — Category View Header & Filtres |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Rapport avec un provider LLM ayant des données partielles pour la catégorie (ex: Perplexity n'a pas analysé toutes les questions). |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer les toggles LLM dans le header.
3. Activer le provider avec données partielles (Perplexity).
4. Observer les métriques.

**Données de test :**
- Provider partiel : Perplexity (50% des questions analysées)

**Résultat attendu :**
Le toggle Perplexity est disponible et activable. Les métriques recalculés reflètent les données disponibles. Une indication visuelle (ex: icône d'avertissement ou note) signale la couverture partielle.

**Critère d'acceptation couvert :** CA-001, CA-003

---

## Module : MATRIX — F-002 Brand Prioritization Matrix

---

## MATRIX-001 — Affichage nominal de la matrix avec 5 marques

| Champ | Valeur |
|---|---|
| **ID** | MATRIX-001 |
| **Module** | Brand Prioritization Matrix |
| **Fonctionnalité** | F-002 — Brand Prioritization Matrix |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Rapport complété avec données visibility ET competitive. Entité cible + 4 compétiteurs avec données complètes pour le marché US. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer la Brand Prioritization Matrix.

**Données de test :**
- Entité cible : TeslaBrand (SOV=65%, Win Rate=72%)
- Compétiteurs : BMW (SOV=45%, WR=58%), Rivian (SOV=30%, WR=40%), Ford (SOV=25%, WR=35%), GM (SOV=15%, WR=20%)

**Résultat attendu :**
La matrix SVG s'affiche avec : (1) axe X = SOV (0-100%), axe Y = Win Rate (0-100%), (2) gridlines aux midpoints (50%, 50%), (3) 5 cercles positionnés correctement, (4) TeslaBrand avec bordure bleue, (5) chaque cercle avec logo de la marque + ring SOV d'épaisseur proportionnelle.

**Critère d'acceptation couvert :** CA-004, CA-007

---

## MATRIX-002 — Vérification du calcul SOV via la formule

| Champ | Valeur |
|---|---|
| **ID** | MATRIX-002 |
| **Module** | Brand Prioritization Matrix |
| **Fonctionnalité** | F-002 — Brand Prioritization Matrix |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Rapport avec données visibility connues (visibility et avgPosition fixés). |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Relever la valeur SOV affichée pour une marque dans la matrix.
3. Calculer manuellement : `SOV = visibility × (2 / (avgPosition + 1))`.
4. Comparer la valeur calculée à la valeur affichée.

**Données de test :**
- Marque : TeslaBrand
- visibility = 0.80, avgPosition = 1
- SOV attendu = 0.80 × (2 / (1+1)) = 0.80 × 1 = 0.80 = 80%

**Résultat attendu :**
La valeur SOV affichée dans la matrix est 80%, correspondant exactement à la formule `visibility × (2 / (avgPosition + 1))`.

**Critère d'acceptation couvert :** CA-005

---

## MATRIX-003 — Calcul SOV avec avgPosition = 0 (valeur extrême)

| Champ | Valeur |
|---|---|
| **ID** | MATRIX-003 |
| **Module** | Brand Prioritization Matrix |
| **Fonctionnalité** | F-002 — Brand Prioritization Matrix |
| **Type** | Limite |
| **Priorité** | P1 |
| **Préconditions** | Rapport avec une marque ayant avgPosition = 0. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer la valeur SOV de la marque avec avgPosition = 0.

**Données de test :**
- visibility = 0.70, avgPosition = 0
- SOV attendu = 0.70 × (2 / (0+1)) = 0.70 × 2 = 1.40 → plafonné à 100% ?

**Résultat attendu :**
Le SOV calculé est 140% mathématiquement. Le système doit soit plafonner la valeur à 100%, soit la traiter comme cas spécial avec indication. Aucun crash ou affichage de valeur aberrante (>100%) dans la matrix. La position du dot reste dans les limites du canvas SVG.

**Critère d'acceptation couvert :** CA-005

---

## MATRIX-004 — Absence de données compétitives (Y=0 pour toutes les marques)

| Champ | Valeur |
|---|---|
| **ID** | MATRIX-004 |
| **Module** | Brand Prioritization Matrix |
| **Fonctionnalité** | F-002 — Brand Prioritization Matrix |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Rapport avec données visibility uniquement, aucune question competitive configurée. |

**Étapes :**
1. Naviguer vers le Category View Dashboard d'un rapport sans questions competitive.
2. Observer la Brand Prioritization Matrix.

**Données de test :**
- Questions competitive : 0
- Données visibility : disponibles pour toutes les marques

**Résultat attendu :**
La matrix s'affiche. Tous les dots de marques sont positionnés à Y=0 (Win Rate = 0). L'axe Y est toujours affiché. La matrix reste utilisable pour comparer les SOV sur l'axe X. Aucun message d'erreur bloquant n'est affiché.

**Critère d'acceptation couvert :** CA-006

---

## MATRIX-005 — Fallback lettermark si logo indisponible

| Champ | Valeur |
|---|---|
| **ID** | MATRIX-005 |
| **Module** | Brand Prioritization Matrix |
| **Fonctionnalité** | F-002 — Brand Prioritization Matrix |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Logo service renvoie une erreur (404 ou 500) pour au moins une marque. |

**Étapes :**
1. Simuler l'échec du logo service pour la marque "Rivian".
2. Naviguer vers le Category View Dashboard.
3. Observer le dot de Rivian dans la matrix.

**Données de test :**
- Marque avec logo manquant : Rivian
- Initiales attendues : "RI"

**Résultat attendu :**
Le dot de Rivian affiche les initiales "RI" (lettermark fallback) à la place du logo. Le cercle conserve sa taille, sa position et son SOV ring normalement. Les autres marques avec logos valides ne sont pas affectées.

**Critère d'acceptation couvert :** CA-008

---

## MATRIX-006 — Hover sur un dot en mode multi-marché : affichage des market flags

| Champ | Valeur |
|---|---|
| **ID** | MATRIX-006 |
| **Module** | Brand Prioritization Matrix |
| **Fonctionnalité** | F-002 — Brand Prioritization Matrix |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Rapport multi-marché complété (US, Germany, Japan). Dashboard en mode "All Markets". |

**Étapes :**
1. Naviguer vers le Category View Dashboard en mode "All Markets".
2. Survoler (hover) le dot d'une marque présente dans plusieurs marchés (ex: BMW dans US et Germany).
3. Observer le tooltip/overlay affiché.

**Données de test :**
- Marque : BMW
- Marchés de présence : US, Germany

**Résultat attendu :**
Un tooltip s'affiche avec les drapeaux (market flags) des marchés où BMW est présent : drapeau US et drapeau Germany. Le tooltip est lisible et se ferme à la sortie du hover.

**Critère d'acceptation couvert :** CA-009

---

## MATRIX-007 — Mode "All Markets" : top 4 compétiteurs par pays

| Champ | Valeur |
|---|---|
| **ID** | MATRIX-007 |
| **Module** | Brand Prioritization Matrix |
| **Fonctionnalité** | F-002 — Brand Prioritization Matrix |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Rapport avec 3 marchés (US, Germany, Japan), chaque marché ayant des compétiteurs différents dans le top 4. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. S'assurer que le mode "All Markets" est sélectionné.
3. Observer les dots affichés dans la matrix.

**Données de test :**
- US top 4 : BMW, Rivian, Ford, GM
- Germany top 4 : BMW, Volkswagen, Audi, Mercedes
- Japan top 4 : Toyota, Honda, Nissan, Mitsubishi

**Résultat attendu :**
La matrix agrège les compétiteurs de chaque pays selon leurs propres rankings filtrés par LLM. Des marques présentes dans plusieurs pays peuvent apparaître avec une position agrégée. L'entité cible est toujours mise en évidence avec bordure bleue.

**Critère d'acceptation couvert :** CA-010

---

## MATRIX-008 — Moins de 4 compétiteurs disponibles

| Champ | Valeur |
|---|---|
| **ID** | MATRIX-008 |
| **Module** | Brand Prioritization Matrix |
| **Fonctionnalité** | F-002 — Brand Prioritization Matrix |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Rapport avec seulement 2 compétiteurs identifiés pour la catégorie. |

**Étapes :**
1. Naviguer vers le Category View Dashboard d'un rapport avec 2 compétiteurs uniquement.
2. Observer la Brand Prioritization Matrix.

**Données de test :**
- Entité cible : TeslaBrand
- Compétiteurs disponibles : BMW, Rivian (seulement 2)

**Résultat attendu :**
La matrix s'affiche avec 3 dots seulement (entité cible + 2 compétiteurs). Aucun dot vide ou placeholder n'est affiché pour les emplacements manquants. La matrix reste fonctionnelle.

**Critère d'acceptation couvert :** CA-004

---

## MATRIX-009 — Marque non mentionnée par les LLMs

| Champ | Valeur |
|---|---|
| **ID** | MATRIX-009 |
| **Module** | Brand Prioritization Matrix |
| **Fonctionnalité** | F-002 — Brand Prioritization Matrix |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Rapport où un compétiteur n'est jamais mentionné par aucun LLM dans cette catégorie. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer si la marque sans mention LLM apparaît dans la matrix.

**Données de test :**
- Marque sans mention LLM : "BrandX" (0% SOV, 0% Win Rate)

**Résultat attendu :**
La marque sans mention LLM est soit absente de la matrix (non comptabilisée dans les top 4), soit affichée en position (0,0) avec un indicateur visuel spécifique. Le comportement est cohérent et documenté.

**Critère d'acceptation couvert :** CA-004

---

## MATRIX-010 — Responsivité SVG de la matrix

| Champ | Valeur |
|---|---|
| **ID** | MATRIX-010 |
| **Module** | Brand Prioritization Matrix |
| **Fonctionnalité** | F-002 — Brand Prioritization Matrix |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Dashboard chargé sur un écran standard (1920x1080). |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Réduire la largeur du navigateur progressivement (1920 → 1280 → 768px).
3. Observer la matrix à chaque résolution.

**Données de test :**
- Résolutions : 1920px, 1280px, 768px

**Résultat attendu :**
La matrix SVG se redimensionne correctement à chaque résolution. Les dots, axes, gridlines et labels restent lisibles. Aucun élément ne sort du conteneur SVG. Les proportions des positions relatives sont maintenues.

**Critère d'acceptation couvert :** CA-004

---

## Module : METRICS — F-003 5 Metric Cards

---

## METRICS-001 — Affichage des 5 cartes KPI

| Champ | Valeur |
|---|---|
| **ID** | METRICS-001 |
| **Module** | 5 Metric Cards |
| **Fonctionnalité** | F-003 — 5 Metric Cards |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Rapport complété avec données complètes pour la catégorie. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer les cartes KPI affichées sous le header.

**Données de test :**
- Rapport avec données complètes : SOV, Visibility, Avg Position, LLM Choice, Sentiment tous calculés.

**Résultat attendu :**
5 cartes KPI sont affichées dans cet ordre : SOV, Visibility, Avg Position, LLM Choice, Sentiment. Chaque carte affiche une valeur numérique et un label. Aucune carte n'est absente ou vide.

**Critère d'acceptation couvert :** CA-011

---

## METRICS-002 — Recalcul des métriques au changement de marché

| Champ | Valeur |
|---|---|
| **ID** | METRICS-002 |
| **Module** | 5 Metric Cards |
| **Fonctionnalité** | F-003 — 5 Metric Cards |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Rapport multi-marché complété. Dashboard affiché en "All Markets". Valeurs initiales connues. |

**Étapes :**
1. Naviguer vers le Category View Dashboard en "All Markets".
2. Noter les valeurs des 5 cartes KPI.
3. Changer le marché vers "Germany".
4. Observer les nouvelles valeurs des 5 cartes KPI.

**Données de test :**
- Marché initial : All Markets (SOV=45%, Visibility=62%, AvgPos=2.1, LLMChoice=3, Sentiment=72%)
- Marché cible : Germany

**Résultat attendu :**
Les 5 cartes se recalculent immédiatement après la sélection de "Germany". Les valeurs changent pour refléter les données Germany uniquement. L'état de chargement (spinner ou skeleton) est visible pendant le recalcul si celui-ci est asynchrone.

**Critère d'acceptation couvert :** CA-012

---

## METRICS-003 — Recalcul des métriques au changement de filtre LLM

| Champ | Valeur |
|---|---|
| **ID** | METRICS-003 |
| **Module** | 5 Metric Cards |
| **Fonctionnalité** | F-003 — 5 Metric Cards |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Dashboard affiché avec 3 LLM activés. Valeurs initiales connues. |

**Étapes :**
1. Naviguer vers le Category View Dashboard avec ChatGPT, Gemini, Perplexity actifs.
2. Noter les valeurs des 5 cartes KPI.
3. Désactiver ChatGPT et Perplexity (garder seulement Gemini).
4. Observer les nouvelles valeurs des 5 cartes KPI.

**Résultat attendu :**
Les valeurs des 5 cartes se recalculent pour refléter les données Gemini uniquement. Les valeurs sont différentes des valeurs avec 3 LLM actifs.

**Critère d'acceptation couvert :** CA-012

---

## METRICS-004 — Métriques avec données partielles (1 seul LLM)

| Champ | Valeur |
|---|---|
| **ID** | METRICS-004 |
| **Module** | 5 Metric Cards |
| **Fonctionnalité** | F-003 — 5 Metric Cards |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Rapport avec un seul provider LLM ayant des données pour la catégorie. |

**Étapes :**
1. Naviguer vers le Category View Dashboard d'un rapport avec un seul LLM actif.
2. Observer les 5 cartes KPI.

**Données de test :**
- LLM unique : Gemini (couverture = 1/5 providers habituels)

**Résultat attendu :**
Les 5 cartes affichent des valeurs calculées sur Gemini uniquement. Une indication de couverture limitée est visible (ex: note, badge ou icône d'avertissement sur les cartes). Les valeurs sont cohérentes et non aberrantes.

**Critère d'acceptation couvert :** CA-011, CA-012

---

## METRICS-005 — Affichage des 5 cartes après changement de catégorie via sidebar

| Champ | Valeur |
|---|---|
| **ID** | METRICS-005 |
| **Module** | 5 Metric Cards |
| **Fonctionnalité** | F-003 — 5 Metric Cards |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Rapport avec 2 catégories configurées ("Electric Vehicles" et "Autonomous Driving"). |

**Étapes :**
1. Naviguer vers le Category View Dashboard de "Electric Vehicles".
2. Noter les valeurs des 5 cartes.
3. Naviguer vers la catégorie "Autonomous Driving" via la sidebar.
4. Observer les valeurs des 5 cartes.

**Résultat attendu :**
Les 5 cartes affichent les métriques spécifiques à "Autonomous Driving", différents de ceux d'"Electric Vehicles". Aucune valeur résiduelle de la catégorie précédente n'est affichée.

**Critère d'acceptation couvert :** CA-011

---

## Module : BANNER — F-004 Perception Summary Banner

---

## BANNER-001 — Affichage nominal de la bannière AI-generated

| Champ | Valeur |
|---|---|
| **ID** | BANNER-001 |
| **Module** | Perception Summary Banner |
| **Fonctionnalité** | F-004 — Perception Summary Banner |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Rapport complété avec summaries AI disponibles. Endpoint `GET /api/reports/:id/perception-summary` opérationnel et retourne un texte non vide. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer la bannière de perception.

**Résultat attendu :**
La bannière affiche : (1) fond dégradé blue-50 vers purple-50 avec bordure blue-200, (2) icône Sparkles en blue-500, (3) texte AI-generated résumant la perception de la marque dans cette catégorie.

**Critère d'acceptation couvert :** CA-013

---

## BANNER-002 — Mise à jour de la bannière au changement de marché

| Champ | Valeur |
|---|---|
| **ID** | BANNER-002 |
| **Module** | Perception Summary Banner |
| **Fonctionnalité** | F-004 — Perception Summary Banner |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Rapport multi-marché avec summaries AI disponibles par marché. Dashboard affiché sur "All Markets". |

**Étapes :**
1. Naviguer vers le Category View Dashboard en "All Markets".
2. Lire le texte de la bannière AI.
3. Changer le marché vers "Germany".
4. Observer le texte de la bannière.

**Données de test :**
- Summary "All Markets" : "Tesla leads the EV market globally..."
- Summary "Germany" : "In Germany, Tesla faces strong competition from Volkswagen..."

**Résultat attendu :**
La bannière se met à jour avec le summary per-market per-category correspondant à "Germany". Le texte change notablement par rapport au summary "All Markets". Un état de chargement est visible pendant la mise à jour si asynchrone.

**Critère d'acceptation couvert :** CA-014

---

## BANNER-003 — Fallback vers Key Insight Banner (rapport ancien sans summary AI)

| Champ | Valeur |
|---|---|
| **ID** | BANNER-003 |
| **Module** | Perception Summary Banner |
| **Fonctionnalité** | F-004 — Perception Summary Banner |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Rapport ancien ne disposant pas de summaries AI. Endpoint retourne 404 ou réponse vide. |

**Étapes :**
1. Naviguer vers le Category View Dashboard d'un rapport ancien.
2. Observer la bannière affichée.

**Résultat attendu :**
Le **Key Insight Banner** est affiché à la place de la bannière AI. Le Key Insight Banner affiche des métriques contextuels basés sur des règles métier. L'icône Sparkles AI n'est pas présente. Aucun message d'erreur technique n'est visible pour l'utilisateur.

**Critère d'acceptation couvert :** CA-015

---

## BANNER-004 — Fallback si endpoint perception-summary retourne erreur 500

| Champ | Valeur |
|---|---|
| **ID** | BANNER-004 |
| **Module** | Perception Summary Banner |
| **Fonctionnalité** | F-004 — Perception Summary Banner |
| **Type** | Négatif |
| **Priorité** | P1 |
| **Préconditions** | Endpoint `GET /api/reports/:id/perception-summary` configuré pour retourner HTTP 500. |

**Étapes :**
1. Simuler une erreur 500 sur l'endpoint perception-summary.
2. Naviguer vers le Category View Dashboard.
3. Observer la bannière.

**Résultat attendu :**
Le système bascule vers le Key Insight Banner (fallback) sans afficher de message d'erreur technique à l'utilisateur. Le reste du dashboard continue de fonctionner normalement. (Ambiguïté AMB-003 — à confirmer si fallback ou message d'erreur visible.)

**Critère d'acceptation couvert :** CA-015

---

## BANNER-005 — Summary vide retourné par l'API

| Champ | Valeur |
|---|---|
| **ID** | BANNER-005 |
| **Module** | Perception Summary Banner |
| **Fonctionnalité** | F-004 — Perception Summary Banner |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Endpoint perception-summary retourne HTTP 200 avec un string vide `""`. |

**Étapes :**
1. Configurer l'endpoint pour retourner `{"summary": ""}`.
2. Naviguer vers le Category View Dashboard.
3. Observer la bannière.

**Résultat attendu :**
Le système détecte le summary vide et affiche le Key Insight Banner (fallback) plutôt qu'une bannière AI avec contenu vide. Aucune bannière avec fond dégradé et texte vide n'est visible.

**Critère d'acceptation couvert :** CA-015

---

## Module : RANKINGS — F-005 Brand Rankings Table

---

## RANKINGS-001 — Affichage nominal du tableau Brand Rankings

| Champ | Valeur |
|---|---|
| **ID** | RANKINGS-001 |
| **Module** | Brand Rankings Table |
| **Fonctionnalité** | F-005 — Brand Rankings Table |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Rapport complété avec données visibility et competitive. Brand Prioritization Matrix visible. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Faire défiler sous la Brand Prioritization Matrix.
3. Observer le Brand Rankings Table.

**Résultat attendu :**
Le tableau est positionné après la Brand Prioritization Matrix. Les colonnes suivantes sont présentes : Brand, SOV %, Visibility %, Avg Position, Win Rate. Les marques sont classées par SOV décroissant.

**Critère d'acceptation couvert :** CA-016, CA-017

---

## RANKINGS-002 — Recalcul du tableau au changement de filtre

| Champ | Valeur |
|---|---|
| **ID** | RANKINGS-002 |
| **Module** | Brand Rankings Table |
| **Fonctionnalité** | F-005 — Brand Rankings Table |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Rapport multi-marché complété. Dashboard en "All Markets". |

**Étapes :**
1. Naviguer vers le Category View Dashboard en "All Markets".
2. Noter les valeurs et l'ordre des marques dans le tableau.
3. Changer le marché vers "Germany".
4. Observer les nouvelles valeurs et l'ordre.

**Résultat attendu :**
Les valeurs SOV, Visibility, Avg Position, Win Rate se recalculent pour le marché Germany. L'ordre des marques peut changer. Les valeurs sont cohérentes avec les données du marché Germany.

**Critère d'acceptation couvert :** CA-018

---

## RANKINGS-003 — Affichage de la colonne Win Rate sans données compétitives

| Champ | Valeur |
|---|---|
| **ID** | RANKINGS-003 |
| **Module** | Brand Rankings Table |
| **Fonctionnalité** | F-005 — Brand Rankings Table |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Rapport sans questions competitive configurées. |

**Étapes :**
1. Naviguer vers le Category View Dashboard d'un rapport sans données competitive.
2. Observer la colonne Win Rate dans le tableau Brand Rankings.

**Résultat attendu :**
La colonne Win Rate est soit masquée (non affichée), soit affiche "-" pour toutes les marques. Aucune valeur numérique erronée (ex: 0% ou NaN) n'est affichée.

**Critère d'acceptation couvert :** CA-017

---

## RANKINGS-004 — Cohérence des valeurs SOV entre matrix et tableau

| Champ | Valeur |
|---|---|
| **ID** | RANKINGS-004 |
| **Module** | Brand Rankings Table |
| **Fonctionnalité** | F-005 — Brand Rankings Table |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Rapport complété avec données visibility. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Relever la valeur SOV d'une marque dans la Brand Prioritization Matrix (position sur axe X).
3. Relever la valeur SOV de la même marque dans le Brand Rankings Table (colonne SOV %).
4. Comparer les deux valeurs.

**Résultat attendu :**
La valeur SOV % dans le tableau correspond à la position sur l'axe X de la matrix pour la même marque. Les deux sources de données sont cohérentes.

**Critère d'acceptation couvert :** CA-016, CA-017

---

## Module : SENTIMENT — F-006 Sentiment & Key Concepts

---

## SENTIMENT-001 — Affichage de la section TopConceptsChart

| Champ | Valeur |
|---|---|
| **ID** | SENTIMENT-001 |
| **Module** | Sentiment & Key Concepts |
| **Fonctionnalité** | F-006 — Sentiment & Key Concepts |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Rapport complété avec données perception disponibles. Brand Rankings Table visible. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Faire défiler sous le Brand Rankings Table.
3. Observer la section TopConceptsChart.

**Résultat attendu :**
La section TopConceptsChart est affichée après le Brand Rankings Table. Les topics et concepts-clés de sentiment sont listés pour la catégorie courante.

**Critère d'acceptation couvert :** CA-019, CA-020

---

## SENTIMENT-002 — Mise à jour des concepts au changement de filtre

| Champ | Valeur |
|---|---|
| **ID** | SENTIMENT-002 |
| **Module** | Sentiment & Key Concepts |
| **Fonctionnalité** | F-006 — Sentiment & Key Concepts |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Rapport multi-marché avec données perception par marché. |

**Étapes :**
1. Naviguer vers le Category View Dashboard en "All Markets".
2. Observer les topics de la section TopConceptsChart.
3. Changer le marché vers "Japan".
4. Observer les topics mis à jour.

**Résultat attendu :**
Les topics et concepts-clés se recalculent pour refléter les données du marché Japan. Les topics peuvent différer de ceux en "All Markets".

**Critère d'acceptation couvert :** CA-021

---

## SENTIMENT-003 — Mise à jour des concepts au changement de filtre LLM

| Champ | Valeur |
|---|---|
| **ID** | SENTIMENT-003 |
| **Module** | Sentiment & Key Concepts |
| **Fonctionnalité** | F-006 — Sentiment & Key Concepts |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Dashboard avec 3 LLM activés. |

**Étapes :**
1. Naviguer vers le Category View Dashboard avec 3 LLM actifs.
2. Observer les topics.
3. Désactiver 2 LLM (garder Gemini uniquement).
4. Observer les topics mis à jour.

**Résultat attendu :**
Les topics et concepts-clés se recalculent pour les données Gemini uniquement. Les topics peuvent varier selon le LLM source.

**Critère d'acceptation couvert :** CA-021

---

## Module : QUESTIONS — F-007 Unified Questions Table

---

## QUESTIONS-001 — Affichage nominal du tableau Unified Questions

| Champ | Valeur |
|---|---|
| **ID** | QUESTIONS-001 |
| **Module** | Unified Questions Table |
| **Fonctionnalité** | F-007 — Unified Questions Table |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Rapport avec questions visibility ET competitive. Rapport multi-marché. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer le Unified Questions Table.

**Données de test :**
- Questions visibility : 5
- Questions competitive : 3
- Rapport multi-marché : US, Germany

**Résultat attendu :**
Le tableau affiche les 8 questions (visibility + competitive) avec les colonnes : icône type (V pour visibility / C pour competitive), texte de la question, winner/themes (avec badge "Split" si applicable), market flag (drapeau pour les marchés US/Germany).

**Critère d'acceptation couvert :** CA-024

---

## QUESTIONS-002 — Labels texte du filtre Favorability

| Champ | Valeur |
|---|---|
| **ID** | QUESTIONS-002 |
| **Module** | Unified Questions Table |
| **Fonctionnalité** | F-007 — Unified Questions Table |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Tableau Unified Questions affiché. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer le filtre de favorabilité au-dessus ou dans le header du tableau.

**Résultat attendu :**
Le filtre affiche exactement 3 options en texte : "Favorable", "Split", "Not Favorable". Aucune icône seule, aucun code couleur sans label texte. Les labels correspondent exactement à ces libellés.

**Critère d'acceptation couvert :** CA-022

---

## QUESTIONS-003 — Filtre "Not Favorable" : affichage des questions non gagnées

| Champ | Valeur |
|---|---|
| **ID** | QUESTIONS-003 |
| **Module** | Unified Questions Table |
| **Fonctionnalité** | F-007 — Unified Questions Table |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Tableau avec questions où la marque cible n'est pas toujours #1. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Appliquer le filtre "Not Favorable".
3. Observer les questions affichées.

**Données de test :**
- Questions où la marque n'est pas #1 (visibility) ou n'a pas gagné (competitive) : 3 questions

**Résultat attendu :**
Seules les questions où la marque cible n'est PAS classée #1 (visibility) OU n'a PAS gagné (competitive) sont affichées. Les questions "Favorable" sont masquées.

**Critère d'acceptation couvert :** CA-023

---

## QUESTIONS-004 — Indicateur "Split" sur une question avec désaccord entre LLMs

| Champ | Valeur |
|---|---|
| **ID** | QUESTIONS-004 |
| **Module** | Unified Questions Table |
| **Fonctionnalité** | F-007 — Unified Questions Table |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Question competitive où ChatGPT désigne TeslaBrand gagnant et Gemini désigne BMW gagnant. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Localiser dans le tableau une question competitive avec résultats divergents entre LLMs.
3. Observer la colonne winner/themes pour cette question.

**Données de test :**
- Question : "Which brand offers the best range for electric vehicles?"
- ChatGPT : TeslaBrand gagnant
- Gemini : BMW gagnant

**Résultat attendu :**
La colonne winner/themes affiche l'indicateur "Split" pour cette question, signalant que les LLMs ne s'accordent pas sur le gagnant. Le badge "Split" est visuellement distinct.

**Critère d'acceptation couvert :** CA-024

---

## QUESTIONS-005 — Clic sur une ligne : ouverture du side panel

| Champ | Valeur |
|---|---|
| **ID** | QUESTIONS-005 |
| **Module** | Unified Questions Table |
| **Fonctionnalité** | F-007 — Unified Questions Table |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Tableau Unified Questions affiché avec au moins une question. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Cliquer sur la ligne d'une question visibility.
3. Observer le side panel qui s'ouvre.

**Données de test :**
- Question visibility : "What are the top 5 EV brands in 2024?"
- Marché : US

**Résultat attendu :**
Un side panel s'ouvre avec : (1) texte complet de la question, (2) ranking complet par LLM (top entités avec badges de rang ex: #1, #2, #3...), (3) liens vers les sources citées, (4) contexte marché (US). Le side panel est scrollable si le contenu dépasse la hauteur visible.

**Critère d'acceptation couvert :** CA-025

---

## QUESTIONS-006 — Barre de favorabilité dans le header collapsible

| Champ | Valeur |
|---|---|
| **ID** | QUESTIONS-006 |
| **Module** | Unified Questions Table |
| **Fonctionnalité** | F-007 — Unified Questions Table |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Tableau Unified Questions affiché avec questions de différentes favorabilités. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer le header du Unified Questions Table.
3. Vérifier la présence d'une barre de favorabilité dans ce header.
4. Cliquer sur le header pour le collapsible.

**Données de test :**
- Questions Favorable : 5 | Split : 2 | Not Favorable : 3

**Résultat attendu :**
La barre de favorabilité dans le header affiche une répartition visuelle des proportions Favorable/Split/Not Favorable. Le tableau se collapse/expand au clic sur le header. La barre reste visible même en état collapsé.

**Critère d'acceptation couvert :** CA-026

---

## QUESTIONS-007 — Filtre "Not Favorable" avec 0 résultat

| Champ | Valeur |
|---|---|
| **ID** | QUESTIONS-007 |
| **Module** | Unified Questions Table |
| **Fonctionnalité** | F-007 — Unified Questions Table |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Rapport où la marque cible est #1 sur toutes les questions (100% favorable). |

**Étapes :**
1. Naviguer vers le Category View Dashboard d'un rapport 100% favorable.
2. Appliquer le filtre "Not Favorable".
3. Observer le contenu du tableau.

**Résultat attendu :**
Un message "No results" (ou équivalent) s'affiche dans le tableau. Le tableau ne reste pas vide sans indication. Le filtre reste accessible pour être modifié. (Ambiguïté non résolue : filtre désactivé ou message vide ?)

**Critère d'acceptation couvert :** CA-023

---

## QUESTIONS-008 — Question avec un seul LLM actif : pas d'indicateur Split

| Champ | Valeur |
|---|---|
| **ID** | QUESTIONS-008 |
| **Module** | Unified Questions Table |
| **Fonctionnalité** | F-007 — Unified Questions Table |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Dashboard avec un seul LLM activé (Gemini). |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Désactiver tous les LLM sauf Gemini.
3. Observer les questions dans le tableau.

**Résultat attendu :**
Aucune question n'affiche le badge "Split" (impossible avec un seul LLM). Les questions affichent directement le gagnant désigné par Gemini sans ambiguïté de split.

**Critère d'acceptation couvert :** CA-024

---

## QUESTIONS-009 — Performance : filtrage mémoïsé sur grand ensemble de questions

| Champ | Valeur |
|---|---|
| **ID** | QUESTIONS-009 |
| **Module** | Unified Questions Table |
| **Fonctionnalité** | F-007 — Unified Questions Table |
| **Type** | Performance |
| **Priorité** | P2 |
| **Préconditions** | Rapport avec ≥ 100 questions (visibility + competitive). |

**Étapes :**
1. Naviguer vers le Category View Dashboard d'un rapport avec 100+ questions.
2. Appliquer le filtre "Favorable".
3. Mesurer le temps de rendu du tableau.
4. Changer le filtre vers "Not Favorable".
5. Mesurer le temps de rendu.
6. Revenir au filtre "Favorable".
7. Mesurer le temps de rendu (doit être plus rapide grâce à la mémoïsation).

**Données de test :**
- Nombre de questions : 120 (80 visibility + 40 competitive)

**Résultat attendu :**
Le premier filtrage prend moins de 2 secondes. Les filtrages suivants sur des critères déjà appliqués sont notablement plus rapides (mémoïsation active). L'interface ne se fige pas.

**Critère d'acceptation couvert :** CA-024

---

## Module : PERCEPTION — F-008 Perception Questions Table

---

## PERCEPTION-001 — Affichage nominal du tableau Perception Questions

| Champ | Valeur |
|---|---|
| **ID** | PERCEPTION-001 |
| **Module** | Perception Questions Table |
| **Fonctionnalité** | F-008 — Perception Questions Table |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Rapport avec questions perception analysées couvrant les 3 sentiments. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer le Perception Questions Table.

**Données de test :**
- Questions positive : 4 | Mixed : 3 | Negative : 2

**Résultat attendu :**
Le tableau affiche les questions de perception avec : texte de la question, indicateur sentiment (Positive/Mixed/Negative), badge LLM indiquant quel(s) provider(s) ont analysé la question.

**Critère d'acceptation couvert :** CA-027, CA-028

---

## PERCEPTION-002 — Filtre sentiment : Positive, Mixed, Negative

| Champ | Valeur |
|---|---|
| **ID** | PERCEPTION-002 |
| **Module** | Perception Questions Table |
| **Fonctionnalité** | F-008 — Perception Questions Table |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Tableau Perception Questions affiché avec questions de 3 sentiments. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer les options du filtre sentiment.
3. Appliquer le filtre "Negative".
4. Observer les questions affichées.

**Résultat attendu :**
Le filtre affiche exactement : "Positive", "Mixed", "Negative". Après sélection de "Negative", seules les 2 questions à sentiment négatif sont affichées. Les questions Positive et Mixed sont masquées.

**Critère d'acceptation couvert :** CA-027

---

## PERCEPTION-003 — Clic sur une ligne : side panel avec réponses LLM

| Champ | Valeur |
|---|---|
| **ID** | PERCEPTION-003 |
| **Module** | Perception Questions Table |
| **Fonctionnalité** | F-008 — Perception Questions Table |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Tableau Perception Questions affiché avec au moins une question. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Cliquer sur une ligne du Perception Questions Table.
3. Observer le side panel.

**Données de test :**
- Question : "How is TeslaBrand perceived in terms of sustainability?"

**Résultat attendu :**
Un side panel s'ouvre avec : (1) réponses brutes de chaque LLM provider séparées, (2) thèmes/topics extraits de ces réponses, (3) citations sources avec URLs. Le side panel est distinct de celui du Unified Questions Table.

**Critère d'acceptation couvert :** CA-029

---

## PERCEPTION-004 — LLM avec réponse vide dans le side panel

| Champ | Valeur |
|---|---|
| **ID** | PERCEPTION-004 |
| **Module** | Perception Questions Table |
| **Fonctionnalité** | F-008 — Perception Questions Table |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Question de perception où un LLM (ex: Perplexity) n'a pas fourni de réponse. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Cliquer sur une ligne dont un LLM n'a pas de réponse.
3. Observer la section Perplexity dans le side panel.

**Données de test :**
- LLM sans réponse : Perplexity (réponse = null ou string vide)

**Résultat attendu :**
Le side panel affiche "(No response)" ou équivalent pour la section Perplexity. La section n'est pas absente mais indique explicitement l'absence de réponse. Les réponses des autres LLM sont affichées normalement.

**Critère d'acceptation couvert :** CA-029

---

## PERCEPTION-005 — Filtre "Negative" avec 0 question négative

| Champ | Valeur |
|---|---|
| **ID** | PERCEPTION-005 |
| **Module** | Perception Questions Table |
| **Fonctionnalité** | F-008 — Perception Questions Table |
| **Type** | Limite |
| **Priorité** | P3 |
| **Préconditions** | Rapport sans questions à sentiment négatif. |

**Étapes :**
1. Naviguer vers le Category View Dashboard d'un rapport 100% positif/mixed.
2. Appliquer le filtre "Negative".
3. Observer le contenu du tableau.

**Résultat attendu :**
Un message "No negative perceptions" (ou "No results") s'affiche. Le filtre ne plante pas. L'utilisateur peut changer de filtre librement.

**Critère d'acceptation couvert :** CA-027

---

## PERCEPTION-006 — Classification globale d'une question Mixed/Positive selon LLM

| Champ | Valeur |
|---|---|
| **ID** | PERCEPTION-006 |
| **Module** | Perception Questions Table |
| **Fonctionnalité** | F-008 — Perception Questions Table |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Question de perception classée "Mixed" par Gemini et "Positive" par ChatGPT. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Localiser une question avec sentiment divergent entre LLMs.
3. Observer l'indicateur sentiment global dans la colonne sentiment du tableau.

**Données de test :**
- ChatGPT : Positive
- Gemini : Mixed
- Perplexity : Positive

**Résultat attendu :**
Une classification globale unique est affichée (ex: "Mixed" par majorité ou logique de priorité définie). La classification est cohérente et non aléatoire entre rechargements.

**Critère d'acceptation couvert :** CA-028

---

## Module : DISTRIB — F-009 Sentiment Distribution Chart

---

## DISTRIB-001 — Affichage nominal de la barre de distribution sentiment

| Champ | Valeur |
|---|---|
| **ID** | DISTRIB-001 |
| **Module** | Sentiment Distribution Chart |
| **Fonctionnalité** | F-009 — Sentiment Distribution Chart |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Rapport avec questions perception couvrant les 3 types de sentiment. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer la Sentiment Distribution Chart.

**Données de test :**
- Positive : 50% | Mixed : 30% | Negative : 20%

**Résultat attendu :**
Une barre horizontale s'affiche avec 3 segments colorés : vert (50% Positive), orange (30% Mixed), rouge (20% Negative). Les largeurs sont visuellement proportionnelles aux pourcentages. Les labels de chaque segment sont lisibles.

**Critère d'acceptation couvert :** CA-030, CA-031

---

## DISTRIB-002 — Mise à jour du chart au changement de filtre

| Champ | Valeur |
|---|---|
| **ID** | DISTRIB-002 |
| **Module** | Sentiment Distribution Chart |
| **Fonctionnalité** | F-009 — Sentiment Distribution Chart |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Rapport multi-marché avec distributions sentiment différentes par marché. |

**Étapes :**
1. Naviguer vers le Category View Dashboard en "All Markets".
2. Observer les proportions des 3 segments.
3. Changer le marché vers "Japan".
4. Observer les nouvelles proportions.

**Résultat attendu :**
Les proportions des 3 segments se mettent à jour pour refléter la distribution sentiment du marché Japan. Les largeurs des segments changent en conséquence.

**Critère d'acceptation couvert :** CA-032

---

## DISTRIB-003 — Distribution 100% positive : segments Mixed et Negative

| Champ | Valeur |
|---|---|
| **ID** | DISTRIB-003 |
| **Module** | Sentiment Distribution Chart |
| **Fonctionnalité** | F-009 — Sentiment Distribution Chart |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Rapport avec 100% de questions à sentiment positif. |

**Étapes :**
1. Naviguer vers le Category View Dashboard d'un rapport 100% positif.
2. Observer la Sentiment Distribution Chart.

**Données de test :**
- Positive : 100% | Mixed : 0% | Negative : 0%

**Résultat attendu :**
La barre affiche un segment vert unique (100%). Les segments Mixed et Negative sont soit absents soit affichés à 0px de largeur sans débordement visuel. Aucun segment fantôme ou label 0% mal positionné n'est visible.

**Critère d'acceptation couvert :** CA-030, CA-031

---

## DISTRIB-004 — Chart avec 0 question de perception

| Champ | Valeur |
|---|---|
| **ID** | DISTRIB-004 |
| **Module** | Sentiment Distribution Chart |
| **Fonctionnalité** | F-009 — Sentiment Distribution Chart |
| **Type** | Limite |
| **Priorité** | P3 |
| **Préconditions** | Rapport sans aucune question de perception analysée pour cette catégorie. |

**Étapes :**
1. Naviguer vers le Category View Dashboard d'un rapport sans données perception.
2. Observer la zone où s'afficherait normalement la Sentiment Distribution Chart.

**Résultat attendu :**
Le chart est soit masqué, soit affiche un état vide avec un message approprié (ex: "No perception data available"). Aucune barre vide sans indication n'est affichée.

**Critère d'acceptation couvert :** CA-030

---

## Module : SOURCES — F-010 AI Citation Sources

---

## SOURCES-001 — Affichage nominal du stacked bar chart des types de sources

| Champ | Valeur |
|---|---|
| **ID** | SOURCES-001 |
| **Module** | AI Citation Sources |
| **Fonctionnalité** | F-010 — AI Citation Sources (viewContext='category') |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Rapport avec données de citation disponibles couvrant plusieurs types de sources. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer la section AI Citation Sources.
3. Observer le stacked bar chart.

**Résultat attendu :**
Un stacked bar chart s'affiche avec les types de sources (11-category taxonomy). Chaque type de source est représenté par une couleur distincte. Une légende cliquable est présente. Les comptages par type sont visibles.

**Critère d'acceptation couvert :** CA-033

---

## SOURCES-002 — Filtrage par type de source via la légende

| Champ | Valeur |
|---|---|
| **ID** | SOURCES-002 |
| **Module** | AI Citation Sources |
| **Fonctionnalité** | F-010 — AI Citation Sources |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Stacked bar chart affiché avec au moins 3 types de sources. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Cliquer sur un type de source dans la légende du chart (ex: "News").
3. Observer le filtrage appliqué au tableau de domaines.

**Données de test :**
- Type sélectionné : "News"

**Résultat attendu :**
Le tableau des domaines filtre pour n'afficher que les domaines du type "News". Le chart met en évidence le type sélectionné. Un clic sur le même type de source désactive le filtre (toggle).

**Critère d'acceptation couvert :** CA-033

---

## SOURCES-003 — Affichage du tableau des domaines avec colonnes complètes

| Champ | Valeur |
|---|---|
| **ID** | SOURCES-003 |
| **Module** | AI Citation Sources |
| **Fonctionnalité** | F-010 — AI Citation Sources |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Rapport avec au moins 5 domaines cités ayant des priority scores variés. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer le tableau des domaines dans la section AI Citation Sources.

**Données de test :**
- Domaines : tesla.com (priority=75), nytimes.com (priority=65), forbes.com (priority=45), techcrunch.com (priority=25), bmw.com (priority=70)

**Résultat attendu :**
Le tableau affiche les colonnes : (1) Domain avec favicon, (2) Source Type avec badge coloré, (3) Priority avec barre de score (tesla.com=Rouge≥70, nytimes.com=Amber 50-69, forbes.com=Blue 30-49, techcrunch.com=Slate<30), (4) Citations count, (5) Impact Area avec icônes Eye=visibility et Trophy=competitive.

**Critère d'acceptation couvert :** CA-034

---

## SOURCES-004 — viewContext='category' : uniquement Visibility Gaps + Competitive Losses

| Champ | Valeur |
|---|---|
| **ID** | SOURCES-004 |
| **Module** | AI Citation Sources |
| **Fonctionnalité** | F-010 — AI Citation Sources |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Dashboard Category View affiché (viewContext='category'). Données Visibility Gaps, Competitive Losses et Reputation Issues disponibles. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Expander une ligne du tableau de domaines.
3. Observer les panels affichés dans la ligne expandée.

**Résultat attendu :**
Seuls 2 panels sont affichés : "Visibility Gaps" (border bleue) et "Competitive Losses" (border ambre). Le panel "Reputation Issues" est absent (déplacé dans EPIC-002 Actions Center). Ce comportement est spécifique au viewContext='category'.

**Critère d'acceptation couvert :** CA-035

---

## SOURCES-005 — Expand d'une ligne : panels Visibility Gaps + Competitive Losses + LLM Citations

| Champ | Valeur |
|---|---|
| **ID** | SOURCES-005 |
| **Module** | AI Citation Sources |
| **Fonctionnalité** | F-010 — AI Citation Sources |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Tableau de domaines affiché avec au moins un domaine ayant des Visibility Gaps et Competitive Losses. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Cliquer sur le bouton expand d'un domaine (ex: nytimes.com).
3. Observer les panels affichés.

**Résultat attendu :**
Trois sections s'affichent : (1) Visibility Gaps avec border bleue, (2) Competitive Losses avec border ambre, (3) LLM Citations avec badges par LLM provider. Les contenus sont distincts et non mélangés.

**Critère d'acceptation couvert :** CA-036

---

## SOURCES-006 — Cited URLs : affichage jusqu'à 6 items et bouton "View All"

| Champ | Valeur |
|---|---|
| **ID** | SOURCES-006 |
| **Module** | AI Citation Sources |
| **Fonctionnalité** | F-010 — AI Citation Sources |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Domaine avec plus de 6 URLs citées (ex: 10 citations). |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Expander la ligne d'un domaine avec 10 URLs.
3. Observer la section "Cited URLs".
4. Cliquer sur "View All".

**Données de test :**
- Domaine : nytimes.com avec 10 URLs citées

**Résultat attendu :**
La section "Cited URLs" affiche 6 items au maximum. Un bouton "View All" est visible. Chaque item affiche : favicon, titre lisible, domain/path, logos LLM provider, badge source type. Au clic sur "View All", une modal scrollable s'ouvre avec les 10 URLs complètes.

**Critère d'acceptation couvert :** CA-037

---

## SOURCES-007 — Fallback favicon générique pour domaine sans favicon

| Champ | Valeur |
|---|---|
| **ID** | SOURCES-007 |
| **Module** | AI Citation Sources |
| **Fonctionnalité** | F-010 — AI Citation Sources |
| **Type** | Limite |
| **Priorité** | P3 |
| **Préconditions** | Domaine cité dont le favicon n'est pas disponible (ex: site obscur ou favicon 404). |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Observer le tableau de domaines pour un domaine sans favicon.

**Données de test :**
- Domaine sans favicon : obscuredomain.example.com

**Résultat attendu :**
Une icône générique (ex: icône globe ou lettre) est affichée à la place du favicon manquant. Aucun espace vide ou image cassée n'est visible dans la colonne Domain.

**Critère d'acceptation couvert :** CA-034

---

## SOURCES-008 — Priority score = 70 exactement : classification Rouge ou Amber

| Champ | Valeur |
|---|---|
| **ID** | SOURCES-008 |
| **Module** | AI Citation Sources |
| **Fonctionnalité** | F-010 — AI Citation Sources |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Domaine avec un priority score = 70 exactement. |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Identifier un domaine avec priority score = 70.
3. Observer la couleur de la barre Priority.

**Données de test :**
- Domaine : exactscore.com (priority = 70)

**Résultat attendu :**
La barre Priority est de couleur Rouge (score ≥ 70 est inclusif = Rouge). Si la borne est exclusive, la couleur serait Amber. Ce test valide la borne inclusive/exclusive. (Ambiguïté AMB-006 à confirmer : Rouge si ≥70 inclusif.)

**Critère d'acceptation couvert :** CA-034

---

## Module : MULTIMARKET — F-011 Multi-Market Support

---

## MULTIMARKET-001 — Dropdown avec N marchés + "All Markets"

| Champ | Valeur |
|---|---|
| **ID** | MULTIMARKET-001 |
| **Module** | Multi-Market Support |
| **Fonctionnalité** | F-011 — Multi-Market Support |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Rapport avec exactement 3 marchés (US, Germany, Japan). |

**Étapes :**
1. Naviguer vers le Category View Dashboard.
2. Ouvrir le market selector dropdown.
3. Observer la liste complète des options.

**Données de test :**
- Marchés du rapport : US, Germany, Japan

**Résultat attendu :**
Le dropdown affiche exactement 4 options : "All Markets", "US", "Germany", "Japan". L'option "All Markets" est en tête de liste. Aucun marché supplémentaire ni manquant.

**Critère d'acceptation couvert :** CA-038, CA-040

---

## MULTIMARKET-002 — Filtrage global de toutes les sections au changement de marché

| Champ | Valeur |
|---|---|
| **ID** | MULTIMARKET-002 |
| **Module** | Multi-Market Support |
| **Fonctionnalité** | F-011 — Multi-Market Support |
| **Type** | Fonctionnel |
| **Priorité** | P1 |
| **Préconditions** | Rapport multi-marché complété avec toutes les sections affichées. |

**Étapes :**
1. Naviguer vers le Category View Dashboard en "All Markets".
2. Sélectionner "US" dans le market selector.
3. Vérifier chacune des sections : Matrix, Metric Cards, Questions Unified, Questions Perception, Sources, Sentiment Chart.

**Données de test :**
- Marché sélectionné : US

**Résultat attendu :**
Toutes les sections (matrix, questions unified, perception questions, sources, métriques, sentiment chart) filtrent simultanément sur le marché US. Aucune section ne conserve des données "All Markets".

**Critère d'acceptation couvert :** CA-039

---

## MULTIMARKET-003 — Rapport single-market : market selector non affiché

| Champ | Valeur |
|---|---|
| **ID** | MULTIMARKET-003 |
| **Module** | Multi-Market Support |
| **Fonctionnalité** | F-011 — Multi-Market Support |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Rapport avec un seul marché (US uniquement). |

**Étapes :**
1. Naviguer vers le Category View Dashboard d'un rapport single-market.
2. Observer le header.

**Résultat attendu :**
Le market selector n'est pas affiché dans le header (comportement attendu pour single-market). Le dashboard affiche les données du marché unique sans dropdown. (Ambiguïté AMB-001 — à clarifier : masqué vs lecture seule.)

**Critère d'acceptation couvert :** CA-038

---

## MULTIMARKET-004 — Marché sans données pour cette catégorie

| Champ | Valeur |
|---|---|
| **ID** | MULTIMARKET-004 |
| **Module** | Multi-Market Support |
| **Fonctionnalité** | F-011 — Multi-Market Support |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Rapport multi-marché où le marché "Japan" n'a pas de données pour la catégorie "Electric Vehicles". |

**Étapes :**
1. Naviguer vers le Category View Dashboard en "All Markets".
2. Sélectionner "Japan" dans le market selector.
3. Observer l'état du dashboard.

**Données de test :**
- Marché sélectionné : Japan
- Données disponibles pour Japan/Electric Vehicles : 0

**Résultat attendu :**
Toutes les sections affichent un état vide avec un message approprié (ex: "No data available for Japan in this category"). Aucune section ne crash ou n'affiche des données résiduelles d'un autre marché.

**Critère d'acceptation couvert :** CA-039

---

## MULTIMARKET-005 — Persistance du marché sélectionné lors du changement de catégorie

| Champ | Valeur |
|---|---|
| **ID** | MULTIMARKET-005 |
| **Module** | Multi-Market Support |
| **Fonctionnalité** | F-011 — Multi-Market Support |
| **Type** | Fonctionnel |
| **Priorité** | P2 |
| **Préconditions** | Rapport multi-marché avec 2 catégories. Marché "Germany" sélectionné sur la catégorie 1. |

**Étapes :**
1. Naviguer vers le Category View Dashboard "Electric Vehicles" en mode "Germany".
2. Naviguer vers la catégorie "Autonomous Driving" via la sidebar.
3. Observer le marché sélectionné sur la nouvelle catégorie.

**Résultat attendu :**
Le comportement de persistance est documenté : soit "Germany" reste sélectionné sur la nouvelle catégorie, soit le marché revient à "All Markets". Quelle que soit la logique, elle est cohérente à chaque navigation.

**Critère d'acceptation couvert :** CA-038, CA-039

---

## Module : PENDING — F-012 Analysis Pending State

---

## PENDING-001 — Affichage de l'état "Analysis Pending" pour une catégorie en cours

| Champ | Valeur |
|---|---|
| **ID** | PENDING-001 |
| **Module** | Analysis Pending State |
| **Fonctionnalité** | F-012 — Analysis Pending State |
| **Type** | Fonctionnel |
| **Priorité** | P3 |
| **Préconditions** | Rapport en cours de traitement pour la catégorie "Electric Vehicles". Analyse non complète (statut = IN_PROGRESS). |

**Étapes :**
1. Naviguer vers le Category View Dashboard de "Electric Vehicles" pendant que l'analyse est en cours.
2. Observer l'état affiché.

**Résultat attendu :**
L'écran affiche : (1) icône Clock visible, (2) titre "Analysis Pending", (3) description "Analysis for Electric Vehicles is in progress", (4) indicateur de progression si disponible. Le contenu normal du dashboard n'est pas affiché (pour éviter des données incomplètes).

**Critère d'acceptation couvert :** CA-041

---

## PENDING-002 — Analyse en état FAILED : écran dédié ou "Pending" générique

| Champ | Valeur |
|---|---|
| **ID** | PENDING-002 |
| **Module** | Analysis Pending State |
| **Fonctionnalité** | F-012 — Analysis Pending State |
| **Type** | Négatif |
| **Priorité** | P2 |
| **Préconditions** | Rapport avec une analyse en état FAILED pour la catégorie. |

**Étapes :**
1. Naviguer vers le Category View Dashboard d'une catégorie dont l'analyse a échoué (FAILED).
2. Observer l'état affiché.

**Résultat attendu :**
Un écran d'erreur dédié est affiché (différent de "Analysis Pending") avec un message indiquant l'échec et une action corrective possible (ex: "Retry" ou "Contact support"). (Ambiguïté AMB-007 — à confirmer si même écran Pending ou erreur dédiée.)

**Critère d'acceptation couvert :** CA-041

---

## PENDING-003 — Analyse partiellement complète : affichage des données disponibles

| Champ | Valeur |
|---|---|
| **ID** | PENDING-003 |
| **Module** | Analysis Pending State |
| **Fonctionnalité** | F-012 — Analysis Pending State |
| **Type** | Limite |
| **Priorité** | P2 |
| **Préconditions** | Analyse partiellement complète : dimension Visibility terminée, dimensions Competitive et Perception en cours. |

**Étapes :**
1. Naviguer vers le Category View Dashboard d'une catégorie avec analyse partielle.
2. Observer l'état du dashboard.

**Données de test :**
- Visibility : COMPLETE
- Competitive : IN_PROGRESS
- Perception : IN_PROGRESS

**Résultat attendu :**
Le comportement est l'un des deux suivants (à confirmer avec l'équipe produit selon AMB-008) : (a) les sections Visibility/Matrix/Rankings sont affichées avec les données disponibles, et les sections Competitive/Perception affichent "In progress", OU (b) l'écran "Analysis Pending" masque tout le contenu jusqu'à complétion totale.

**Critère d'acceptation couvert :** CA-041

---

## Récapitulatif de Couverture

### Total des cas de test : 69

---

### Répartition par module

| Module | ID Cas | Nombre de cas |
|---|---|---|
| Header & Filtres (F-001) | HEADER-001 à HEADER-007 | 7 |
| Brand Prioritization Matrix (F-002) | MATRIX-001 à MATRIX-010 | 10 |
| 5 Metric Cards (F-003) | METRICS-001 à METRICS-005 | 5 |
| Perception Summary Banner (F-004) | BANNER-001 à BANNER-005 | 5 |
| Brand Rankings Table (F-005) | RANKINGS-001 à RANKINGS-004 | 4 |
| Sentiment & Key Concepts (F-006) | SENTIMENT-001 à SENTIMENT-003 | 3 |
| Unified Questions Table (F-007) | QUESTIONS-001 à QUESTIONS-009 | 9 |
| Perception Questions Table (F-008) | PERCEPTION-001 à PERCEPTION-006 | 6 |
| Sentiment Distribution Chart (F-009) | DISTRIB-001 à DISTRIB-004 | 4 |
| AI Citation Sources (F-010) | SOURCES-001 à SOURCES-008 | 8 |
| Multi-Market Support (F-011) | MULTIMARKET-001 à MULTIMARKET-005 | 5 |
| Analysis Pending State (F-012) | PENDING-001 à PENDING-003 | 3 |
| **TOTAL** | | **69** |

---

### Répartition par priorité

| Priorité | Nombre de cas | Pourcentage |
|---|---|---|
| P1 — Critique | 27 | 39% |
| P2 — Majeur | 34 | 49% |
| P3 — Mineur | 8 | 12% |
| **TOTAL** | **69** | **100%** |

**Cas P1 :** HEADER-001, HEADER-002, HEADER-003, HEADER-004, HEADER-006, MATRIX-001, MATRIX-002, MATRIX-003, MATRIX-004, METRICS-001, METRICS-002, METRICS-003, METRICS-005, BANNER-004, RANKINGS-004, QUESTIONS-001, QUESTIONS-002, QUESTIONS-003, QUESTIONS-004, QUESTIONS-005, SOURCES-004, MULTIMARKET-001, MULTIMARKET-002

---

### Répartition par type

| Type | Nombre de cas | Pourcentage |
|---|---|---|
| Fonctionnel | 41 | 59% |
| Limite | 18 | 26% |
| Négatif | 4 | 6% |
| Performance | 1 | 2% |
| Sécurité | 0 | 0% |
| **TOTAL** | **69** | **100%** |

---

### Couverture des critères d'acceptation

| Critère | Cas de test couvrant |
|---|---|
| CA-001 | HEADER-001, HEADER-002, HEADER-007 |
| CA-002 | HEADER-003 |
| CA-003 | HEADER-004, HEADER-006, HEADER-007 |
| CA-004 | MATRIX-001, MATRIX-007, MATRIX-008, MATRIX-009 |
| CA-005 | MATRIX-002, MATRIX-003 |
| CA-006 | MATRIX-004 |
| CA-007 | MATRIX-001 |
| CA-008 | MATRIX-005 |
| CA-009 | MATRIX-006 |
| CA-010 | MATRIX-007 |
| CA-011 | METRICS-001, METRICS-004, METRICS-005 |
| CA-012 | METRICS-002, METRICS-003, METRICS-004 |
| CA-013 | BANNER-001 |
| CA-014 | BANNER-002 |
| CA-015 | BANNER-003, BANNER-004, BANNER-005 |
| CA-016 | RANKINGS-001, RANKINGS-004 |
| CA-017 | RANKINGS-001, RANKINGS-003, RANKINGS-004 |
| CA-018 | RANKINGS-002 |
| CA-019 | SENTIMENT-001 |
| CA-020 | SENTIMENT-001 |
| CA-021 | SENTIMENT-002, SENTIMENT-003 |
| CA-022 | QUESTIONS-002 |
| CA-023 | QUESTIONS-003, QUESTIONS-007 |
| CA-024 | QUESTIONS-001, QUESTIONS-004, QUESTIONS-008, QUESTIONS-009 |
| CA-025 | QUESTIONS-005 |
| CA-026 | QUESTIONS-006 |
| CA-027 | PERCEPTION-001, PERCEPTION-002, PERCEPTION-005 |
| CA-028 | PERCEPTION-001, PERCEPTION-006 |
| CA-029 | PERCEPTION-003, PERCEPTION-004 |
| CA-030 | DISTRIB-001, DISTRIB-003, DISTRIB-004 |
| CA-031 | DISTRIB-001, DISTRIB-003 |
| CA-032 | DISTRIB-002 |
| CA-033 | SOURCES-001, SOURCES-002 |
| CA-034 | SOURCES-003, SOURCES-007, SOURCES-008 |
| CA-035 | SOURCES-004 |
| CA-036 | SOURCES-005 |
| CA-037 | SOURCES-006 |
| CA-038 | MULTIMARKET-001, MULTIMARKET-003, MULTIMARKET-005 |
| CA-039 | MULTIMARKET-002, MULTIMARKET-004, MULTIMARKET-005 |
| CA-040 | MULTIMARKET-001 |
| CA-041 | PENDING-001, PENDING-002, PENDING-003 |

---

### Ambiguïtés couvertes par des cas de test

| Ambiguïté | Cas de test associé |
|---|---|
| AMB-001 — Single-market selector masqué ou lecture seule | HEADER-005, MULTIMARKET-003 |
| AMB-002 — Tous LLM désactivés : état vide ou blocage | HEADER-006 |
| AMB-003 — Endpoint 500 : fallback ou erreur visible | BANNER-004 |
| AMB-004 — Summary "All Markets" : global ou premier marché | BANNER-002 |
| AMB-005 — Critère "Split" : majorité ou 50/50 strict | QUESTIONS-004, QUESTIONS-008 |
| AMB-006 — Priority score = 70 : Rouge ou Amber | SOURCES-008 |
| AMB-007 — Analyse FAILED : même écran Pending ou erreur dédiée | PENDING-002 |
| AMB-008 — Analyse partielle : données visibles ou tout masqué | PENDING-003 |
