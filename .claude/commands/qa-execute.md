Exécute les cas de test sur l'application cible et enregistre les résultats.

## Instructions

Utilise l'agent `test-executor` pour exécuter les tests sur l'application.

**Source d'entrée :**
- Cas de test : `outputs/test-cases.md`
- URL de l'application : depuis `$ARGUMENTS` ou demander à l'utilisateur

**Parsing des arguments (`$ARGUMENTS`) :**
- URL seule → exécuter tous les cas sur cette URL
- `module:NomModule` → exécuter uniquement les cas du module spécifié
- `priority:P1` → exécuter uniquement les cas P1
- `from:TC-010` → reprendre l'exécution à partir de TC-010
- `tag:smoke` → exécuter uniquement les cas avec ce tag

**Actions à effectuer :**
1. Lire `outputs/test-cases.md` et appliquer le filtre
2. Ouvrir/naviguer vers l'application dans Chrome
3. Pour chaque cas de test (dans l'ordre P1 → P2 → P3) :
   a. Préparer les préconditions
   b. Exécuter les étapes
   c. Comparer le résultat observé au résultat attendu
   d. Enregistrer le statut : PASS / FAIL / BLOCKED / SKIPPED
   e. Prendre un screenshot en cas de FAIL
   f. Documenter les bugs dans `outputs/bugs-found.md`
4. Mettre à jour `outputs/execution-results.md` en temps réel
5. Continuer même en cas de FAIL (ne pas arrêter le cycle)

**À la fin**, afficher le tableau de bord : Total | PASS | FAIL | BLOCKED | SKIPPED | Taux de succès.

Paramètres : $ARGUMENTS
