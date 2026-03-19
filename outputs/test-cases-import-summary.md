# Résumé de Transformation — test-cases-import.csv

**Date :** 2026-03-18
**Source :** outputs/test-cases.md
**Sortie :** outputs/test-cases-import.csv
**Epic :** CATEGORY-001 (DIGIMIND-18640)

---

## Résultat de la transformation

| Indicateur | Valeur |
|---|---|
| Cas exportés | 69 |
| Suites de tests créées | 12 |
| Encodage | UTF-8 avec BOM |
| Séparateur | Virgule (,) |
| Statut par défaut | Non exécuté |

---

## Répartition par priorité

| Priorité | Nombre | Pourcentage |
|---|---|---|
| P1 — Critique | 24 | 35% |
| P2 — Majeur | 41 | 59% |
| P3 — Mineur | 4 | 6% |
| **TOTAL** | **69** | **100%** |

---

## Répartition par module (Suite de tests)

| Suite de tests | Nombre de cas |
|---|---|
| Header & Filtres | 7 |
| Brand Prioritization Matrix | 10 |
| 5 Metric Cards | 5 |
| Perception Summary Banner | 5 |
| Brand Rankings Table | 4 |
| Sentiment & Key Concepts | 3 |
| Unified Questions Table | 9 |
| Perception Questions Table | 6 |
| Sentiment Distribution Chart | 4 |
| AI Citation Sources | 8 |
| Multi-Market Support | 5 |
| Analysis Pending State | 3 |
| **TOTAL** | **69** |

---

## Répartition par type

| Type | Nombre |
|---|---|
| Fonctionnel | 41 |
| Limite | 18 |
| Négatif | 4 |
| Performance | 1 |
| Régression | 0 |
| Smoke | 0 |

---

## Validations effectuées

| Contrôle | Résultat |
|---|---|
| IDs uniques (pas de doublons) | Conforme — 69 IDs distincts |
| Champs obligatoires non vides | Conforme — aucun champ vide détecté |
| Priorités dans P1/P2/P3 | Conforme |
| Nombre de cas CSV = nombre source | Conforme — 69 cas dans les deux |
| Encodage UTF-8 avec BOM | Conforme |
| Statut "Non exécuté" sur tous les cas | Conforme |

---

## Avertissements

| Code | Description |
|---|---|
| WARN-001 | QUESTIONS-009 est de type "Performance". Ce type n'est pas dans la liste standard Quality Plus (Fonctionnel, Régression, Limite, Négatif, Smoke). Il a été conservé tel quel depuis la source. A vérifier avec l'administrateur Quality Plus avant import. |
| WARN-002 | Le récapitulatif du fichier source indiquait 27 cas P1. Le comptage réel sur les tableaux de données de chaque cas donne 24 cas P1. La valeur des tableaux individuels a été retenue car elle prime sur le récapitulatif agrégé (possibilité d'une erreur dans le récapitulatif source). |

---

## Règles de mapping appliquées

| Champ source | Colonne CSV Quality Plus |
|---|---|
| Fonctionnalité (F-001, F-002...) | Suite de tests |
| ID | ID du cas de test |
| Titre | Titre |
| Préconditions | Préconditions |
| Étapes numérotées | Étapes (séparées par \n) |
| Résultat attendu | Résultats attendus |
| Priorité | Priorité |
| Type | Type |
| (valeur fixe) | Statut = "Non exécuté" |
| Module | Module |
| (dérivé du type et du module) | Tags |

---

## Fichier généré

**Chemin absolu :** `C:\Stricture-QA\outputs\test-cases-import.csv`
