Importe les cas de test dans Quality Plus via le navigateur.

## Instructions

Utilise l'agent `quality-plus-importer` pour automatiser l'import dans Quality Plus.

**Prérequis :**
- `outputs/test-cases-import.csv` doit exister (généré par `/qa-format`)
- Quality Plus doit être accessible dans Chrome
- L'utilisateur doit être connecté à Quality Plus

**Source d'entrée :**
- Fichier : `outputs/test-cases-import.csv`
- URL Quality Plus : `$ARGUMENTS` (si fournie) ou détecter depuis les onglets ouverts

**Actions à effectuer :**
1. Vérifier que le fichier CSV existe et est valide
2. Lister les pages Chrome ouvertes
3. Naviguer vers Quality Plus (demander l'URL si nécessaire)
4. Vérifier la connexion de l'utilisateur
5. Accéder à la section "Cas de test" / Import
6. Uploader `outputs/test-cases-import.csv`
7. Valider et confirmer l'import
8. Vérifier le résultat et prendre un screenshot
9. Documenter le résultat dans `outputs/execution-results.md`

**Important :** Ne jamais écraser des cas existants sans confirmation explicite.

URL Quality Plus (optionnel) : $ARGUMENTS
