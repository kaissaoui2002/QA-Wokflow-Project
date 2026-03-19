Formate les cas de test pour l'import dans Quality Plus (CSV).

## Instructions

Utilise l'agent `test-formatter` pour transformer les cas de test en format d'import.

**Source d'entrée :**
- Lire `outputs/test-cases.md` (généré par `/qa-design`)
- Format de sortie par défaut : CSV (compatible Quality Plus)
- Si `$ARGUMENTS` contient "excel" ou "xlsx", adapter le formatage pour Excel

**Actions à effectuer :**
1. Lire tous les cas de test dans `outputs/test-cases.md`
2. Mapper chaque champ vers les colonnes Quality Plus :
   - Suite de tests ← Module/Fonctionnalité
   - ID du cas de test ← ID (TC-XXX)
   - Titre ← Titre
   - Préconditions ← Préconditions
   - Étapes ← Étapes (séparées par `\n`)
   - Résultats attendus ← Résultat attendu
   - Priorité ← Priorité (P1/P2/P3)
   - Type ← Type
   - Statut ← "Non exécuté" (valeur par défaut)
3. Valider l'intégrité des données (IDs uniques, champs obligatoires non vides)
4. Générer `outputs/test-cases-import.csv` en UTF-8 avec BOM

**À la fin**, afficher le bilan de l'export avec nombre de cas et répartition.

Options : $ARGUMENTS
