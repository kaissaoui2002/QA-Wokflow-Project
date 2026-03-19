Conçoit les cas de test détaillés à partir des exigences analysées.

## Instructions

Utilise l'agent `test-designer` pour concevoir les cas de test.

**Source d'entrée :**
- Lire `outputs/requirements.md` (généré par `/qa-analyze`)
- Si l'argument `$ARGUMENTS` précise un module ou filtre, ne concevoir que les cas pour ce module

**Actions à effectuer :**
1. Lire les exigences dans `outputs/requirements.md`
2. Pour chaque fonctionnalité, appliquer les techniques adaptées :
   - Partitions d'équivalence et valeurs aux limites pour les champs de saisie
   - Tables de décision pour les combinaisons de conditions
   - Transitions d'état pour les workflows
3. Concevoir les scénarios nominaux, alternatifs et d'erreur
4. Identifier les cas limites
5. Générer `outputs/test-cases.md` avec tous les cas structurés

**À la fin**, afficher :
- Nombre total de cas de test conçus
- Répartition par module
- Répartition par priorité (P1/P2/P3)
- Répartition par type (Fonctionnel/Limite/Négatif/etc.)

Filtre optionnel : $ARGUMENTS
